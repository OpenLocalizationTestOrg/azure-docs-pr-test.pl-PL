---
title: aaaBuild pierwszy fabryki danych (Azure portal) | Dokumentacja firmy Microsoft
description: "W tym samouczku utworzysz potok fabryki danych Azure próbki, przy użyciu Edytor fabryki danych w hello portalu Azure."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: d5b14e9e-e358-45be-943c-5297435d402d
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: fc80776001b181a59c04d80d2e05c20b107a63f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-build-your-first-azure-data-factory-using-azure-portal"></a><span data-ttu-id="b38ab-103">Samouczek: tworzenie pierwszej fabryki danych platformy Azure przy użyciu witryny Azure Portal</span><span class="sxs-lookup"><span data-stu-id="b38ab-103">Tutorial: Build your first Azure data factory using Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b38ab-104">Przegląd i wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="b38ab-104">Overview and prerequisites</span></span>](data-factory-build-your-first-pipeline.md)
> * [<span data-ttu-id="b38ab-105">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="b38ab-105">Azure portal</span></span>](data-factory-build-your-first-pipeline-using-editor.md)
> * [<span data-ttu-id="b38ab-106">Program Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b38ab-106">Visual Studio</span></span>](data-factory-build-your-first-pipeline-using-vs.md)
> * [<span data-ttu-id="b38ab-107">Program PowerShell</span><span class="sxs-lookup"><span data-stu-id="b38ab-107">PowerShell</span></span>](data-factory-build-your-first-pipeline-using-powershell.md)
> * [<span data-ttu-id="b38ab-108">Szablon usługi Resource Manager</span><span class="sxs-lookup"><span data-stu-id="b38ab-108">Resource Manager Template</span></span>](data-factory-build-your-first-pipeline-using-arm.md)
> * [<span data-ttu-id="b38ab-109">Interfejs API REST</span><span class="sxs-lookup"><span data-stu-id="b38ab-109">REST API</span></span>](data-factory-build-your-first-pipeline-using-rest-api.md)


<span data-ttu-id="b38ab-110">W tym artykule dowiesz się, jak toouse [portalu Azure](https://portal.azure.com/) toocreate Twojego pierwszego fabryki danych Azure.</span><span class="sxs-lookup"><span data-stu-id="b38ab-110">In this article, you learn how toouse [Azure portal](https://portal.azure.com/) toocreate your first Azure data factory.</span></span> <span data-ttu-id="b38ab-111">Samouczek hello toodo przy użyciu innych narzędzi/SDK, wybierz jedną z opcji hello z listy rozwijanej hello.</span><span class="sxs-lookup"><span data-stu-id="b38ab-111">toodo hello tutorial using other tools/SDKs, select one of hello options from hello drop-down list.</span></span> 

<span data-ttu-id="b38ab-112">Witaj potoku, w tym samouczku ma jedno działanie: **działania HDInsight Hive**.</span><span class="sxs-lookup"><span data-stu-id="b38ab-112">hello pipeline in this tutorial has one activity: **HDInsight Hive activity**.</span></span> <span data-ttu-id="b38ab-113">To działanie uruchamia skrypt hive w klastrze Azure HDInsight czy transformacji wejściowych danych wyjściowych tooproduce danych.</span><span class="sxs-lookup"><span data-stu-id="b38ab-113">This activity runs a hive script on an Azure HDInsight cluster that transforms input data tooproduce output data.</span></span> <span data-ttu-id="b38ab-114">potok Hello jest zaplanowane toorun po miesiącu między hello określono godziny rozpoczęcia i zakończenia.</span><span class="sxs-lookup"><span data-stu-id="b38ab-114">hello pipeline is scheduled toorun once a month between hello specified start and end times.</span></span> 

> [!NOTE]
> <span data-ttu-id="b38ab-115">Witaj potoku danych w tym samouczku przekształca dane wyjściowe tooproduce danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="b38ab-115">hello data pipeline in this tutorial transforms input data tooproduce output data.</span></span> <span data-ttu-id="b38ab-116">Samouczek na temat danych toocopy przy użyciu fabryki danych Azure, zobacz [samouczek: kopiowanie danych z magazynu obiektów Blob tooSQL bazy danych](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="b38ab-116">For a tutorial on how toocopy data using Azure Data Factory, see [Tutorial: Copy data from Blob Storage tooSQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
> 
> <span data-ttu-id="b38ab-117">Potok może obejmować więcej niż jedno działanie.</span><span class="sxs-lookup"><span data-stu-id="b38ab-117">A pipeline can have more than one activity.</span></span> <span data-ttu-id="b38ab-118">I tworzenia łańcucha dwa działania (Uruchom jedno działanie po drugim), ustawiając hello wyjściowy zestaw danych z jednego działania jako hello wejściowy zestaw danych z hello innych działań.</span><span class="sxs-lookup"><span data-stu-id="b38ab-118">And, you can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="b38ab-119">Więcej informacji znajduje się w artykule dotyczącym [planowania i wykonywania w usłudze Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span><span class="sxs-lookup"><span data-stu-id="b38ab-119">For more information, see [scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b38ab-120">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="b38ab-120">Prerequisites</span></span>
1. <span data-ttu-id="b38ab-121">Zapoznaj się z artykułem [— samouczek Przegląd](data-factory-build-your-first-pipeline.md) artykułu i pełne hello **wymagań wstępnych** czynności.</span><span class="sxs-lookup"><span data-stu-id="b38ab-121">Read through [Tutorial Overview](data-factory-build-your-first-pipeline.md) article and complete hello **prerequisite** steps.</span></span>
2. <span data-ttu-id="b38ab-122">W tym artykule nie zawiera omówienie hello usługi fabryka danych Azure.</span><span class="sxs-lookup"><span data-stu-id="b38ab-122">This article does not provide a conceptual overview of hello Azure Data Factory service.</span></span> <span data-ttu-id="b38ab-123">Firma Microsoft zaleca zapoznanie [tooAzure wprowadzenie fabryki danych](data-factory-introduction.md) artykuł, aby szczegółowy przegląd hello usługi.</span><span class="sxs-lookup"><span data-stu-id="b38ab-123">We recommend that you go through [Introduction tooAzure Data Factory](data-factory-introduction.md) article for a detailed overview of hello service.</span></span>  

## <a name="create-data-factory"></a><span data-ttu-id="b38ab-124">Tworzenie fabryki danych</span><span class="sxs-lookup"><span data-stu-id="b38ab-124">Create data factory</span></span>
<span data-ttu-id="b38ab-125">Fabryka danych może obejmować jeden lub wiele potoków.</span><span class="sxs-lookup"><span data-stu-id="b38ab-125">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="b38ab-126">Potok może obejmować jedno lub wiele działań.</span><span class="sxs-lookup"><span data-stu-id="b38ab-126">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="b38ab-127">Na przykład toocopy działanie kopiowania danych z magazynu danych docelowy tooa źródłowego i HDInsight Hive działania toorun tootransform skryptu Hive wejściowe dane wyjściowe tooproduct danych.</span><span class="sxs-lookup"><span data-stu-id="b38ab-127">For example, a Copy Activity toocopy data from a source tooa destination data store and a HDInsight Hive activity toorun a Hive script tootransform input data tooproduct output data.</span></span> <span data-ttu-id="b38ab-128">Zacznijmy od utworzenia hello fabryki danych w tym kroku.</span><span class="sxs-lookup"><span data-stu-id="b38ab-128">Let's start with creating hello data factory in this step.</span></span>

1. <span data-ttu-id="b38ab-129">Zaloguj się za toohello [portalu Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="b38ab-129">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="b38ab-130">Kliknij przycisk **nowy** w menu po lewej stronie powitania kliknij **dane i analiza**i kliknij przycisk **fabryki danych**.</span><span class="sxs-lookup"><span data-stu-id="b38ab-130">Click **NEW** on hello left menu, click **Data + Analytics**, and click **Data Factory**.</span></span>

   ![Blok tworzenia](./media/data-factory-build-your-first-pipeline-using-editor/create-blade.png)
3. <span data-ttu-id="b38ab-132">W hello **nowa fabryka danych** bloku, wprowadź **GetStartedDF** dla hello nazwy.</span><span class="sxs-lookup"><span data-stu-id="b38ab-132">In hello **New data factory** blade, enter **GetStartedDF** for hello Name.</span></span>

   ![Blok Nowa fabryka danych](./media/data-factory-build-your-first-pipeline-using-editor/new-data-factory-blade.png)

   > [!IMPORTANT]
   > <span data-ttu-id="b38ab-134">Nazwa fabryki danych Azure hello Hello musi być **unikatowych**.</span><span class="sxs-lookup"><span data-stu-id="b38ab-134">hello name of hello Azure data factory must be **globally unique**.</span></span> <span data-ttu-id="b38ab-135">Jeśli wystąpi błąd hello: **nazwa fabryki danych "GetStartedDF" nie jest dostępny**.</span><span class="sxs-lookup"><span data-stu-id="b38ab-135">If you receive hello error: **Data factory name “GetStartedDF” is not available**.</span></span> <span data-ttu-id="b38ab-136">Zmień nazwę hello hello fabryki danych (na przykład yournameGetStartedDF), a następnie spróbuj ponownie utworzyć.</span><span class="sxs-lookup"><span data-stu-id="b38ab-136">Change hello name of hello data factory (for example, yournameGetStartedDF) and try creating again.</span></span> <span data-ttu-id="b38ab-137">Artykuł [Data Factory — Naming Rules](data-factory-naming-rules.md) (Fabryka danych — zasady nazewnictwa) zawiera zasady nazewnictwa artefaktów usługi Fabryka danych.</span><span class="sxs-lookup"><span data-stu-id="b38ab-137">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>
   >
   > <span data-ttu-id="b38ab-138">Nazwa fabryki danych hello Hello może zostać zarejestrowana jako **DNS** nazwy w przyszłości hello i dlatego stać się publicznie widoczna.</span><span class="sxs-lookup"><span data-stu-id="b38ab-138">hello name of hello data factory may be registered as a **DNS** name in hello future and hence become publically visible.</span></span>
   >
   >
4. <span data-ttu-id="b38ab-139">Wybierz hello **subskrypcji platformy Azure** miejscu toobe fabryki danych hello utworzony.</span><span class="sxs-lookup"><span data-stu-id="b38ab-139">Select hello **Azure subscription** where you want hello data factory toobe created.</span></span>
5. <span data-ttu-id="b38ab-140">Wybierz istniejącą **grupę zasobów** lub utwórz grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="b38ab-140">Select existing **resource group** or create a resource group.</span></span> <span data-ttu-id="b38ab-141">Samouczek hello, Utwórz grupę zasobów o nazwie: **ADFGetStartedRG**.</span><span class="sxs-lookup"><span data-stu-id="b38ab-141">For hello tutorial, create a resource group named: **ADFGetStartedRG**.</span></span>
6. <span data-ttu-id="b38ab-142">Wybierz hello **lokalizacji** hello fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="b38ab-142">Select hello **location** for hello data factory.</span></span> <span data-ttu-id="b38ab-143">Tylko regiony obsługiwane przez hello usługi fabryka danych są wyświetlane na liście rozwijanej hello.</span><span class="sxs-lookup"><span data-stu-id="b38ab-143">Only regions supported by hello Data Factory service are shown in hello drop-down list.</span></span>
7. <span data-ttu-id="b38ab-144">Wybierz **toodashboard numeru Pin**.</span><span class="sxs-lookup"><span data-stu-id="b38ab-144">Select **Pin toodashboard**.</span></span> 
8. <span data-ttu-id="b38ab-145">Kliknij przycisk **Utwórz** na powitania **nowa fabryka danych** bloku.</span><span class="sxs-lookup"><span data-stu-id="b38ab-145">Click **Create** on hello **New data factory** blade.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="b38ab-146">toocreate wystąpienia fabryki danych, musi być członkiem hello [współautora fabryki danych](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) roli na poziomie grupy zasobów subskrypcji hello.</span><span class="sxs-lookup"><span data-stu-id="b38ab-146">toocreate Data Factory instances, you must be a member of hello [Data Factory Contributor](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) role at hello subscription/resource group level.</span></span>
   >
   >
7. <span data-ttu-id="b38ab-147">Na pulpicie nawigacyjnym hello, zobacz następujące hello kafelka ze stanem: Wdrażanie fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="b38ab-147">On hello dashboard, you see hello following tile with status: Deploying data factory.</span></span>    

   ![Stan tworzenia fabryki danych](./media/data-factory-build-your-first-pipeline-using-editor/creating-data-factory-image.png)
8. <span data-ttu-id="b38ab-149">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="b38ab-149">Congratulations!</span></span> <span data-ttu-id="b38ab-150">Udało Ci się utworzyć pierwszą fabrykę danych.</span><span class="sxs-lookup"><span data-stu-id="b38ab-150">You have successfully created your first data factory.</span></span> <span data-ttu-id="b38ab-151">Po hello fabryki danych został utworzony pomyślnie, zobacz strony fabryki danych hello, który umożliwia hello zawartość hello fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="b38ab-151">After hello data factory has been created successfully, you see hello data factory page, which shows you hello contents of hello data factory.</span></span>     

    ![Blok Fabryka danych](./media/data-factory-build-your-first-pipeline-using-editor/data-factory-blade.png)

<span data-ttu-id="b38ab-153">Przed utworzeniem potok w fabryce danych hello, należy toocreate kilku jednostek fabryki danych najpierw.</span><span class="sxs-lookup"><span data-stu-id="b38ab-153">Before creating a pipeline in hello data factory, you need toocreate a few Data Factory entities first.</span></span> <span data-ttu-id="b38ab-154">Najpierw utwórz danych toolink połączonych usług danych tooyour magazyny/oblicza przechowywania, zdefiniuj dane wejściowe i zestawów danych toorepresent wejścia/wyjścia dane w magazynach połączone dane wyjściowe, a następnie utwórz hello potoku do działania, która używa tych zestawów danych.</span><span class="sxs-lookup"><span data-stu-id="b38ab-154">You first create linked services toolink data stores/computes tooyour data store, define input and output datasets toorepresent input/output data in linked data stores, and then create hello pipeline with an activity that uses these datasets.</span></span>

## <a name="create-linked-services"></a><span data-ttu-id="b38ab-155">Tworzenie połączonych usług</span><span class="sxs-lookup"><span data-stu-id="b38ab-155">Create linked services</span></span>
<span data-ttu-id="b38ab-156">W tym kroku możesz połączyć konta magazynu Azure i fabrykę danych tooyour klastra Azure HDInsight na żądanie.</span><span class="sxs-lookup"><span data-stu-id="b38ab-156">In this step, you link your Azure Storage account and an on-demand Azure HDInsight cluster tooyour data factory.</span></span> <span data-ttu-id="b38ab-157">blokady konta usługi Azure Storage Hello hello danych wejściowych i wyjściowych do potoku hello w tym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="b38ab-157">hello Azure Storage account holds hello input and output data for hello pipeline in this sample.</span></span> <span data-ttu-id="b38ab-158">Hello usługi HDInsight połączony jest używane toorun określony w działaniu hello hello potoku, w tym przykładzie skrypt Hive.</span><span class="sxs-lookup"><span data-stu-id="b38ab-158">hello HDInsight linked service is used toorun a Hive script specified in hello activity of hello pipeline in this sample.</span></span> <span data-ttu-id="b38ab-159">Zidentyfikuj co [magazynu danych](data-factory-data-movement-activities.md)/[obliczeniowe usług](data-factory-compute-linked-services.md) są używane w danym scenariuszu i łączenie fabryki danych toohello tych usług za tworzenie połączonych usług.</span><span class="sxs-lookup"><span data-stu-id="b38ab-159">Identify what [data store](data-factory-data-movement-activities.md)/[compute services](data-factory-compute-linked-services.md) are used in your scenario and link those services toohello data factory by creating linked services.</span></span>  

### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="b38ab-160">Tworzenie połączonej usługi Azure Storage</span><span class="sxs-lookup"><span data-stu-id="b38ab-160">Create Azure Storage linked service</span></span>
<span data-ttu-id="b38ab-161">W tym kroku możesz połączyć fabrykę danych tooyour konta magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="b38ab-161">In this step, you link your Azure Storage account tooyour data factory.</span></span> <span data-ttu-id="b38ab-162">W tym samouczku użyjesz hello tego samego konta magazynu Azure toostore wejścia/wyjścia danych i hello HQL plik skryptu.</span><span class="sxs-lookup"><span data-stu-id="b38ab-162">In this tutorial, you use hello same Azure Storage account toostore input/output data and hello HQL script file.</span></span>

1. <span data-ttu-id="b38ab-163">Kliknij przycisk **tworzenie i wdrażanie** na powitania **FABRYKI danych** bloku **GetStartedDF**.</span><span class="sxs-lookup"><span data-stu-id="b38ab-163">Click **Author and deploy** on hello **DATA FACTORY** blade for **GetStartedDF**.</span></span> <span data-ttu-id="b38ab-164">Powinny pojawić się hello Edytor fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="b38ab-164">You should see hello Data Factory Editor.</span></span>

   ![Kafelek Utwórz i wdróż](./media/data-factory-build-your-first-pipeline-using-editor/data-factory-author-deploy.png)
2. <span data-ttu-id="b38ab-166">Kliknij przycisk **Nowy magazyn danych** i wybierz opcję **Azure Storage**.</span><span class="sxs-lookup"><span data-stu-id="b38ab-166">Click **New data store** and choose **Azure storage**.</span></span>

   ![Nowy magazyn danych — Azure Storage — menu](./media/data-factory-build-your-first-pipeline-using-editor/new-data-store-azure-storage-menu.png)
3. <span data-ttu-id="b38ab-168">Powinny pojawić się hello skryptu JSON do tworzenia usługi Azure Storage połączonej usługi w edytorze hello.</span><span class="sxs-lookup"><span data-stu-id="b38ab-168">You should see hello JSON script for creating an Azure Storage linked service in hello editor.</span></span>

   ![Połączona usługa Azure Storage](./media/data-factory-build-your-first-pipeline-using-editor/azure-storage-linked-service.png)
4. <span data-ttu-id="b38ab-170">Zastąp **nazwa konta** hello nazwą konta magazynu Azure i **klucz konta** z klucz dostępu hello hello kontem magazynu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="b38ab-170">Replace **account name** with hello name of your Azure storage account and **account key** with hello access key of hello Azure storage account.</span></span> <span data-ttu-id="b38ab-171">toolearn sposób dostępu do magazynu tooget klucza, zobacz hello informacji na temat sposobu tooview, kopiowania i regenerate magazynu dostępu do kluczy w [Zarządzanie kontem magazynu](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="b38ab-171">toolearn how tooget your storage access key, see hello information about how tooview, copy, and regenerate storage access keys in [Manage your storage account](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>
5. <span data-ttu-id="b38ab-172">Kliknij przycisk **Wdróż** na pasku toodeploy hello połączone usługi poleceń hello.</span><span class="sxs-lookup"><span data-stu-id="b38ab-172">Click **Deploy** on hello command bar toodeploy hello linked service.</span></span>

    ![Przycisk Wdróż](./media/data-factory-build-your-first-pipeline-using-editor/deploy-button.png)

   <span data-ttu-id="b38ab-174">Witaj po hello połączonej usługi został wdrożony pomyślnie, **projekt 1** powinien zniknąć okna, aby zobaczyć **AzureStorageLinkedService** w widoku drzewa hello powitania po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="b38ab-174">After hello linked service is deployed successfully, hello **Draft-1** window should disappear and you see **AzureStorageLinkedService** in hello tree view on hello left.</span></span>

    ![Połączona usługa Storage w menu](./media/data-factory-build-your-first-pipeline-using-editor/StorageLinkedServiceInTree.png)    

### <a name="create-azure-hdinsight-linked-service"></a><span data-ttu-id="b38ab-176">Tworzenie połączonej usługi Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="b38ab-176">Create Azure HDInsight linked service</span></span>
<span data-ttu-id="b38ab-177">W tym kroku możesz połączyć fabrykę danych tooyour klastra usługi HDInsight na żądanie.</span><span class="sxs-lookup"><span data-stu-id="b38ab-177">In this step, you link an on-demand HDInsight cluster tooyour data factory.</span></span> <span data-ttu-id="b38ab-178">klaster usługi HDInsight Hello jest automatycznie tworzone w czasie wykonywania i usuwane po zakończeniu przetwarzania i bezczynności hello określoną ilość czasu.</span><span class="sxs-lookup"><span data-stu-id="b38ab-178">hello HDInsight cluster is automatically created at runtime and deleted after it is done processing and idle for hello specified amount of time.</span></span>

1. <span data-ttu-id="b38ab-179">W hello **Edytor fabryki danych**, kliknij przycisk **... więcej**, kliknij przycisk **Nowe obliczenie** i wybierz **Klaster usługi HDInsight na żądanie**.</span><span class="sxs-lookup"><span data-stu-id="b38ab-179">In hello **Data Factory Editor**, click **... More**, click **New compute**, and select **On-demand HDInsight cluster**.</span></span>

    ![Nowe obliczenie](./media/data-factory-build-your-first-pipeline-using-editor/new-compute-menu.png)
2. <span data-ttu-id="b38ab-181">Skopiuj i Wklej powitania po toohello fragment **projekt 1** okna.</span><span class="sxs-lookup"><span data-stu-id="b38ab-181">Copy and paste hello following snippet toohello **Draft-1** window.</span></span> <span data-ttu-id="b38ab-182">fragment kodu JSON Hello opisuje hello właściwości, które są używane toocreate hello HDInsight klastra na żądanie.</span><span class="sxs-lookup"><span data-stu-id="b38ab-182">hello JSON snippet describes hello properties that are used toocreate hello HDInsight cluster on-demand.</span></span>

    ```JSON
    {
        "name": "HDInsightOnDemandLinkedService",
        "properties": {
            "type": "HDInsightOnDemand",
            "typeProperties": {
                "version": "3.5",
                "clusterSize": 1,
                "timeToLive": "00:05:00",
                "osType": "Linux",
                "linkedServiceName": "AzureStorageLinkedService"
            }
        }
    }
    ```

    <span data-ttu-id="b38ab-183">Witaj Poniższa tabela zawiera opisy właściwości JSON hello używane we fragmencie hello:</span><span class="sxs-lookup"><span data-stu-id="b38ab-183">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

   | <span data-ttu-id="b38ab-184">Właściwość</span><span class="sxs-lookup"><span data-stu-id="b38ab-184">Property</span></span> | <span data-ttu-id="b38ab-185">Opis</span><span class="sxs-lookup"><span data-stu-id="b38ab-185">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="b38ab-186">ClusterSize</span><span class="sxs-lookup"><span data-stu-id="b38ab-186">ClusterSize</span></span> |<span data-ttu-id="b38ab-187">Określa rozmiar hello hello klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b38ab-187">Specifies hello size of hello HDInsight cluster.</span></span> |
   | <span data-ttu-id="b38ab-188">TimeToLive</span><span class="sxs-lookup"><span data-stu-id="b38ab-188">TimeToLive</span></span> | <span data-ttu-id="b38ab-189">Określa czas bezczynności tej hello hello klastra usługi HDInsight, przed usunięciem.</span><span class="sxs-lookup"><span data-stu-id="b38ab-189">Specifies that hello idle time for hello HDInsight cluster, before it is deleted.</span></span> |
   | <span data-ttu-id="b38ab-190">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="b38ab-190">linkedServiceName</span></span> | <span data-ttu-id="b38ab-191">Określa konto magazynu hello, które jest używane toostore hello dzienniki, generowanych przez usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b38ab-191">Specifies hello storage account that is used toostore hello logs that are generated by HDInsight.</span></span> |

    <span data-ttu-id="b38ab-192">Należy zwrócić uwagę hello następujące punkty:</span><span class="sxs-lookup"><span data-stu-id="b38ab-192">Note hello following points:</span></span>

   * <span data-ttu-id="b38ab-193">Witaj fabryki danych tworzy **opartych na systemie Linux** klastra usługi HDInsight za pomocą hello JSON.</span><span class="sxs-lookup"><span data-stu-id="b38ab-193">hello Data Factory creates a **Linux-based** HDInsight cluster for you with hello JSON.</span></span> <span data-ttu-id="b38ab-194">Szczegółowe informacje znajdują się w artykule [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) (Połączona usługa HDInsight na żądanie).</span><span class="sxs-lookup"><span data-stu-id="b38ab-194">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>
   * <span data-ttu-id="b38ab-195">Możesz użyć **własnego klastra usługi HDInsight** zamiast klastra usługi HDInsight na żądanie.</span><span class="sxs-lookup"><span data-stu-id="b38ab-195">You could use **your own HDInsight cluster** instead of using an on-demand HDInsight cluster.</span></span> <span data-ttu-id="b38ab-196">Szczegółowe informacje znajdują się w artykule [HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) (Połączona usługa HDInsight).</span><span class="sxs-lookup"><span data-stu-id="b38ab-196">See [HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) for details.</span></span>
   * <span data-ttu-id="b38ab-197">Tworzy klaster usługi HDInsight Hello **domyślny kontener** w magazynie obiektów blob hello określone w hello JSON (**linkedServiceName**).</span><span class="sxs-lookup"><span data-stu-id="b38ab-197">hello HDInsight cluster creates a **default container** in hello blob storage you specified in hello JSON (**linkedServiceName**).</span></span> <span data-ttu-id="b38ab-198">Po usunięciu klastra hello HDInsight nie usunie tego kontenera.</span><span class="sxs-lookup"><span data-stu-id="b38ab-198">HDInsight does not delete this container when hello cluster is deleted.</span></span> <span data-ttu-id="b38ab-199">To zachowanie jest celowe.</span><span class="sxs-lookup"><span data-stu-id="b38ab-199">This behavior is by design.</span></span> <span data-ttu-id="b38ab-200">W przypadku połączonej usługi HDInsight na żądanie klaster usługi HDInsight jest tworzony przy każdym przetwarzaniu wycinka — o ile w tym momencie nie istnieje aktywny klaster (**timeToLive**).</span><span class="sxs-lookup"><span data-stu-id="b38ab-200">With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice is processed unless there is an existing live cluster (**timeToLive**).</span></span> <span data-ttu-id="b38ab-201">klaster Hello są automatycznie usuwane po zakończeniu przetwarzania hello.</span><span class="sxs-lookup"><span data-stu-id="b38ab-201">hello cluster is automatically deleted when hello processing is done.</span></span>

       <span data-ttu-id="b38ab-202">Po przetworzeniu większej liczby wycinków w usłudze Azure Blob Storage będzie widocznych wiele kontenerów.</span><span class="sxs-lookup"><span data-stu-id="b38ab-202">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="b38ab-203">Jeśli nie ma potrzeby do rozwiązywania problemów hello zadań, możesz toodelete ich magazynu hello tooreduce kosztów.</span><span class="sxs-lookup"><span data-stu-id="b38ab-203">If you do not need them for troubleshooting of hello jobs, you may want toodelete them tooreduce hello storage cost.</span></span> <span data-ttu-id="b38ab-204">nazwy Hello kontenery wykonaj wzorca: "adf**yourdatafactoryname**-**linkedservicename**- datetimestamp".</span><span class="sxs-lookup"><span data-stu-id="b38ab-204">hello names of these containers follow a pattern: "adf**yourdatafactoryname**-**linkedservicename**-datetimestamp".</span></span> <span data-ttu-id="b38ab-205">Użyj narzędzia takiego jak [Eksploratora magazynu](http://storageexplorer.com/) magazynu obiektów blob toodelete kontenerów w platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="b38ab-205">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) toodelete containers in your Azure blob storage.</span></span>

     <span data-ttu-id="b38ab-206">Szczegółowe informacje znajdują się w artykule [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) (Połączona usługa HDInsight na żądanie).</span><span class="sxs-lookup"><span data-stu-id="b38ab-206">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>
3. <span data-ttu-id="b38ab-207">Kliknij przycisk **Wdróż** na pasku toodeploy hello połączone usługi poleceń hello.</span><span class="sxs-lookup"><span data-stu-id="b38ab-207">Click **Deploy** on hello command bar toodeploy hello linked service.</span></span>

    ![Wdrażanie połączonej usługi HDInsight na żądanie](./media/data-factory-build-your-first-pipeline-using-editor/ondemand-hdinsight-deploy.png)
4. <span data-ttu-id="b38ab-209">Upewnij się, że wyświetlany jest zarówno **AzureStorageLinkedService** i **HDInsightOnDemandLinkedService** w widoku drzewa hello powitania po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="b38ab-209">Confirm that you see both **AzureStorageLinkedService** and **HDInsightOnDemandLinkedService** in hello tree view on hello left.</span></span>

    ![Widok drzewa z połączonymi usługami](./media/data-factory-build-your-first-pipeline-using-editor/tree-view-linked-services.png)

## <a name="create-datasets"></a><span data-ttu-id="b38ab-211">Tworzenie zestawów danych</span><span class="sxs-lookup"><span data-stu-id="b38ab-211">Create datasets</span></span>
<span data-ttu-id="b38ab-212">W tym kroku utwórz wprowadzania hello toorepresent zestawów danych i wysyłania danych do przetwarzania Hive.</span><span class="sxs-lookup"><span data-stu-id="b38ab-212">In this step, you create datasets toorepresent hello input and output data for Hive processing.</span></span> <span data-ttu-id="b38ab-213">Te zestawy danych można znaleźć toohello **AzureStorageLinkedService** został utworzony we wcześniejszej części tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="b38ab-213">These datasets refer toohello **AzureStorageLinkedService** you have created earlier in this tutorial.</span></span> <span data-ttu-id="b38ab-214">Witaj tooan punktów połączonej usługi konta usługi Azure Storage i zestawów danych, określ kontener, folder, nazwa pliku w magazynie hello, która przechowuje dane wejściowe i wyjściowe danych.</span><span class="sxs-lookup"><span data-stu-id="b38ab-214">hello linked service points tooan Azure Storage account and datasets specify container, folder, file name in hello storage that holds input and output data.</span></span>   

### <a name="create-input-dataset"></a><span data-ttu-id="b38ab-215">Tworzenie wejściowego zestawu danych</span><span class="sxs-lookup"><span data-stu-id="b38ab-215">Create input dataset</span></span>
1. <span data-ttu-id="b38ab-216">W hello **Edytor fabryki danych**, kliknij przycisk **... Więcej** na pasku poleceń powitania kliknij **nowy zestaw danych**i wybierz **magazynu obiektów Blob Azure**.</span><span class="sxs-lookup"><span data-stu-id="b38ab-216">In hello **Data Factory Editor**, click **... More** on hello command bar, click **New dataset**, and select **Azure Blob storage**.</span></span>

    ![Nowy zestaw danych](./media/data-factory-build-your-first-pipeline-using-editor/new-data-set.png)
2. <span data-ttu-id="b38ab-218">Skopiuj i Wklej powitania po fragment okna toohello projekt-1.</span><span class="sxs-lookup"><span data-stu-id="b38ab-218">Copy and paste hello following snippet toohello Draft-1 window.</span></span> <span data-ttu-id="b38ab-219">We fragmencie JSON hello, tworzysz zestawu danych o nazwie **AzureBlobInput** reprezentujący dane wejściowe dla działania w potoku hello.</span><span class="sxs-lookup"><span data-stu-id="b38ab-219">In hello JSON snippet, you are creating a dataset called **AzureBlobInput** that represents input data for an activity in hello pipeline.</span></span> <span data-ttu-id="b38ab-220">Ponadto należy określić czy danych wejściowych hello znajduje się w kontenerze obiektów blob hello o nazwie **adfgetstarted** i hello folder o nazwie **inputdata**.</span><span class="sxs-lookup"><span data-stu-id="b38ab-220">In addition, you specify that hello input data is located in hello blob container called **adfgetstarted** and hello folder called **inputdata**.</span></span>

    ```JSON
    {
        "name": "AzureBlobInput",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService",
            "typeProperties": {
                "fileName": "input.log",
                "folderPath": "adfgetstarted/inputdata",
                "format": {
                    "type": "TextFormat",
                    "columnDelimiter": ","
                }
            },
            "availability": {
                "frequency": "Month",
                "interval": 1
            },
            "external": true,
            "policy": {}
        }
    }
    ```
    <span data-ttu-id="b38ab-221">Witaj Poniższa tabela zawiera opisy właściwości JSON hello używane we fragmencie hello:</span><span class="sxs-lookup"><span data-stu-id="b38ab-221">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

   | <span data-ttu-id="b38ab-222">Właściwość</span><span class="sxs-lookup"><span data-stu-id="b38ab-222">Property</span></span> | <span data-ttu-id="b38ab-223">Opis</span><span class="sxs-lookup"><span data-stu-id="b38ab-223">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="b38ab-224">type</span><span class="sxs-lookup"><span data-stu-id="b38ab-224">type</span></span> |<span data-ttu-id="b38ab-225">Właściwość type Hello ustawiono zbyt**AzureBlob** ponieważ danych znajduje się w magazynie obiektów blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="b38ab-225">hello type property is set too**AzureBlob** because data resides in an Azure blob storage.</span></span> |
   | <span data-ttu-id="b38ab-226">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="b38ab-226">linkedServiceName</span></span> |<span data-ttu-id="b38ab-227">Odwołuje się toohello **AzureStorageLinkedService** utworzony wcześniej.</span><span class="sxs-lookup"><span data-stu-id="b38ab-227">Refers toohello **AzureStorageLinkedService** you created earlier.</span></span> |
   | <span data-ttu-id="b38ab-228">folderPath</span><span class="sxs-lookup"><span data-stu-id="b38ab-228">folderPath</span></span> | <span data-ttu-id="b38ab-229">Określa obiekt blob hello **kontenera** i hello **folderu** zawiera obiekty BLOB wejściowego.</span><span class="sxs-lookup"><span data-stu-id="b38ab-229">Specifies hello blob **container** and hello **folder** that contains input blobs.</span></span> | 
   | <span data-ttu-id="b38ab-230">fileName</span><span class="sxs-lookup"><span data-stu-id="b38ab-230">fileName</span></span> |<span data-ttu-id="b38ab-231">Ta właściwość jest opcjonalna.</span><span class="sxs-lookup"><span data-stu-id="b38ab-231">This property is optional.</span></span> <span data-ttu-id="b38ab-232">W przypadku pominięcia tej właściwości, pobierane są wszystkie pliki hello z hello folderPath.</span><span class="sxs-lookup"><span data-stu-id="b38ab-232">If you omit this property, all hello files from hello folderPath are picked.</span></span> <span data-ttu-id="b38ab-233">W tym samouczku tylko hello **input.log** jest przetwarzany.</span><span class="sxs-lookup"><span data-stu-id="b38ab-233">In this tutorial, only hello **input.log** is processed.</span></span> |
   | <span data-ttu-id="b38ab-234">type</span><span class="sxs-lookup"><span data-stu-id="b38ab-234">type</span></span> |<span data-ttu-id="b38ab-235">pliki dziennika Hello są w formacie tekstowym, więc używamy **TextFormat**.</span><span class="sxs-lookup"><span data-stu-id="b38ab-235">hello log files are in text format, so we use **TextFormat**.</span></span> |
   | <span data-ttu-id="b38ab-236">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="b38ab-236">columnDelimiter</span></span> |<span data-ttu-id="b38ab-237">kolumn w plikach dziennika hello są rozdzielane **przecinka (`,`)**</span><span class="sxs-lookup"><span data-stu-id="b38ab-237">columns in hello log files are delimited by **comma character (`,`)**</span></span> |
   | <span data-ttu-id="b38ab-238">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="b38ab-238">frequency/interval</span></span> |<span data-ttu-id="b38ab-239">częstotliwość ustawiona zbyt**miesiąca** i interwał **1**, co oznacza, że hello wejściowych wycinków dostępnych co miesiąc.</span><span class="sxs-lookup"><span data-stu-id="b38ab-239">frequency set too**Month** and interval is **1**, which means that hello input slices are available monthly.</span></span> |
   | <span data-ttu-id="b38ab-240">external</span><span class="sxs-lookup"><span data-stu-id="b38ab-240">external</span></span> | <span data-ttu-id="b38ab-241">Ta właściwość jest ustawiona zbyt**true** czy hello danych wejściowych nie jest generowany przez tego potoku.</span><span class="sxs-lookup"><span data-stu-id="b38ab-241">This property is set too**true** if hello input data is not generated by this pipeline.</span></span> <span data-ttu-id="b38ab-242">W tym samouczku hello input.log plik nie jest generowany przez tego potoku, możemy ustawić hello tootrue właściwości.</span><span class="sxs-lookup"><span data-stu-id="b38ab-242">In this tutorial, hello input.log file is not generated by this pipeline, so we set hello property tootrue.</span></span> |

    <span data-ttu-id="b38ab-243">Aby uzyskać więcej informacji o tych właściwościach JSON, zobacz [artykuł dotyczący łącznika obiektu blob platformy Azure](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="b38ab-243">For more information about these JSON properties, see [Azure Blob connector article](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
3. <span data-ttu-id="b38ab-244">Kliknij przycisk **Wdróż** polecenie hello paska toodeploy hello nowo utworzony w zestawie danych.</span><span class="sxs-lookup"><span data-stu-id="b38ab-244">Click **Deploy** on hello command bar toodeploy hello newly created dataset.</span></span> <span data-ttu-id="b38ab-245">Zestaw danych hello w hello widok drzewa po lewej stronie powitania powinna zostać wyświetlona.</span><span class="sxs-lookup"><span data-stu-id="b38ab-245">You should see hello dataset in hello tree view on hello left.</span></span>

### <a name="create-output-dataset"></a><span data-ttu-id="b38ab-246">Tworzenie wyjściowego zestawu danych</span><span class="sxs-lookup"><span data-stu-id="b38ab-246">Create output dataset</span></span>
<span data-ttu-id="b38ab-247">Można teraz utworzyć hello wyjściowego zestawu danych toorepresent hello danych wyjściowych danych przechowywanych w hello magazynu obiektów Blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="b38ab-247">Now, you create hello output dataset toorepresent hello output data stored in hello Azure Blob storage.</span></span>

1. <span data-ttu-id="b38ab-248">W hello **Edytor fabryki danych**, kliknij przycisk **... Więcej** na pasku poleceń powitania kliknij **nowy zestaw danych**i wybierz **magazynu obiektów Blob Azure**.</span><span class="sxs-lookup"><span data-stu-id="b38ab-248">In hello **Data Factory Editor**, click **... More** on hello command bar, click **New dataset**, and select **Azure Blob storage**.</span></span>  
2. <span data-ttu-id="b38ab-249">Skopiuj i Wklej powitania po fragment okna toohello projekt-1.</span><span class="sxs-lookup"><span data-stu-id="b38ab-249">Copy and paste hello following snippet toohello Draft-1 window.</span></span> <span data-ttu-id="b38ab-250">We fragmencie JSON hello, tworzysz zestawu danych o nazwie **AzureBlobOutput**i określając hello struktury danych hello jest generowany przez hello skryptu Hive.</span><span class="sxs-lookup"><span data-stu-id="b38ab-250">In hello JSON snippet, you are creating a dataset called **AzureBlobOutput**, and specifying hello structure of hello data that is produced by hello Hive script.</span></span> <span data-ttu-id="b38ab-251">Ponadto należy określić czy hello wyniki są przechowywane w kontenerze obiektów blob hello o nazwie **adfgetstarted** i hello folder o nazwie **partitioneddata**.</span><span class="sxs-lookup"><span data-stu-id="b38ab-251">In addition, you specify that hello results are stored in hello blob container called **adfgetstarted** and hello folder called **partitioneddata**.</span></span> <span data-ttu-id="b38ab-252">Witaj **dostępności** sekcja określa, że wyjściowy zestaw danych hello jest tworzony co miesiąc.</span><span class="sxs-lookup"><span data-stu-id="b38ab-252">hello **availability** section specifies that hello output dataset is produced on a monthly basis.</span></span>

    ```JSON
    {
      "name": "AzureBlobOutput",
      "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
          "folderPath": "adfgetstarted/partitioneddata",
          "format": {
            "type": "TextFormat",
            "columnDelimiter": ","
          }
        },
        "availability": {
          "frequency": "Month",
          "interval": 1
        }
      }
    }
    ```
    <span data-ttu-id="b38ab-253">Zobacz **utworzyć zestaw danych wejściowych hello** sekcji, aby uzyskać opis tych właściwości.</span><span class="sxs-lookup"><span data-stu-id="b38ab-253">See **Create hello input dataset** section for descriptions of these properties.</span></span> <span data-ttu-id="b38ab-254">Nie należy ustawiać właściwości zewnętrznych hello na wyjściowy zestaw danych, zgodnie z zestawu danych hello jest generowany przez hello usługi fabryka danych.</span><span class="sxs-lookup"><span data-stu-id="b38ab-254">You do not set hello external property on an output dataset as hello dataset is produced by hello Data Factory service.</span></span>
3. <span data-ttu-id="b38ab-255">Kliknij przycisk **Wdróż** polecenie hello paska toodeploy hello nowo utworzony w zestawie danych.</span><span class="sxs-lookup"><span data-stu-id="b38ab-255">Click **Deploy** on hello command bar toodeploy hello newly created dataset.</span></span>
4. <span data-ttu-id="b38ab-256">Sprawdź, czy pomyślnie utworzono ten zestaw danych hello.</span><span class="sxs-lookup"><span data-stu-id="b38ab-256">Verify that hello dataset is created successfully.</span></span>

    ![Widok drzewa z połączonymi usługami](./media/data-factory-build-your-first-pipeline-using-editor/tree-view-data-set.png)

## <a name="create-pipeline"></a><span data-ttu-id="b38ab-258">Tworzenie potoku</span><span class="sxs-lookup"><span data-stu-id="b38ab-258">Create pipeline</span></span>
<span data-ttu-id="b38ab-259">W tym kroku opisano tworzenie pierwszego potoku za pomocą działania **HDInsightHive**.</span><span class="sxs-lookup"><span data-stu-id="b38ab-259">In this step, you create your first pipeline with a **HDInsightHive** activity.</span></span> <span data-ttu-id="b38ab-260">Wejściowy jest dostępny co miesiąc (częstotliwość: miesiąc, interwał: 1), wycinek danych wyjściowych jest tworzony co miesiąc, a właściwość harmonogramu hello działania hello jest ustawić toomonthly.</span><span class="sxs-lookup"><span data-stu-id="b38ab-260">Input slice is available monthly (frequency: Month, interval: 1), output slice is produced monthly, and hello scheduler property for hello activity is also set toomonthly.</span></span> <span data-ttu-id="b38ab-261">Ustawienia Hello hello wyjściowego zestawu danych i harmonogram działania hello muszą być zgodne.</span><span class="sxs-lookup"><span data-stu-id="b38ab-261">hello settings for hello output dataset and hello activity scheduler must match.</span></span> <span data-ttu-id="b38ab-262">Wyjściowy zestaw danych jest obecnie, jakie dysków hello harmonogramu, dlatego należy utworzyć wyjściowy zestaw danych, nawet wtedy, gdy działanie hello nie generuje żadnego wyniku.</span><span class="sxs-lookup"><span data-stu-id="b38ab-262">Currently, output dataset is what drives hello schedule, so you must create an output dataset even if hello activity does not produce any output.</span></span> <span data-ttu-id="b38ab-263">Jeśli działanie hello nie przyjmuje żadnych danych, możesz pominąć tworzenie zestawu danych wejściowych hello.</span><span class="sxs-lookup"><span data-stu-id="b38ab-263">If hello activity doesn't take any input, you can skip creating hello input dataset.</span></span> <span data-ttu-id="b38ab-264">na końcu hello w tej sekcji opisano Hello właściwości używane w hello następującego formatu JSON.</span><span class="sxs-lookup"><span data-stu-id="b38ab-264">hello properties used in hello following JSON are explained at hello end of this section.</span></span>

1. <span data-ttu-id="b38ab-265">W hello **Edytor fabryki danych**, kliknij przycisk **wielokropek (...) Więcej poleceń** , a następnie kliknij przycisk **nowy potok**.</span><span class="sxs-lookup"><span data-stu-id="b38ab-265">In hello **Data Factory Editor**, click **Ellipsis (…) More commands** and then click **New pipeline**.</span></span>

    ![Przycisk nowy potok](./media/data-factory-build-your-first-pipeline-using-editor/new-pipeline-button.png)
2. <span data-ttu-id="b38ab-267">Skopiuj i Wklej powitania po fragment okna toohello projekt-1.</span><span class="sxs-lookup"><span data-stu-id="b38ab-267">Copy and paste hello following snippet toohello Draft-1 window.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="b38ab-268">Zastąp **storageaccountname** hello nazwą konta magazynu w hello JSON.</span><span class="sxs-lookup"><span data-stu-id="b38ab-268">Replace **storageaccountname** with hello name of your storage account in hello JSON.</span></span>
   >
   >

    ```JSON
    {
        "name": "MyFirstPipeline",
        "properties": {
            "description": "My first Azure Data Factory pipeline",
            "activities": [
                {
                    "type": "HDInsightHive",
                    "typeProperties": {
                        "scriptPath": "adfgetstarted/script/partitionweblogs.hql",
                        "scriptLinkedService": "AzureStorageLinkedService",
                        "defines": {
                            "inputtable": "wasb://adfgetstarted@<storageaccountname>.blob.core.windows.net/inputdata",
                            "partitionedtable": "wasb://adfgetstarted@<storageaccountname>.blob.core.windows.net/partitioneddata"
                        }
                    },
                    "inputs": [
                        {
                            "name": "AzureBlobInput"
                        }
                    ],
                    "outputs": [
                        {
                            "name": "AzureBlobOutput"
                        }
                    ],
                    "policy": {
                        "concurrency": 1,
                        "retry": 3
                    },
                    "scheduler": {
                        "frequency": "Month",
                        "interval": 1
                    },
                    "name": "RunSampleHiveActivity",
                    "linkedServiceName": "HDInsightOnDemandLinkedService"
                }
            ],
            "start": "2017-07-01T00:00:00Z",
            "end": "2017-07-02T00:00:00Z",
            "isPaused": false
        }
    }
    ```

    <span data-ttu-id="b38ab-269">We fragmencie JSON hello tworzysz potok, który składa się z jednego działania używającej tooprocess Hive danych w klastrze usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b38ab-269">In hello JSON snippet, you are creating a pipeline that consists of a single activity that uses Hive tooprocess Data on an HDInsight cluster.</span></span>

    <span data-ttu-id="b38ab-270">plik skryptu Hive Hello, **partitionweblogs.hql**, są przechowywane w hello kontem magazynu platformy Azure (określonego przez element scriptLinkedService hello, nazywany **AzureStorageLinkedService**) i w  **skrypt** folderu w kontenerze hello **adfgetstarted**.</span><span class="sxs-lookup"><span data-stu-id="b38ab-270">hello Hive script file, **partitionweblogs.hql**, is stored in hello Azure storage account (specified by hello scriptLinkedService, called **AzureStorageLinkedService**), and in **script** folder in hello container **adfgetstarted**.</span></span>

    <span data-ttu-id="b38ab-271">Witaj **definiuje** sekcja jest używane toospecify hello środowiska uruchomieniowego ustawień, które są przekazywane skryptu hive toohello jako wartości konfiguracji gałęzi (np. ${hiveconf: inputtable}, {hiveconf:partitionedtable} $).</span><span class="sxs-lookup"><span data-stu-id="b38ab-271">hello **defines** section is used toospecify hello runtime settings that are passed toohello hive script as Hive configuration values (e.g ${hiveconf:inputtable}, ${hiveconf:partitionedtable}).</span></span>

    <span data-ttu-id="b38ab-272">Witaj **start** i **zakończenia** hello aktywny okres potoku hello określa właściwości hello potoku.</span><span class="sxs-lookup"><span data-stu-id="b38ab-272">hello **start** and **end** properties of hello pipeline specifies hello active period of hello pipeline.</span></span>

    <span data-ttu-id="b38ab-273">W działaniu hello JSON, możesz określić, tego skryptu Hive hello zostanie uruchomiona na określony przez hello obliczeń hello **linkedServiceName** — **HDInsightOnDemandLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="b38ab-273">In hello activity JSON, you specify that hello Hive script runs on hello compute specified by hello **linkedServiceName** – **HDInsightOnDemandLinkedService**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="b38ab-274">Zobacz sekcję "JSON potoku" w [potoki i działań w fabryce danych Azure](data-factory-create-pipelines.md) szczegółowe informacje na temat właściwości JSON używane w przykładzie hello.</span><span class="sxs-lookup"><span data-stu-id="b38ab-274">See "Pipeline JSON" in [Pipelines and activities in Azure Data Factory](data-factory-create-pipelines.md) for details about JSON properties used in hello example.</span></span>
   >
   >
3. <span data-ttu-id="b38ab-275">Potwierdź hello następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="b38ab-275">Confirm hello following:</span></span>

   1. <span data-ttu-id="b38ab-276">**Input.log** plik istnieje w hello **inputdata** folderu hello **adfgetstarted** kontenera w hello magazynu obiektów blob platformy Azure</span><span class="sxs-lookup"><span data-stu-id="b38ab-276">**input.log** file exists in hello **inputdata** folder of hello **adfgetstarted** container in hello Azure blob storage</span></span>
   2. <span data-ttu-id="b38ab-277">**partitionweblogs.hql** plik istnieje w hello **skryptu** folderu hello **adfgetstarted** kontenera w hello magazynu obiektów blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="b38ab-277">**partitionweblogs.hql** file exists in hello **script** folder of hello **adfgetstarted** container in hello Azure blob storage.</span></span> <span data-ttu-id="b38ab-278">Wstępny pełny hello etapami hello [— samouczek Przegląd](data-factory-build-your-first-pipeline.md) Jeśli nie widzisz tych plików.</span><span class="sxs-lookup"><span data-stu-id="b38ab-278">Complete hello prerequisite steps in hello [Tutorial Overview](data-factory-build-your-first-pipeline.md) if you don't see these files.</span></span>
   3. <span data-ttu-id="b38ab-279">Upewnij się, że zastąpione **storageaccountname** hello nazwą konta magazynu w hello potoku JSON.</span><span class="sxs-lookup"><span data-stu-id="b38ab-279">Confirm that you replaced **storageaccountname** with hello name of your storage account in hello pipeline JSON.</span></span>
4. <span data-ttu-id="b38ab-280">Kliknij przycisk **Wdróż** na pasku toodeploy hello potoku poleceń hello.</span><span class="sxs-lookup"><span data-stu-id="b38ab-280">Click **Deploy** on hello command bar toodeploy hello pipeline.</span></span> <span data-ttu-id="b38ab-281">Ponieważ hello **start** i **zakończenia** czasy są ustawiane w przeszłości hello i **isPaused** jest zestaw toofalse, potoku hello (działania w potoku hello) uruchamia natychmiast po wdrożeniu.</span><span class="sxs-lookup"><span data-stu-id="b38ab-281">Since hello **start** and **end** times are set in hello past and **isPaused** is set toofalse, hello pipeline (activity in hello pipeline) runs immediately after you deploy.</span></span>
5. <span data-ttu-id="b38ab-282">Upewnij się, że potoku hello w widoku drzewa hello jest wyświetlany.</span><span class="sxs-lookup"><span data-stu-id="b38ab-282">Confirm that you see hello pipeline in hello tree view.</span></span>

    ![Widok drzewa z potokiem](./media/data-factory-build-your-first-pipeline-using-editor/tree-view-pipeline.png)
6. <span data-ttu-id="b38ab-284">Gratulacje! Udało Ci się utworzyć pierwszy potok!</span><span class="sxs-lookup"><span data-stu-id="b38ab-284">Congratulations, you have successfully created your first pipeline!</span></span>

## <a name="monitor-pipeline"></a><span data-ttu-id="b38ab-285">Monitorowanie potoku</span><span class="sxs-lookup"><span data-stu-id="b38ab-285">Monitor pipeline</span></span>
### <a name="monitor-pipeline-using-diagram-view"></a><span data-ttu-id="b38ab-286">Monitorowanie potoku przy użyciu widoku diagramu</span><span class="sxs-lookup"><span data-stu-id="b38ab-286">Monitor pipeline using Diagram View</span></span>
1. <span data-ttu-id="b38ab-287">Kliknij przycisk **X** tooclose Edytor fabryki danych bloków toonavigate kopii toohello bloku fabryki danych i kliknij przycisk **Diagram**.</span><span class="sxs-lookup"><span data-stu-id="b38ab-287">Click **X** tooclose Data Factory Editor blades and toonavigate back toohello Data Factory blade, and click **Diagram**.</span></span>

    ![Kafelek Diagram](./media/data-factory-build-your-first-pipeline-using-editor/diagram-tile.png)
2. <span data-ttu-id="b38ab-289">W widoku diagramu hello zapoznać się z omówieniem potoki hello i zestawów danych użytych w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="b38ab-289">In hello Diagram View, you see an overview of hello pipelines, and datasets used in this tutorial.</span></span>

    ![Widok diagramu](./media/data-factory-build-your-first-pipeline-using-editor/diagram-view-2.png)
3. <span data-ttu-id="b38ab-291">tooview wszystkie działania w potoku hello, kliknij prawym przyciskiem myszy potoku w hello diagram i kliknij przycisk Otwórz potoku.</span><span class="sxs-lookup"><span data-stu-id="b38ab-291">tooview all activities in hello pipeline, right-click pipeline in hello diagram and click Open Pipeline.</span></span>

    ![Menu Otwórz potok](./media/data-factory-build-your-first-pipeline-using-editor/open-pipeline-menu.png)
4. <span data-ttu-id="b38ab-293">Upewnij się, że widoczny hello HDInsightHive działania w potoku hello.</span><span class="sxs-lookup"><span data-stu-id="b38ab-293">Confirm that you see hello HDInsightHive activity in hello pipeline.</span></span>

    ![Widok Otwórz potok](./media/data-factory-build-your-first-pipeline-using-editor/open-pipeline-view.png)

    <span data-ttu-id="b38ab-295">toonavigate kopii toohello poprzedni widok, kliknij przycisk **fabryki danych** hello nawigacją menu u góry hello.</span><span class="sxs-lookup"><span data-stu-id="b38ab-295">toonavigate back toohello previous view, click **Data factory** in hello breadcrumb menu at hello top.</span></span>
5. <span data-ttu-id="b38ab-296">W hello **widoku diagramu**, kliknij dwukrotnie plik zestawu danych hello **AzureBlobInput**.</span><span class="sxs-lookup"><span data-stu-id="b38ab-296">In hello **Diagram View**, double-click hello dataset **AzureBlobInput**.</span></span> <span data-ttu-id="b38ab-297">Upewnij się, że wycinek hello jest w **gotowe** stanu.</span><span class="sxs-lookup"><span data-stu-id="b38ab-297">Confirm that hello slice is in **Ready** state.</span></span> <span data-ttu-id="b38ab-298">Może potrwać kilka minut dla tooshow wycinka hello w stanie gotowe.</span><span class="sxs-lookup"><span data-stu-id="b38ab-298">It may take a couple of minutes for hello slice tooshow up in Ready state.</span></span> <span data-ttu-id="b38ab-299">Jeśli nie następuje po poczekaj przez pewien czas, zobacz, jeśli masz pliku wejściowego hello (input.log) umieszczone w prawo kontenera hello (adfgetstarted) i folderu (inputdata).</span><span class="sxs-lookup"><span data-stu-id="b38ab-299">If it does not happen after you wait for sometime, see if you have hello input file (input.log) placed in hello right container (adfgetstarted) and folder (inputdata).</span></span>

   ![Wycinek danych wejściowych w stanie gotowości](./media/data-factory-build-your-first-pipeline-using-editor/input-slice-ready.png)
6. <span data-ttu-id="b38ab-301">Kliknij przycisk **X** tooclose **AzureBlobInput** bloku.</span><span class="sxs-lookup"><span data-stu-id="b38ab-301">Click **X** tooclose **AzureBlobInput** blade.</span></span>
7. <span data-ttu-id="b38ab-302">W hello **widoku diagramu**, kliknij dwukrotnie plik zestawu danych hello **AzureBlobOutput**.</span><span class="sxs-lookup"><span data-stu-id="b38ab-302">In hello **Diagram View**, double-click hello dataset **AzureBlobOutput**.</span></span> <span data-ttu-id="b38ab-303">Użytkownik widzi tego hello wycinek, który jest obecnie przetwarzane.</span><span class="sxs-lookup"><span data-stu-id="b38ab-303">You see that hello slice that is currently being processed.</span></span>

   ![Zestaw danych](./media/data-factory-build-your-first-pipeline-using-editor/dataset-blade.png)
8. <span data-ttu-id="b38ab-305">Po zakończeniu przetwarzania zostanie wyświetlony wycinek hello **gotowe** stanu.</span><span class="sxs-lookup"><span data-stu-id="b38ab-305">When processing is done, you see hello slice in **Ready** state.</span></span>

   ![Zestaw danych](./media/data-factory-build-your-first-pipeline-using-editor/dataset-slice-ready.png)  

   > [!IMPORTANT]
   > <span data-ttu-id="b38ab-307">Tworzenie klastra usługi HDInsight na żądanie zwykle trwa trochę czasu (około 20 minut).</span><span class="sxs-lookup"><span data-stu-id="b38ab-307">Creation of an on-demand HDInsight cluster usually takes sometime (approximately 20 minutes).</span></span> <span data-ttu-id="b38ab-308">W związku z tym spodziewać się potoku hello trwać zbyt **około 30 minut** tooprocess hello wycinka.</span><span class="sxs-lookup"><span data-stu-id="b38ab-308">Therefore, expect hello pipeline too      take **approximately 30 minutes** tooprocess hello slice.</span></span>
   >
   >

9. <span data-ttu-id="b38ab-309">Gdy wycinek hello jest **gotowe** stanu, należy sprawdzić hello **partitioneddata** folderu w hello **adfgetstarted** kontenera w magazynie obiektów blob na powitania dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="b38ab-309">When hello slice is in **Ready** state, check hello **partitioneddata** folder in hello **adfgetstarted** container in your blob storage for hello output data.</span></span>  

   ![Dane wyjściowe](./media/data-factory-build-your-first-pipeline-using-editor/three-ouptut-files.png)
10. <span data-ttu-id="b38ab-311">Kliknij przycisk Szczegóły toosee wycinka hello o nim w **wycinka danych** bloku.</span><span class="sxs-lookup"><span data-stu-id="b38ab-311">Click hello slice toosee details about it in a **Data slice** blade.</span></span>

   ![Szczegóły wycinka danych](./media/data-factory-build-your-first-pipeline-using-editor/data-slice-details.png)  
11. <span data-ttu-id="b38ab-313">Kliknij przycisk uruchamiania w hello działania **listy odbywa się działanie** toosee szczegółowe informacje o działaniu można uruchomić (działanie gałęzi w naszym scenariuszu) w **szczegóły uruchomienia działania** okna.</span><span class="sxs-lookup"><span data-stu-id="b38ab-313">Click an activity run in hello **Activity runs list** toosee details about an activity run (Hive activity in our scenario) in an **Activity run details** window.</span></span>   

   ![Szczegóły uruchamiania działania](./media/data-factory-build-your-first-pipeline-using-editor/activity-window-blade.png)    

   <span data-ttu-id="b38ab-315">Z plików dziennika hello widać, zapytanie Hive hello, które zostało wykonane i informacje o stanie.</span><span class="sxs-lookup"><span data-stu-id="b38ab-315">From hello log files, you can see hello Hive query that was executed and status information.</span></span> <span data-ttu-id="b38ab-316">Dzienniki te są przydatne w przypadku rozwiązywania różnych problemów.</span><span class="sxs-lookup"><span data-stu-id="b38ab-316">These logs are useful for troubleshooting any issues.</span></span>
   <span data-ttu-id="b38ab-317">Więcej szczegółowych informacji znajduje się w artykule [Monitor and manage pipelines using Azure portal blades](data-factory-monitor-manage-pipelines.md) (Monitorowanie potoków i zarządzanie nimi przy użyciu bloków w witrynie Azure Portal).</span><span class="sxs-lookup"><span data-stu-id="b38ab-317">See [Monitor and manage pipelines using Azure portal blades](data-factory-monitor-manage-pipelines.md) article for more details.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b38ab-318">Plik wejściowy Hello zostaje usunięta, gdy hello wycinek jest przetwarzany pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="b38ab-318">hello input file gets deleted when hello slice is processed successfully.</span></span> <span data-ttu-id="b38ab-319">W związku z tym hello plik wejściowy (input.log) toohello inputdata folder kontenera adfgetstarted hello przekazywania wycinek hello toorerun lub Witaj ponownie samouczek.</span><span class="sxs-lookup"><span data-stu-id="b38ab-319">Therefore, if you want toorerun hello slice or do hello tutorial again, upload hello input file (input.log) toohello inputdata folder of hello adfgetstarted container.</span></span>
>
>

### <a name="monitor-pipeline-using-monitor--manage-app"></a><span data-ttu-id="b38ab-320">Monitorowanie potoku przy użyciu aplikacji Monitorowanie i zarządzanie</span><span class="sxs-lookup"><span data-stu-id="b38ab-320">Monitor pipeline using Monitor & Manage App</span></span>
<span data-ttu-id="b38ab-321">Można również użyć monitora i zarządzanie toomonitor aplikacji z potoków.</span><span class="sxs-lookup"><span data-stu-id="b38ab-321">You can also use Monitor & Manage application toomonitor your pipelines.</span></span> <span data-ttu-id="b38ab-322">Szczegółowe informacje dotyczące korzystania z aplikacji znajdują się w artykule [Monitor and manage Azure Data Factory pipelines using Monitoring and Management App](data-factory-monitor-manage-app.md) (Monitorowanie potoków usługi Azure Data Factory oraz zarządzanie nimi za pomocą aplikacji Monitorowanie i zarządzanie).</span><span class="sxs-lookup"><span data-stu-id="b38ab-322">For detailed information about using this application, see [Monitor and manage Azure Data Factory pipelines using Monitoring and Management App](data-factory-monitor-manage-app.md).</span></span>

1. <span data-ttu-id="b38ab-323">Kliknij przycisk **Monitor & Zarządzaj** kafelka na stronie głównej hello w fabryce danych.</span><span class="sxs-lookup"><span data-stu-id="b38ab-323">Click **Monitor & Manage** tile on hello home page for your data factory.</span></span>

    ![Kafelek Monitorowanie i zarządzanie](./media/data-factory-build-your-first-pipeline-using-editor/monitor-and-manage-tile.png)
2. <span data-ttu-id="b38ab-325">Powinna zostać wyświetlona **aplikacja Monitorowanie i zarządzanie**.</span><span class="sxs-lookup"><span data-stu-id="b38ab-325">You should see **Monitor & Manage application**.</span></span> <span data-ttu-id="b38ab-326">Zmień hello **godzina rozpoczęcia** i **czas zakończenia** toomatch start i end razy potoku sieci i kliknij **Zastosuj**.</span><span class="sxs-lookup"><span data-stu-id="b38ab-326">Change hello **Start time** and **End time** toomatch start and end times of your pipeline, and click **Apply**.</span></span>

    ![Aplikacja Monitorowanie i zarządzanie](./media/data-factory-build-your-first-pipeline-using-editor/monitor-and-manage-app.png)
3. <span data-ttu-id="b38ab-328">Wybierz przedział działania w hello **okien działania** listy toosee uzyskać szczegółowe informacje o nim.</span><span class="sxs-lookup"><span data-stu-id="b38ab-328">Select an activity window in hello **Activity Windows** list toosee details about it.</span></span>

    ![Szczegóły okna działania](./media/data-factory-build-your-first-pipeline-using-editor/activity-window-details.png)

## <a name="summary"></a><span data-ttu-id="b38ab-330">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="b38ab-330">Summary</span></span>
<span data-ttu-id="b38ab-331">W tym samouczku danych tooprocess fabryki danych Azure została utworzona przez uruchomienie skryptu Hive w klastrze HDInsight hadoop.</span><span class="sxs-lookup"><span data-stu-id="b38ab-331">In this tutorial, you created an Azure data factory tooprocess data by running Hive script on a HDInsight hadoop cluster.</span></span> <span data-ttu-id="b38ab-332">Użyto hello Edytor fabryki danych w hello Azure toodo portalu hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="b38ab-332">You used hello Data Factory Editor in hello Azure portal toodo hello following steps:</span></span>  

1. <span data-ttu-id="b38ab-333">Tworzenie **fabryki danych** Azure.</span><span class="sxs-lookup"><span data-stu-id="b38ab-333">Created an Azure **data factory**.</span></span>
2. <span data-ttu-id="b38ab-334">Utworzyć dwie **połączone usługi**:</span><span class="sxs-lookup"><span data-stu-id="b38ab-334">Created two **linked services**:</span></span>
   1. <span data-ttu-id="b38ab-335">**Usługa Azure Storage** połączone usługi toolink Twojego magazynu Azure blob storage przechowuje pliki danych wejściowych/wyjściowych toohello usługi fabryka danych.</span><span class="sxs-lookup"><span data-stu-id="b38ab-335">**Azure Storage** linked service toolink your Azure blob storage that holds input/output files toohello data factory.</span></span>
   2. <span data-ttu-id="b38ab-336">**Usługa Azure HDInsight** na żądanie połączone usługi toolink fabrykę danych toohello klastra usługi HDInsight Hadoop na żądanie.</span><span class="sxs-lookup"><span data-stu-id="b38ab-336">**Azure HDInsight** on-demand linked service toolink an on-demand HDInsight Hadoop cluster toohello data factory.</span></span> <span data-ttu-id="b38ab-337">Fabryka danych Azure tworzy HDInsight Hadoop dane wejściowe w czasie tooprocess klastra i danych wyjściowych produktu.</span><span class="sxs-lookup"><span data-stu-id="b38ab-337">Azure Data Factory creates a HDInsight Hadoop cluster just-in-time tooprocess input data and produce output data.</span></span>
3. <span data-ttu-id="b38ab-338">Utworzone dwie **zestawów danych**, które opisują danych wejściowych i wyjściowych dla działania HDInsight Hive w potoku hello.</span><span class="sxs-lookup"><span data-stu-id="b38ab-338">Created two **datasets**, which describe input and output data for HDInsight Hive activity in hello pipeline.</span></span>
4. <span data-ttu-id="b38ab-339">Utworzyć **potok** za pomocą działania **programu Hive w usłudze HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="b38ab-339">Created a **pipeline** with a **HDInsight Hive** activity.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b38ab-340">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b38ab-340">Next Steps</span></span>
<span data-ttu-id="b38ab-341">W tym artykule opisano tworzenie potoku za pomocą działania przekształcenia (działanie usługi HDInsight), które uruchamia skrypt programu Hive w klastrze usługi HDInsight na żądanie.</span><span class="sxs-lookup"><span data-stu-id="b38ab-341">In this article, you have created a pipeline with a transformation activity (HDInsight Activity) that runs a Hive script on an on-demand HDInsight cluster.</span></span> <span data-ttu-id="b38ab-342">toosee toouse toocopy działanie kopiowania danych z tooAzure obiektów Blob platformy Azure SQL, zobacz temat [samouczek: kopiowanie danych z tooAzure obiektów blob platformy Azure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="b38ab-342">toosee how toouse a Copy Activity toocopy data from an Azure Blob tooAzure SQL, see [Tutorial: Copy data from an Azure blob tooAzure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="b38ab-343">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="b38ab-343">See Also</span></span>
| <span data-ttu-id="b38ab-344">Temat</span><span class="sxs-lookup"><span data-stu-id="b38ab-344">Topic</span></span> | <span data-ttu-id="b38ab-345">Opis</span><span class="sxs-lookup"><span data-stu-id="b38ab-345">Description</span></span> |
|:--- |:--- |
| [<span data-ttu-id="b38ab-346">Potoki</span><span class="sxs-lookup"><span data-stu-id="b38ab-346">Pipelines</span></span>](data-factory-create-pipelines.md) |<span data-ttu-id="b38ab-347">Ten artykuł pomaga w zrozumieniu potoki i działań w fabryce danych Azure i w jaki sposób toouse ich tooconstruct end-to-end danymi przepływy pracy dla Twojego scenariusza lub firmy.</span><span class="sxs-lookup"><span data-stu-id="b38ab-347">This article helps you understand pipelines and activities in Azure Data Factory and how toouse them tooconstruct end-to-end data-driven workflows for your scenario or business.</span></span> |
| [<span data-ttu-id="b38ab-348">Zestawy danych</span><span class="sxs-lookup"><span data-stu-id="b38ab-348">Datasets</span></span>](data-factory-create-datasets.md) |<span data-ttu-id="b38ab-349">Ten artykuł ułatwia zapoznanie się z zestawami danych w usłudze Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="b38ab-349">This article helps you understand datasets in Azure Data Factory.</span></span> |
| [<span data-ttu-id="b38ab-350">Planowanie i wykonywanie</span><span class="sxs-lookup"><span data-stu-id="b38ab-350">Scheduling and execution</span></span>](data-factory-scheduling-and-execution.md) |<span data-ttu-id="b38ab-351">W tym artykule opisano aspekty planowania i wykonywania hello modelu aplikacji fabryki danych Azure.</span><span class="sxs-lookup"><span data-stu-id="b38ab-351">This article explains hello scheduling and execution aspects of Azure Data Factory application model.</span></span> |
| [<span data-ttu-id="b38ab-352">Monitorowanie potoków i zarządzanie nimi za pomocą aplikacji do monitorowania</span><span class="sxs-lookup"><span data-stu-id="b38ab-352">Monitor and manage pipelines using Monitoring App</span></span>](data-factory-monitor-manage-app.md) |<span data-ttu-id="b38ab-353">W tym artykule opisano sposób toomonitor, zarządzania i debugowania potoki przy użyciu hello monitorowanie & aplikacji do zarządzania.</span><span class="sxs-lookup"><span data-stu-id="b38ab-353">This article describes how toomonitor, manage, and debug pipelines using hello Monitoring & Management App.</span></span> |
