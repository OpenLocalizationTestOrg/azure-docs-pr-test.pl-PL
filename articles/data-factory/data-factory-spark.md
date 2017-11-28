---
title: aaaInvoke Spark programy z fabryki danych Azure | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak programy Spark tooinvoke z fabryki danych Azure przy użyciu hello działania MapReduce."
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
ms.openlocfilehash: f88943ece7ee3d21dedbd857609f1b2713b62741
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="invoke-spark-programs-from-azure-data-factory-pipelines"></a><span data-ttu-id="59432-103">Wywoływanie programów Spark z potoków fabryki danych Azure</span><span class="sxs-lookup"><span data-stu-id="59432-103">Invoke Spark programs from Azure Data Factory pipelines</span></span>

> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="59432-104">Działanie gałęzi</span><span class="sxs-lookup"><span data-stu-id="59432-104">Hive Activity</span></span>](data-factory-hive-activity.md)
> * [<span data-ttu-id="59432-105">Działanie pig</span><span class="sxs-lookup"><span data-stu-id="59432-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="59432-106">Działania MapReduce</span><span class="sxs-lookup"><span data-stu-id="59432-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="59432-107">Działaniu przesyłania strumieniowego usługi Hadoop</span><span class="sxs-lookup"><span data-stu-id="59432-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="59432-108">Działanie Spark</span><span class="sxs-lookup"><span data-stu-id="59432-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="59432-109">Działanie wykonywania wsadowego w usłudze Machine Learning</span><span class="sxs-lookup"><span data-stu-id="59432-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="59432-110">Działania aktualizowania zasobów w usłudze Machine Learning</span><span class="sxs-lookup"><span data-stu-id="59432-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="59432-111">Działania procedur składowanych</span><span class="sxs-lookup"><span data-stu-id="59432-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="59432-112">Działania języka U-SQL usługi Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="59432-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="59432-113">Działania niestandardowe .NET</span><span class="sxs-lookup"><span data-stu-id="59432-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

## <a name="introduction"></a><span data-ttu-id="59432-114">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="59432-114">Introduction</span></span>
<span data-ttu-id="59432-115">Działanie Spark jest jednym z hello [działań przekształcania danych](data-factory-data-transformation-activities.md) obsługiwane przez usługi fabryka danych Azure.</span><span class="sxs-lookup"><span data-stu-id="59432-115">Spark Activity is one of hello [data transformation activities](data-factory-data-transformation-activities.md) supported by Azure Data Factory.</span></span> <span data-ttu-id="59432-116">To działanie jest uruchomione hello określony program Spark w klastrze Apache Spark w usłudze Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="59432-116">This activity runs hello specified Spark program on your Apache Spark cluster in Azure HDInsight.</span></span>    

> [!IMPORTANT]
> - <span data-ttu-id="59432-117">Działanie Spark nie obsługuje klastrów HDInsight Spark, które używają usługi Azure Data Lake Store jako podstawowy magazyn.</span><span class="sxs-lookup"><span data-stu-id="59432-117">Spark Activity does not support HDInsight Spark clusters that use an Azure Data Lake Store as primary storage.</span></span>
> - <span data-ttu-id="59432-118">Działanie Spark obsługuje tylko istniejące (własne) klastry HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="59432-118">Spark Activity supports only existing (your own) HDInsight Spark clusters.</span></span> <span data-ttu-id="59432-119">Nie obsługuje usługi HDInsight połączony na żądanie.</span><span class="sxs-lookup"><span data-stu-id="59432-119">It does not support an on-demand HDInsight linked service.</span></span>

## <a name="walkthrough-create-a-pipeline-with-spark-activity"></a><span data-ttu-id="59432-120">Wskazówki: tworzenie potoku z działaniem Spark</span><span class="sxs-lookup"><span data-stu-id="59432-120">Walkthrough: create a pipeline with Spark activity</span></span>
<span data-ttu-id="59432-121">Poniżej przedstawiono hello toocreate typowe etapy potoku fabryki danych z działaniem Spark.</span><span class="sxs-lookup"><span data-stu-id="59432-121">Here are hello typical steps toocreate a Data Factory pipeline with a Spark activity.</span></span>  

1. <span data-ttu-id="59432-122">Tworzenie fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="59432-122">Create a data factory.</span></span>
2. <span data-ttu-id="59432-123">Utwórz magazyn Azure skojarzony z fabryką danych toohello klastra Spark w usłudze HDInsight toolink usługi Azure Storage połączone.</span><span class="sxs-lookup"><span data-stu-id="59432-123">Create an Azure Storage linked service toolink your Azure storage that is associated with your HDInsight Spark cluster toohello data factory.</span></span>     
2. <span data-ttu-id="59432-124">Utwórz toolink usługi Azure HDInsight połączone klastra Apache Spark w fabryce danych Azure HDInsight toohello.</span><span class="sxs-lookup"><span data-stu-id="59432-124">Create an Azure HDInsight linked service toolink your Apache Spark cluster in Azure HDInsight toohello data factory.</span></span>
3. <span data-ttu-id="59432-125">Tworzenie zestawu danych, który odwołuje się toohello połączoną usługą magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="59432-125">Create a dataset that refers toohello Azure Storage linked service.</span></span> <span data-ttu-id="59432-126">Obecnie należy określić wyjściowy zestaw danych działania nawet jeśli dostępny jest nie wytworzonych.</span><span class="sxs-lookup"><span data-stu-id="59432-126">Currently, you must specify an output dataset for an activity even if there is no output being produced.</span></span>  
4. <span data-ttu-id="59432-127">Utworzyć potok z działaniem Spark, odnoszący się do usługi HDInsight połączone toohello utworzone w #2.</span><span class="sxs-lookup"><span data-stu-id="59432-127">Create a pipeline with Spark activity that refers toohello HDInsight linked service created in #2.</span></span> <span data-ttu-id="59432-128">Hello jest skonfigurowane z zestawem danych hello, utworzony w poprzednim kroku hello jako wyjściowego zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="59432-128">hello activity is configured with hello dataset you created in hello previous step as an output dataset.</span></span> <span data-ttu-id="59432-129">Witaj wyjściowy zestaw danych jest jakie dysków hello harmonogram (co godzinę, codziennie, itp.).</span><span class="sxs-lookup"><span data-stu-id="59432-129">hello output dataset is what drives hello schedule (hourly, daily, etc.).</span></span> <span data-ttu-id="59432-130">W związku z tym należy określić hello wyjściowy zestaw danych nawet, jeśli działanie hello nie tworzy naprawdę danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="59432-130">Therefore, you must specify hello output dataset even though hello activity does not really produce an output.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="59432-131">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="59432-131">Prerequisites</span></span>
1. <span data-ttu-id="59432-132">Utwórz **ogólnego przeznaczenia konta magazynu Azure** przez następujące instrukcje w przewodniku hello: [Utwórz konto magazynu](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span><span class="sxs-lookup"><span data-stu-id="59432-132">Create a **general-purpose Azure Storage Account** by following instructions in hello walkthrough: [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span></span>  
2. <span data-ttu-id="59432-133">Utwórz **klastra Apache Spark w usłudze Azure HDInsight** przez następujące instrukcje w samouczku hello: [klastra Utwórz Apache Spark w usłudze Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="59432-133">Create an **Apache Spark cluster in Azure HDInsight** by following instructions in hello tutorial: [Create Apache Spark cluster in Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md).</span></span> <span data-ttu-id="59432-134">Kojarzenie hello kontem magazynu platformy Azure, który został utworzony w kroku #1 z tym klastrem.</span><span class="sxs-lookup"><span data-stu-id="59432-134">Associate hello Azure storage account you created in step #1 with this cluster.</span></span>  
3. <span data-ttu-id="59432-135">Pobierz i przejrzyj plik skryptu języka python hello **test.py** w lokalizacji: [https://adftutorialfiles.blob.core.windows.net/sparktutorial/test.py](https://adftutorialfiles.blob.core.windows.net/sparktutorial/test.py).</span><span class="sxs-lookup"><span data-stu-id="59432-135">Download and review hello python script file **test.py** located at: [https://adftutorialfiles.blob.core.windows.net/sparktutorial/test.py](https://adftutorialfiles.blob.core.windows.net/sparktutorial/test.py).</span></span>  
3.  <span data-ttu-id="59432-136">Przekaż **test.py** toohello **pyFiles** folderu w hello **adfspark** kontenera w magazynie obiektów Blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="59432-136">Upload **test.py** toohello **pyFiles** folder in hello **adfspark** container in your Azure Blob storage.</span></span> <span data-ttu-id="59432-137">Utwórz hello kontenera i folderu hello, jeśli nie istnieją.</span><span class="sxs-lookup"><span data-stu-id="59432-137">Create hello container and hello folder if they do not exist.</span></span>

### <a name="create-data-factory"></a><span data-ttu-id="59432-138">Tworzenie fabryki danych</span><span class="sxs-lookup"><span data-stu-id="59432-138">Create data factory</span></span>
<span data-ttu-id="59432-139">Zacznijmy od utworzenia hello fabryki danych w tym kroku.</span><span class="sxs-lookup"><span data-stu-id="59432-139">Let's start with creating hello data factory in this step.</span></span>

1. <span data-ttu-id="59432-140">Zaloguj się za toohello [portalu Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="59432-140">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="59432-141">Kliknij przycisk **nowy** w menu po lewej stronie powitania kliknij **dane i analiza**i kliknij przycisk **fabryki danych**.</span><span class="sxs-lookup"><span data-stu-id="59432-141">Click **NEW** on hello left menu, click **Data + Analytics**, and click **Data Factory**.</span></span>
3. <span data-ttu-id="59432-142">W hello **nowa fabryka danych** bloku, wprowadź **SparkDF** dla hello nazwy.</span><span class="sxs-lookup"><span data-stu-id="59432-142">In hello **New data factory** blade, enter **SparkDF** for hello Name.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="59432-143">Nazwa fabryki danych Azure hello Hello musi być **unikatowych**.</span><span class="sxs-lookup"><span data-stu-id="59432-143">hello name of hello Azure data factory must be **globally unique**.</span></span> <span data-ttu-id="59432-144">Jeśli zostanie wyświetlony błąd hello: **nazwa fabryki danych "SparkDF" nie jest dostępny**.</span><span class="sxs-lookup"><span data-stu-id="59432-144">If you see hello error: **Data factory name “SparkDF” is not available**.</span></span> <span data-ttu-id="59432-145">Zmień nazwę hello fabryki danych hello (na przykład yournameSparkDFdate i spróbuj ponownie utworzyć.</span><span class="sxs-lookup"><span data-stu-id="59432-145">Change hello name of hello data factory (for example, yournameSparkDFdate, and try creating again.</span></span> <span data-ttu-id="59432-146">Artykuł [Data Factory — Naming Rules](data-factory-naming-rules.md) (Fabryka danych — zasady nazewnictwa) zawiera zasady nazewnictwa artefaktów usługi Fabryka danych.</span><span class="sxs-lookup"><span data-stu-id="59432-146">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>   
4. <span data-ttu-id="59432-147">Wybierz hello **subskrypcji platformy Azure** miejscu toobe fabryki danych hello utworzony.</span><span class="sxs-lookup"><span data-stu-id="59432-147">Select hello **Azure subscription** where you want hello data factory toobe created.</span></span>
5. <span data-ttu-id="59432-148">Wybierz istniejący **grupy zasobów** lub Utwórz grupę zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="59432-148">Select an existing **resource group** or create an Azure resource group.</span></span>
6. <span data-ttu-id="59432-149">Wybierz **toodashboard numeru Pin** opcji.</span><span class="sxs-lookup"><span data-stu-id="59432-149">Select **Pin toodashboard** option.</span></span>  
6. <span data-ttu-id="59432-150">Kliknij przycisk **Utwórz** na powitania **nowa fabryka danych** bloku.</span><span class="sxs-lookup"><span data-stu-id="59432-150">Click **Create** on hello **New data factory** blade.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="59432-151">toocreate wystąpienia fabryki danych, musi być członkiem hello [współautora fabryki danych](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) roli na poziomie grupy zasobów subskrypcji hello.</span><span class="sxs-lookup"><span data-stu-id="59432-151">toocreate Data Factory instances, you must be a member of hello [Data Factory Contributor](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) role at hello subscription/resource group level.</span></span>
7. <span data-ttu-id="59432-152">Zobacz hello fabryki danych tworzona w hello **pulpitu nawigacyjnego** z hello portalu Azure w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="59432-152">You see hello data factory being created in hello **dashboard** of hello Azure portal as follows:</span></span>   
8. <span data-ttu-id="59432-153">Po hello fabryki danych został utworzony pomyślnie, zobacz strony fabryki danych hello, który umożliwia hello zawartość hello fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="59432-153">After hello data factory has been created successfully, you see hello data factory page, which shows you hello contents of hello data factory.</span></span> <span data-ttu-id="59432-154">Jeśli nie ma strony fabryki danych hello, kliknij Kafelek hello fabrykę danych na pulpicie nawigacyjnym hello.</span><span class="sxs-lookup"><span data-stu-id="59432-154">If you do not see hello data factory page, click hello tile for your data factory on hello dashboard.</span></span>

    ![Blok Fabryka danych](./media/data-factory-spark/data-factory-blade.png)

### <a name="create-linked-services"></a><span data-ttu-id="59432-156">Tworzenie połączonych usług</span><span class="sxs-lookup"><span data-stu-id="59432-156">Create linked services</span></span>
<span data-ttu-id="59432-157">W tym kroku utwórz dwa połączone usługi, co toolink fabrykę danych tooyour klastra Spark, a hello innych toolink fabrykę danych tooyour magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="59432-157">In this step, you create two linked services, one toolink your Spark cluster tooyour data factory, and hello other toolink your Azure storage tooyour data factory.</span></span>  

#### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="59432-158">Tworzenie połączonej usługi Azure Storage</span><span class="sxs-lookup"><span data-stu-id="59432-158">Create Azure Storage linked service</span></span>
<span data-ttu-id="59432-159">W tym kroku możesz połączyć fabrykę danych tooyour konta magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="59432-159">In this step, you link your Azure Storage account tooyour data factory.</span></span> <span data-ttu-id="59432-160">Zestaw danych utworzone w kroku później w tym przewodniku odnosi się toothis połączone usługi.</span><span class="sxs-lookup"><span data-stu-id="59432-160">A dataset you create in a step later in this walkthrough refers toothis linked service.</span></span> <span data-ttu-id="59432-161">Hello usługi HDInsight połączone, zdefiniowanego w następnym kroku hello zbyt odwołuje się toothis połączone usługi.</span><span class="sxs-lookup"><span data-stu-id="59432-161">hello HDInsight linked service that you define in hello next step refers toothis linked service too.</span></span>  

1. <span data-ttu-id="59432-162">Kliknij przycisk **tworzenie i wdrażanie** na powitania **fabryki danych** bloku fabryką danych.</span><span class="sxs-lookup"><span data-stu-id="59432-162">Click **Author and deploy** on hello **Data Factory** blade for your data factory.</span></span> <span data-ttu-id="59432-163">Powinny pojawić się hello Edytor fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="59432-163">You should see hello Data Factory Editor.</span></span>
2. <span data-ttu-id="59432-164">Kliknij przycisk **Nowy magazyn danych** i wybierz opcję **Azure Storage**.</span><span class="sxs-lookup"><span data-stu-id="59432-164">Click **New data store** and choose **Azure storage**.</span></span>

   ![Nowy magazyn danych — Azure Storage — menu](./media/data-factory-spark/new-data-store-azure-storage-menu.png)
3. <span data-ttu-id="59432-166">Powinny pojawić się hello **skryptu JSON** do tworzenia usługi Azure Storage połączonej usługi w edytorze hello.</span><span class="sxs-lookup"><span data-stu-id="59432-166">You should see hello **JSON script** for creating an Azure Storage linked service in hello editor.</span></span>

   ![Połączona usługa Azure Storage](./media/data-factory-build-your-first-pipeline-using-editor/azure-storage-linked-service.png)
4. <span data-ttu-id="59432-168">Zastąp **nazwa konta** i **klucz konta** z hello nazwy i klucza dostępu konta magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="59432-168">Replace **account name** and **account key** with hello name and access key of your Azure storage account.</span></span> <span data-ttu-id="59432-169">toolearn sposób dostępu do magazynu tooget klucza, zobacz hello informacji na temat sposobu tooview, kopiowania i regenerate magazynu dostępu do kluczy w [Zarządzanie kontem magazynu](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="59432-169">toolearn how tooget your storage access key, see hello information about how tooview, copy, and regenerate storage access keys in [Manage your storage account](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>
5. <span data-ttu-id="59432-170">toodeploy hello połączonej usługi, kliknij przycisk **Wdróż** na powitania paska poleceń.</span><span class="sxs-lookup"><span data-stu-id="59432-170">toodeploy hello linked service, click **Deploy** on hello command bar.</span></span> <span data-ttu-id="59432-171">Witaj po hello połączonej usługi został wdrożony pomyślnie, **projekt 1** powinien zniknąć okna, aby zobaczyć **AzureStorageLinkedService** w widoku drzewa hello powitania po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="59432-171">After hello linked service is deployed successfully, hello **Draft-1** window should disappear and you see **AzureStorageLinkedService** in hello tree view on hello left.</span></span>

#### <a name="create-hdinsight-linked-service"></a><span data-ttu-id="59432-172">Tworzenie usługi HDInsight połączone</span><span class="sxs-lookup"><span data-stu-id="59432-172">Create HDInsight linked service</span></span>
<span data-ttu-id="59432-173">W tym kroku utworzysz toolink usługi Azure HDInsight połączone fabrykę danych toohello klastra Spark w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="59432-173">In this step, you create Azure HDInsight linked service toolink your HDInsight Spark cluster toohello data factory.</span></span> <span data-ttu-id="59432-174">klaster usługi HDInsight Hello jest programu Spark hello używane toorun określony w działaniu Spark hello hello potoku, w tym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="59432-174">hello HDInsight cluster is used toorun hello Spark program specified in hello Spark activity of hello pipeline in this sample.</span></span>  

1. <span data-ttu-id="59432-175">Kliknij przycisk **... Więcej** na powitania narzędzi, kliknij przycisk **nowych obliczeń**, a następnie kliknij przycisk **klastra usługi HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="59432-175">Click **... More** on hello toolbar, click **New compute**, and then click **HDInsight cluster**.</span></span>

    ![Tworzenie usługi HDInsight połączone](media/data-factory-spark/new-hdinsight-linked-service.png)
2. <span data-ttu-id="59432-177">Skopiuj i Wklej powitania po toohello fragment **projekt 1** okna.</span><span class="sxs-lookup"><span data-stu-id="59432-177">Copy and paste hello following snippet toohello **Draft-1** window.</span></span> <span data-ttu-id="59432-178">W edytorze JSON hello hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="59432-178">In hello JSON editor, do hello following steps:</span></span>
    1. <span data-ttu-id="59432-179">Określ hello **URI** hello Spark w usłudze HDInsight klastra.</span><span class="sxs-lookup"><span data-stu-id="59432-179">Specify hello **URI** for hello HDInsight Spark cluster.</span></span> <span data-ttu-id="59432-180">Na przykład: `https://<sparkclustername>.azurehdinsight.net/`.</span><span class="sxs-lookup"><span data-stu-id="59432-180">For example: `https://<sparkclustername>.azurehdinsight.net/`.</span></span>
    2. <span data-ttu-id="59432-181">Określ nazwę hello hello **użytkownika** kto ma dostęp toohello Spark klastra.</span><span class="sxs-lookup"><span data-stu-id="59432-181">Specify hello name of hello **user** who has access toohello Spark cluster.</span></span>
    3. <span data-ttu-id="59432-182">Określ hello **hasło** dla użytkownika.</span><span class="sxs-lookup"><span data-stu-id="59432-182">Specify hello **password** for user.</span></span>
    4. <span data-ttu-id="59432-183">Określ hello **połączonej usługi magazynu Azure** skojarzonego z hello klastra Spark w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="59432-183">Specify hello **Azure Storage linked service** that is associated with hello HDInsight Spark cluster.</span></span> <span data-ttu-id="59432-184">W tym przykładzie jest: **AzureStorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="59432-184">In this example, it is: **AzureStorageLinkedService**.</span></span>

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
    > - <span data-ttu-id="59432-185">Działanie Spark nie obsługuje klastrów HDInsight Spark, które używają usługi Azure Data Lake Store jako podstawowy magazyn.</span><span class="sxs-lookup"><span data-stu-id="59432-185">Spark Activity does not support HDInsight Spark clusters that use an Azure Data Lake Store as primary storage.</span></span>
    > - <span data-ttu-id="59432-186">Działanie Spark obsługuje tylko istniejące (własne) klastra Spark w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="59432-186">Spark Activity supports only existing (your own) HDInsight Spark cluster.</span></span> <span data-ttu-id="59432-187">Nie obsługuje usługi HDInsight połączony na żądanie.</span><span class="sxs-lookup"><span data-stu-id="59432-187">It does not support an on-demand HDInsight linked service.</span></span>

    <span data-ttu-id="59432-188">Zobacz [połączoną usługą usługi HDInsight](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) szczegółowe informacje o hello HDInsight połączonej usługi.</span><span class="sxs-lookup"><span data-stu-id="59432-188">See [HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) for details about hello HDInsight linked service.</span></span>
3.  <span data-ttu-id="59432-189">toodeploy hello połączonej usługi, kliknij przycisk **Wdróż** na powitania paska poleceń.</span><span class="sxs-lookup"><span data-stu-id="59432-189">toodeploy hello linked service, click **Deploy** on hello command bar.</span></span>  

### <a name="create-output-dataset"></a><span data-ttu-id="59432-190">Tworzenie wyjściowego zestawu danych</span><span class="sxs-lookup"><span data-stu-id="59432-190">Create output dataset</span></span>
<span data-ttu-id="59432-191">Witaj wyjściowy zestaw danych jest jakie dysków hello harmonogram (co godzinę, codziennie, itp.).</span><span class="sxs-lookup"><span data-stu-id="59432-191">hello output dataset is what drives hello schedule (hourly, daily, etc.).</span></span> <span data-ttu-id="59432-192">W związku z tym należy określić wyjściowy zestaw danych dla hello spark działania w potoku hello mimo, że działanie hello nie tworzy naprawdę żadnych danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="59432-192">Therefore, you must specify an output dataset for hello spark activity in hello pipeline even though hello activity does not really produce any output.</span></span> <span data-ttu-id="59432-193">Określenie zestawem danych wejściowych dla działania hello jest opcjonalne.</span><span class="sxs-lookup"><span data-stu-id="59432-193">Specifying an input dataset for hello activity is optional.</span></span>

1. <span data-ttu-id="59432-194">W hello **Edytor fabryki danych**, kliknij przycisk **... Więcej** na pasku poleceń powitania kliknij **nowy zestaw danych**i wybierz **magazynu obiektów Blob Azure**.</span><span class="sxs-lookup"><span data-stu-id="59432-194">In hello **Data Factory Editor**, click **... More** on hello command bar, click **New dataset**, and select **Azure Blob storage**.</span></span>  
2. <span data-ttu-id="59432-195">Skopiuj i Wklej powitania po fragment okna toohello projekt-1.</span><span class="sxs-lookup"><span data-stu-id="59432-195">Copy and paste hello following snippet toohello Draft-1 window.</span></span> <span data-ttu-id="59432-196">fragment kodu JSON Hello definiuje zestaw danych o nazwie **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="59432-196">hello JSON snippet defines a dataset called **OutputDataset**.</span></span> <span data-ttu-id="59432-197">Ponadto należy określić czy hello wyniki są przechowywane w kontenerze obiektów blob hello o nazwie **adfspark** i hello folder o nazwie **pyFiles/wyjścia**.</span><span class="sxs-lookup"><span data-stu-id="59432-197">In addition, you specify that hello results are stored in hello blob container called **adfspark** and hello folder called **pyFiles/output**.</span></span> <span data-ttu-id="59432-198">Jak wspomniano wcześniej, ten zestaw danych jest fikcyjny zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="59432-198">As mentioned earlier, this dataset is a dummy dataset.</span></span> <span data-ttu-id="59432-199">program Spark Hello w tym przykładzie nie generuje żadnego wyniku.</span><span class="sxs-lookup"><span data-stu-id="59432-199">hello Spark program in this example does not produce any output.</span></span> <span data-ttu-id="59432-200">Witaj **dostępności** sekcja określa, że wyjściowy zestaw danych hello jest tworzony codziennie.</span><span class="sxs-lookup"><span data-stu-id="59432-200">hello **availability** section specifies that hello output dataset is produced daily.</span></span>  

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
3. <span data-ttu-id="59432-201">toodeploy hello zestawu danych, kliknij przycisk **Wdróż** na powitania paska poleceń.</span><span class="sxs-lookup"><span data-stu-id="59432-201">toodeploy hello dataset, click **Deploy** on hello command bar.</span></span>


### <a name="create-pipeline"></a><span data-ttu-id="59432-202">Tworzenie potoku</span><span class="sxs-lookup"><span data-stu-id="59432-202">Create pipeline</span></span>
<span data-ttu-id="59432-203">W tym kroku możesz utworzyć potok wraz z **HDInsightSpark** działania.</span><span class="sxs-lookup"><span data-stu-id="59432-203">In this step, you create a pipeline with a **HDInsightSpark** activity.</span></span> <span data-ttu-id="59432-204">Wyjściowy zestaw danych jest obecnie, jakie dysków hello harmonogramu, dlatego należy utworzyć wyjściowy zestaw danych, nawet wtedy, gdy działanie hello nie generuje żadnego wyniku.</span><span class="sxs-lookup"><span data-stu-id="59432-204">Currently, output dataset is what drives hello schedule, so you must create an output dataset even if hello activity does not produce any output.</span></span> <span data-ttu-id="59432-205">Jeśli działanie hello nie przyjmuje żadnych danych, możesz pominąć tworzenie zestawu danych wejściowych hello.</span><span class="sxs-lookup"><span data-stu-id="59432-205">If hello activity doesn't take any input, you can skip creating hello input dataset.</span></span> <span data-ttu-id="59432-206">W związku z tym nie wejściowy zestaw danych został określony w tym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="59432-206">Therefore, no input dataset is specified in this example.</span></span>

1. <span data-ttu-id="59432-207">W hello **Edytor fabryki danych**, kliknij przycisk **... Więcej** na hello pasek poleceń, a następnie kliknij przycisk **nowy potok**.</span><span class="sxs-lookup"><span data-stu-id="59432-207">In hello **Data Factory Editor**, click **… More** on hello command bar, and then click **New pipeline**.</span></span>
2. <span data-ttu-id="59432-208">Zastąp hello skryptu w oknie hello projekt 1 hello następującego skryptu:</span><span class="sxs-lookup"><span data-stu-id="59432-208">Replace hello script in hello Draft-1 window with hello following script:</span></span>

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
    <span data-ttu-id="59432-209">Należy zwrócić uwagę hello następujące punkty:</span><span class="sxs-lookup"><span data-stu-id="59432-209">Note hello following points:</span></span>
    - <span data-ttu-id="59432-210">Witaj **typu** właściwość jest ustawiona zbyt**HDInsightSpark**.</span><span class="sxs-lookup"><span data-stu-id="59432-210">hello **type** property is set too**HDInsightSpark**.</span></span>
    - <span data-ttu-id="59432-211">Witaj **właściwość rootPath** ustawiono zbyt**adfspark\\pyFiles** gdzie adfspark jest pyFiles i kontener obiektów Blob Azure hello jest poprawnie folderu, w tym kontenerze.</span><span class="sxs-lookup"><span data-stu-id="59432-211">hello **rootPath** is set too**adfspark\\pyFiles** where adfspark is hello Azure Blob container and pyFiles is fine folder in that container.</span></span> <span data-ttu-id="59432-212">W tym przykładzie hello magazynu obiektów Blob Azure jest hello, który jest skojarzony z klastrem Spark hello.</span><span class="sxs-lookup"><span data-stu-id="59432-212">In this example, hello Azure Blob Storage is hello one that is associated with hello Spark cluster.</span></span> <span data-ttu-id="59432-213">Możesz przekazać tooa pliku hello innego magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="59432-213">You can upload hello file tooa different Azure Storage.</span></span> <span data-ttu-id="59432-214">Jeśli tak zrobisz, należy utworzyć toolink usługi Azure Storage połączone tej fabryki danych toohello konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="59432-214">If you do so, create an Azure Storage linked service toolink that storage account toohello data factory.</span></span> <span data-ttu-id="59432-215">Następnie określ nazwę hello hello połączone usługi jako wartość hello **sparkJobLinkedService** właściwości.</span><span class="sxs-lookup"><span data-stu-id="59432-215">Then, specify hello name of hello linked service as a value for hello **sparkJobLinkedService** property.</span></span> <span data-ttu-id="59432-216">Zobacz [właściwości działania Spark](#spark-activity-properties) szczegóły dotyczące tej właściwości oraz inne właściwości obsługiwanych przez hello działania Spark.</span><span class="sxs-lookup"><span data-stu-id="59432-216">See [Spark Activity properties](#spark-activity-properties) for details about this property and other properties supported by hello Spark Activity.</span></span>  
    - <span data-ttu-id="59432-217">Witaj **entryFilePath** ustawiono toohello **test.py**, czyli plik python hello.</span><span class="sxs-lookup"><span data-stu-id="59432-217">hello **entryFilePath** is set toohello **test.py**, which is hello python file.</span></span>
    - <span data-ttu-id="59432-218">Witaj **getDebugInfo** właściwość jest ustawiona zbyt**zawsze**, co oznacza, że pliki dziennika hello są zawsze generowany (powodzenie lub niepowodzenie).</span><span class="sxs-lookup"><span data-stu-id="59432-218">hello **getDebugInfo** property is set too**Always**, which means hello log files are always generated (success or failure).</span></span>

        > [!IMPORTANT]
        > <span data-ttu-id="59432-219">Firma Microsoft zaleca, aby nie ustawisz tę właściwość za`Always` w środowisku produkcyjnym, chyba że są Rozwiązywanie problemów.</span><span class="sxs-lookup"><span data-stu-id="59432-219">We recommend that you do not set this property too`Always` in a production environment unless you are troubleshooting an issue.</span></span>
    - <span data-ttu-id="59432-220">Witaj **generuje** sekcja ma jeden wyjściowy zestaw danych.</span><span class="sxs-lookup"><span data-stu-id="59432-220">hello **outputs** section has one output dataset.</span></span> <span data-ttu-id="59432-221">Należy określić wyjściowy zestaw danych, nawet jeśli hello spark program nie zwraca żadnych danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="59432-221">You must specify an output dataset even if hello spark program does not produce any output.</span></span> <span data-ttu-id="59432-222">Hello wyjściowego zestawu danych dysków hello harmonogram dla potoku hello (co godzinę, codziennie, itp.).</span><span class="sxs-lookup"><span data-stu-id="59432-222">hello output dataset drives hello schedule for hello pipeline (hourly, daily, etc.).</span></span>  

        <span data-ttu-id="59432-223">Aby uzyskać szczegółowe informacje o obsługiwanych przez działanie Spark właściwości hello, zobacz [Spark właściwości działania](#spark-activity-properties) sekcji.</span><span class="sxs-lookup"><span data-stu-id="59432-223">For details about hello properties supported by Spark activity, see [Spark activity properties](#spark-activity-properties) section.</span></span>
3. <span data-ttu-id="59432-224">toodeploy hello potoku, kliknij przycisk **Wdróż** na powitania paska poleceń.</span><span class="sxs-lookup"><span data-stu-id="59432-224">toodeploy hello pipeline, click **Deploy** on hello command bar.</span></span>

### <a name="monitor-pipeline"></a><span data-ttu-id="59432-225">Monitorowanie potoku</span><span class="sxs-lookup"><span data-stu-id="59432-225">Monitor pipeline</span></span>
1. <span data-ttu-id="59432-226">Kliknij przycisk **X** tooclose bloków Edytor fabryki danych i toonavigate ponownie strony głównej toohello fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="59432-226">Click **X** tooclose Data Factory Editor blades and toonavigate back toohello Data Factory home page.</span></span> <span data-ttu-id="59432-227">Kliknij przycisk **monitorowanie i zarządzanie** hello toolaunch monitorowania aplikacji w innej karty.</span><span class="sxs-lookup"><span data-stu-id="59432-227">Click **Monitor and Manage** toolaunch hello monitoring application in another tab.</span></span>

    ![Monitorowanie i zarządzanie nimi kafelka](media/data-factory-spark/monitor-and-manage-tile.png)
2. <span data-ttu-id="59432-229">Zmień hello **godzina rozpoczęcia** filtru u góry hello zbyt**2/1/2017**i kliknij przycisk **Zastosuj**.</span><span class="sxs-lookup"><span data-stu-id="59432-229">Change hello **Start time** filter at hello top too**2/1/2017**, and click **Apply**.</span></span>
3. <span data-ttu-id="59432-230">Tylko jedno okno działania powinna zostać wyświetlona z powodu godziny (2017-02-02) potoku hello między hello tylko jeden dzień rozpoczęcia (2017-02-01) i zakończenia.</span><span class="sxs-lookup"><span data-stu-id="59432-230">You should see only one activity window as there is only one day between hello start (2017-02-01) and end times (2017-02-02) of hello pipeline.</span></span> <span data-ttu-id="59432-231">Upewnij się, że hello wycinka danych jest w **gotowe** stanu.</span><span class="sxs-lookup"><span data-stu-id="59432-231">Confirm that hello data slice is in **ready** state.</span></span>

    ![Monitor hello potoku](media/data-factory-spark/monitor-and-manage-app.png)    
4. <span data-ttu-id="59432-233">Wybierz hello **okno działania** toosee szczegóły dotyczące uruchamiania działania hello.</span><span class="sxs-lookup"><span data-stu-id="59432-233">Select hello **activity window** toosee details about hello activity run.</span></span> <span data-ttu-id="59432-234">Jeśli występuje błąd, zobaczysz szczegółowe informacje o nim w okienku po prawej stronie powitania.</span><span class="sxs-lookup"><span data-stu-id="59432-234">If there is an error, you see details about it in hello right pane.</span></span>

### <a name="verify-hello-results"></a><span data-ttu-id="59432-235">Sprawdź wyniki hello</span><span class="sxs-lookup"><span data-stu-id="59432-235">Verify hello results</span></span>

1. <span data-ttu-id="59432-236">Uruchom **notesu Jupyter** przechodząc do klastra Spark w usłudze HDInsight: https://CLUSTERNAME.azurehdinsight.net/jupyter.</span><span class="sxs-lookup"><span data-stu-id="59432-236">Launch **Jupyter notebook** for your HDInsight Spark cluster by navigating to: https://CLUSTERNAME.azurehdinsight.net/jupyter.</span></span> <span data-ttu-id="59432-237">Można również uruchomić Pulpit nawigacyjny klastra dla klastra Spark w usłudze HDInsight, a następnie uruchom **notesu Jupyter**.</span><span class="sxs-lookup"><span data-stu-id="59432-237">You can also launch cluster dashboard for your HDInsight Spark cluster, and then launch **Jupyter Notebook**.</span></span>
2. <span data-ttu-id="59432-238">Kliknij przycisk **nowy** -> **PySpark** toostart nowy notes.</span><span class="sxs-lookup"><span data-stu-id="59432-238">Click **New** -> **PySpark** toostart a new notebook.</span></span>

    ![Nowego notesu Jupyter](media/data-factory-spark/jupyter-new-book.png)
3. <span data-ttu-id="59432-240">Uruchom hello następujące polecenia kopiowania/wklejania hello tekstu i naciskając klawisz **SHIFT + ENTER** na końcu hello hello drugiej instrukcji.</span><span class="sxs-lookup"><span data-stu-id="59432-240">Run hello following command by copy/pasting hello text and pressing **SHIFT + ENTER** at hello end of hello second statement.</span></span>  

    ```sql
    %%sql

    SELECT buildingID, (targettemp - actualtemp) AS temp_diff, date FROM hvac WHERE date = \"6/1/13\"
    ```
4. <span data-ttu-id="59432-241">Upewnij się, że widoczny hello danych z tabeli hvac hello:</span><span class="sxs-lookup"><span data-stu-id="59432-241">Confirm that you see hello data from hello hvac table:</span></span>  

    ![Wyniki zapytania Jupyter](media/data-factory-spark/jupyter-notebook-results.png)

<span data-ttu-id="59432-243">Zobacz [uruchamiania zapytań Spark SQL](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md#run-a-hive-query-using-spark-sql) sekcji, aby uzyskać szczegółowe instrukcje.</span><span class="sxs-lookup"><span data-stu-id="59432-243">See [Run a Spark SQL query](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md#run-a-hive-query-using-spark-sql) section for detailed instructions.</span></span> 

### <a name="troubleshooting"></a><span data-ttu-id="59432-244">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="59432-244">Troubleshooting</span></span>
<span data-ttu-id="59432-245">Ponieważ ustawisz **getDebugInfo** za**zawsze**, zostanie wyświetlony **dziennika** podfolder hello **pyFiles** folderu w kontenerze obiektu Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="59432-245">Since you set **getDebugInfo** too**Always**, you see a **log** subfolder in hello **pyFiles** folder in your Azure Blob container.</span></span> <span data-ttu-id="59432-246">Witaj pliku dziennika w folderze dziennika hello zawiera dodatkowe szczegóły.</span><span class="sxs-lookup"><span data-stu-id="59432-246">hello log file in hello log folder provides additional details.</span></span> <span data-ttu-id="59432-247">Ten plik dziennika jest szczególnie przydatna w przypadku, gdy występuje błąd.</span><span class="sxs-lookup"><span data-stu-id="59432-247">This log file is especially useful when there is an error.</span></span> <span data-ttu-id="59432-248">W środowisku produkcyjnym można tooset on zbyt**błąd**.</span><span class="sxs-lookup"><span data-stu-id="59432-248">In a production environment, you may want tooset it too**Failure**.</span></span>

<span data-ttu-id="59432-249">Aby uzyskać dodatkowe informacje o rozwiązywaniu, hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="59432-249">For further troubleshooting, do hello following steps:</span></span>


1. <span data-ttu-id="59432-250">Przejdź do zbyt`https://<CLUSTERNAME>.azurehdinsight.net/yarnui/hn/cluster`.</span><span class="sxs-lookup"><span data-stu-id="59432-250">Navigate too`https://<CLUSTERNAME>.azurehdinsight.net/yarnui/hn/cluster`.</span></span>

    ![Aplikacja YARN interfejsu użytkownika](media/data-factory-spark/yarnui-application.png)  
2. <span data-ttu-id="59432-252">Kliknij przycisk **dzienniki** jednego hello Uruchom prób.</span><span class="sxs-lookup"><span data-stu-id="59432-252">Click **Logs** for one of hello run attempts.</span></span>

    ![Strona aplikacji](media/data-factory-spark/yarn-applications.png)
3. <span data-ttu-id="59432-254">Dodatkowe informacje o błędzie na stronie dziennika hello powinna zostać wyświetlona.</span><span class="sxs-lookup"><span data-stu-id="59432-254">You should see additional error information in hello log page.</span></span>

    ![Błąd dziennika](media/data-factory-spark/yarnui-application-error.png)

<span data-ttu-id="59432-256">Witaj następujące sekcje zawierają informacje dotyczące klastra Apache Spark toouse jednostek fabryki danych i działania Spark w fabryce danych.</span><span class="sxs-lookup"><span data-stu-id="59432-256">hello following sections provide information about Data Factory entities toouse Apache Spark cluster and Spark Activity in your data factory.</span></span>

## <a name="spark-activity-properties"></a><span data-ttu-id="59432-257">Właściwości działania Spark</span><span class="sxs-lookup"><span data-stu-id="59432-257">Spark activity properties</span></span>
<span data-ttu-id="59432-258">Oto definicji JSON próbki hello potoku z działaniem Spark:</span><span class="sxs-lookup"><span data-stu-id="59432-258">Here is hello sample JSON definition of a pipeline with Spark Activity:</span></span>    

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
                "description": "This activity invokes hello Spark program",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2017-02-01T00:00:00Z",
        "end": "2017-02-02T00:00:00Z"
    }
}
```

<span data-ttu-id="59432-259">Witaj poniższej tabeli opisano właściwości JSON hello używane w definicji JSON hello:</span><span class="sxs-lookup"><span data-stu-id="59432-259">hello following table describes hello JSON properties used in hello JSON definition:</span></span>

| <span data-ttu-id="59432-260">Właściwość</span><span class="sxs-lookup"><span data-stu-id="59432-260">Property</span></span> | <span data-ttu-id="59432-261">Opis</span><span class="sxs-lookup"><span data-stu-id="59432-261">Description</span></span> | <span data-ttu-id="59432-262">Wymagane</span><span class="sxs-lookup"><span data-stu-id="59432-262">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="59432-263">name</span><span class="sxs-lookup"><span data-stu-id="59432-263">name</span></span> | <span data-ttu-id="59432-264">Nazwa działania hello w potoku hello.</span><span class="sxs-lookup"><span data-stu-id="59432-264">Name of hello activity in hello pipeline.</span></span> | <span data-ttu-id="59432-265">Tak</span><span class="sxs-lookup"><span data-stu-id="59432-265">Yes</span></span> |
| <span data-ttu-id="59432-266">description</span><span class="sxs-lookup"><span data-stu-id="59432-266">description</span></span> | <span data-ttu-id="59432-267">Tekst opisujący jakie działanie hello jest.</span><span class="sxs-lookup"><span data-stu-id="59432-267">Text describing what hello activity does.</span></span> | <span data-ttu-id="59432-268">Nie</span><span class="sxs-lookup"><span data-stu-id="59432-268">No</span></span> |
| <span data-ttu-id="59432-269">type</span><span class="sxs-lookup"><span data-stu-id="59432-269">type</span></span> | <span data-ttu-id="59432-270">Tej właściwości należy ustawić tooHDInsightSpark.</span><span class="sxs-lookup"><span data-stu-id="59432-270">This property must be set tooHDInsightSpark.</span></span> | <span data-ttu-id="59432-271">Tak</span><span class="sxs-lookup"><span data-stu-id="59432-271">Yes</span></span> |
| <span data-ttu-id="59432-272">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="59432-272">linkedServiceName</span></span> | <span data-ttu-id="59432-273">Nazwa hello HDInsight połączonej usługi, na których hello Spark program będzie uruchamiany.</span><span class="sxs-lookup"><span data-stu-id="59432-273">Name of hello HDInsight linked service on which hello Spark program runs.</span></span> | <span data-ttu-id="59432-274">Tak</span><span class="sxs-lookup"><span data-stu-id="59432-274">Yes</span></span> |
| <span data-ttu-id="59432-275">Właściwość rootPath</span><span class="sxs-lookup"><span data-stu-id="59432-275">rootPath</span></span> | <span data-ttu-id="59432-276">Witaj kontenera obiektów Blob platformy Azure i folder zawierający plik Spark hello.</span><span class="sxs-lookup"><span data-stu-id="59432-276">hello Azure Blob container and folder that contains hello Spark file.</span></span> <span data-ttu-id="59432-277">Nazwa pliku Hello jest rozróżniana wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="59432-277">hello file name is case-sensitive.</span></span> | <span data-ttu-id="59432-278">Tak</span><span class="sxs-lookup"><span data-stu-id="59432-278">Yes</span></span> |
| <span data-ttu-id="59432-279">entryFilePath</span><span class="sxs-lookup"><span data-stu-id="59432-279">entryFilePath</span></span> | <span data-ttu-id="59432-280">Względna ścieżka folderu głównego toohello hello pakietu kodu Spark.</span><span class="sxs-lookup"><span data-stu-id="59432-280">Relative path toohello root folder of hello Spark code/package.</span></span> | <span data-ttu-id="59432-281">Tak</span><span class="sxs-lookup"><span data-stu-id="59432-281">Yes</span></span> |
| <span data-ttu-id="59432-282">className</span><span class="sxs-lookup"><span data-stu-id="59432-282">className</span></span> | <span data-ttu-id="59432-283">Klasy głównym aplikacji Java/Spark</span><span class="sxs-lookup"><span data-stu-id="59432-283">Application's Java/Spark main class</span></span> | <span data-ttu-id="59432-284">Nie</span><span class="sxs-lookup"><span data-stu-id="59432-284">No</span></span> |
| <span data-ttu-id="59432-285">Argumenty</span><span class="sxs-lookup"><span data-stu-id="59432-285">arguments</span></span> | <span data-ttu-id="59432-286">Lista argumentów wiersza polecenia toohello Spark program.</span><span class="sxs-lookup"><span data-stu-id="59432-286">A list of command-line arguments toohello Spark program.</span></span> | <span data-ttu-id="59432-287">Nie</span><span class="sxs-lookup"><span data-stu-id="59432-287">No</span></span> |
| <span data-ttu-id="59432-288">proxyUser</span><span class="sxs-lookup"><span data-stu-id="59432-288">proxyUser</span></span> | <span data-ttu-id="59432-289">program Spark hello tooexecute tooimpersonate Hello użytkownika konta</span><span class="sxs-lookup"><span data-stu-id="59432-289">hello user account tooimpersonate tooexecute hello Spark program</span></span> | <span data-ttu-id="59432-290">Nie</span><span class="sxs-lookup"><span data-stu-id="59432-290">No</span></span> |
| <span data-ttu-id="59432-291">sparkConfig</span><span class="sxs-lookup"><span data-stu-id="59432-291">sparkConfig</span></span> | <span data-ttu-id="59432-292">Określ wartości dla właściwości konfiguracji Spark wymienione w temacie hello: [konfiguracji Spark — właściwości aplikacji](https://spark.apache.org/docs/latest/configuration.html#available-properties).</span><span class="sxs-lookup"><span data-stu-id="59432-292">Specify values for Spark configuration properties listed in hello topic: [Spark Configuration - Application properties](https://spark.apache.org/docs/latest/configuration.html#available-properties).</span></span> | <span data-ttu-id="59432-293">Nie</span><span class="sxs-lookup"><span data-stu-id="59432-293">No</span></span> |
| <span data-ttu-id="59432-294">getDebugInfo</span><span class="sxs-lookup"><span data-stu-id="59432-294">getDebugInfo</span></span> | <span data-ttu-id="59432-295">Określa, kiedy pliki dziennika Spark hello są kopiowane toohello magazynu Azure używanego przez klaster usługi HDInsight (lub) został określony przez sparkJobLinkedService.</span><span class="sxs-lookup"><span data-stu-id="59432-295">Specifies when hello Spark log files are copied toohello Azure storage used by HDInsight cluster (or) specified by sparkJobLinkedService.</span></span> <span data-ttu-id="59432-296">Dozwolone wartości: None, zawsze lub niepowodzenie.</span><span class="sxs-lookup"><span data-stu-id="59432-296">Allowed values: None, Always, or Failure.</span></span> <span data-ttu-id="59432-297">Wartość domyślna: Brak.</span><span class="sxs-lookup"><span data-stu-id="59432-297">Default value: None.</span></span> | <span data-ttu-id="59432-298">Nie</span><span class="sxs-lookup"><span data-stu-id="59432-298">No</span></span> |
| <span data-ttu-id="59432-299">sparkJobLinkedService</span><span class="sxs-lookup"><span data-stu-id="59432-299">sparkJobLinkedService</span></span> | <span data-ttu-id="59432-300">Witaj połączoną usługą magazynu Azure zawierający plik zadania hello Spark, zależności i dzienniki.</span><span class="sxs-lookup"><span data-stu-id="59432-300">hello Azure Storage linked service that holds hello Spark job file, dependencies, and logs.</span></span>  <span data-ttu-id="59432-301">Jeśli nie określisz wartości dla tej właściwości, jest używany Magazyn hello skojarzony z klastrem usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="59432-301">If you do not specify a value for this property, hello storage associated with HDInsight cluster is used.</span></span> | <span data-ttu-id="59432-302">Nie</span><span class="sxs-lookup"><span data-stu-id="59432-302">No</span></span> |

## <a name="folder-structure"></a><span data-ttu-id="59432-303">Struktura folderów</span><span class="sxs-lookup"><span data-stu-id="59432-303">Folder structure</span></span>
<span data-ttu-id="59432-304">Hello Spark działania nie obsługuje skryptu w wierszu jako Pig i do gałęzi działań.</span><span class="sxs-lookup"><span data-stu-id="59432-304">hello Spark activity does not support an in-line script as Pig and Hive activities do.</span></span> <span data-ttu-id="59432-305">Zadań Spark jest również extensible więcej niż zadań Pig/Hive.</span><span class="sxs-lookup"><span data-stu-id="59432-305">Spark jobs are also more extensible than Pig/Hive jobs.</span></span> <span data-ttu-id="59432-306">W przypadku zadań Spark, możesz podać wiele zależności takich jak jar pakietów (umieszczona w języku java hello ścieżki klasy), pliki języka python (umieszczona na powitania PYTHONPATH) i innych plików.</span><span class="sxs-lookup"><span data-stu-id="59432-306">For Spark jobs, you can provide multiple dependencies such as jar packages (placed in hello java CLASSPATH), python files (placed on hello PYTHONPATH), and any other files.</span></span>

<span data-ttu-id="59432-307">Utwórz hello następujące struktury folderów w hello odwołuje się hello HDInsight połączone usługi magazynu obiektów Blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="59432-307">Create hello following folder structure in hello Azure Blob storage referenced by hello HDInsight linked service.</span></span> <span data-ttu-id="59432-308">Natomiast przekazywanie plików zależnych toohello odpowiednie podfoldery w folderze głównym hello reprezentowany przez **entryFilePath**.</span><span class="sxs-lookup"><span data-stu-id="59432-308">Then, upload dependent files toohello appropriate sub folders in hello root folder represented by **entryFilePath**.</span></span> <span data-ttu-id="59432-309">Na przykład Przekaż podfolder pyFiles toohello pliki języka python oraz jar pliki toohello słoików podfolder folderu głównego hello.</span><span class="sxs-lookup"><span data-stu-id="59432-309">For example, upload python files toohello pyFiles subfolder and jar files toohello jars subfolder of hello root folder.</span></span> <span data-ttu-id="59432-310">W czasie wykonywania usługi fabryka danych oczekuje hello następujące struktury folderów w hello magazynu obiektów Blob platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="59432-310">At runtime, Data Factory service expects hello following folder structure in hello Azure Blob storage:</span></span>     

| <span data-ttu-id="59432-311">Ścieżka</span><span class="sxs-lookup"><span data-stu-id="59432-311">Path</span></span> | <span data-ttu-id="59432-312">Opis</span><span class="sxs-lookup"><span data-stu-id="59432-312">Description</span></span> | <span data-ttu-id="59432-313">Wymagane</span><span class="sxs-lookup"><span data-stu-id="59432-313">Required</span></span> | <span data-ttu-id="59432-314">Typ</span><span class="sxs-lookup"><span data-stu-id="59432-314">Type</span></span> |
| ---- | ----------- | -------- | ---- |
| <span data-ttu-id="59432-315">.</span><span class="sxs-lookup"><span data-stu-id="59432-315">.</span></span> | <span data-ttu-id="59432-316">Ścieżka katalogu głównego Hello hello Spark zadania w hello połączoną usługą magazynu</span><span class="sxs-lookup"><span data-stu-id="59432-316">hello root path of hello Spark job in hello storage linked service</span></span>    | <span data-ttu-id="59432-317">Tak</span><span class="sxs-lookup"><span data-stu-id="59432-317">Yes</span></span> | <span data-ttu-id="59432-318">Folder</span><span class="sxs-lookup"><span data-stu-id="59432-318">Folder</span></span> |
| <span data-ttu-id="59432-319">&lt;zdefiniowane przez użytkownika&gt;</span><span class="sxs-lookup"><span data-stu-id="59432-319">&lt;user defined &gt;</span></span> | <span data-ttu-id="59432-320">Ścieżka pliku wpis toohello zadania Spark hello Hello</span><span class="sxs-lookup"><span data-stu-id="59432-320">hello path pointing toohello entry file of hello Spark job</span></span> | <span data-ttu-id="59432-321">Tak</span><span class="sxs-lookup"><span data-stu-id="59432-321">Yes</span></span> | <span data-ttu-id="59432-322">Plik</span><span class="sxs-lookup"><span data-stu-id="59432-322">File</span></span> |
| <span data-ttu-id="59432-323">. / jars</span><span class="sxs-lookup"><span data-stu-id="59432-323">./jars</span></span> | <span data-ttu-id="59432-324">Wszystkie pliki w tym folderze są przekazywane i umieszczane na powitania klasy java hello klastra</span><span class="sxs-lookup"><span data-stu-id="59432-324">All files under this folder are uploaded and placed on hello java classpath of hello cluster</span></span> | <span data-ttu-id="59432-325">Nie</span><span class="sxs-lookup"><span data-stu-id="59432-325">No</span></span> | <span data-ttu-id="59432-326">Folder</span><span class="sxs-lookup"><span data-stu-id="59432-326">Folder</span></span> |
| <span data-ttu-id="59432-327">. / pyFiles</span><span class="sxs-lookup"><span data-stu-id="59432-327">./pyFiles</span></span> | <span data-ttu-id="59432-328">Wszystkie pliki w tym folderze są przekazywane i umieszczane na powitania PYTHONPATH hello klastra</span><span class="sxs-lookup"><span data-stu-id="59432-328">All files under this folder are uploaded and placed on hello PYTHONPATH of hello cluster</span></span> | <span data-ttu-id="59432-329">Nie</span><span class="sxs-lookup"><span data-stu-id="59432-329">No</span></span> | <span data-ttu-id="59432-330">Folder</span><span class="sxs-lookup"><span data-stu-id="59432-330">Folder</span></span> |
| <span data-ttu-id="59432-331">. / pliki</span><span class="sxs-lookup"><span data-stu-id="59432-331">./files</span></span> | <span data-ttu-id="59432-332">Wszystkie pliki w tym folderze są przekazywane i dotyczącymi Moduł wykonujący katalog roboczy</span><span class="sxs-lookup"><span data-stu-id="59432-332">All files under this folder are uploaded and placed on executor working directory</span></span> | <span data-ttu-id="59432-333">Nie</span><span class="sxs-lookup"><span data-stu-id="59432-333">No</span></span> | <span data-ttu-id="59432-334">Folder</span><span class="sxs-lookup"><span data-stu-id="59432-334">Folder</span></span> |
| <span data-ttu-id="59432-335">. / archiwa</span><span class="sxs-lookup"><span data-stu-id="59432-335">./archives</span></span> | <span data-ttu-id="59432-336">Wszystkie pliki w tym folderze są nieskompresowanych</span><span class="sxs-lookup"><span data-stu-id="59432-336">All files under this folder are uncompressed</span></span> | <span data-ttu-id="59432-337">Nie</span><span class="sxs-lookup"><span data-stu-id="59432-337">No</span></span> | <span data-ttu-id="59432-338">Folder</span><span class="sxs-lookup"><span data-stu-id="59432-338">Folder</span></span> |
| <span data-ttu-id="59432-339">. / dzienników</span><span class="sxs-lookup"><span data-stu-id="59432-339">./logs</span></span> | <span data-ttu-id="59432-340">Witaj folder, w którym są przechowywane dzienniki hello klastra Spark.</span><span class="sxs-lookup"><span data-stu-id="59432-340">hello folder where logs from hello Spark cluster are stored.</span></span>| <span data-ttu-id="59432-341">Nie</span><span class="sxs-lookup"><span data-stu-id="59432-341">No</span></span> | <span data-ttu-id="59432-342">Folder</span><span class="sxs-lookup"><span data-stu-id="59432-342">Folder</span></span> |

<span data-ttu-id="59432-343">Oto przykład do magazynu zawierającego dwa pliki zadania Spark w hello odwołuje się hello HDInsight połączone usługi Magazyn obiektów Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="59432-343">Here is an example for a storage containing two Spark job files in hello Azure Blob Storage referenced by hello HDInsight linked service.</span></span>

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
