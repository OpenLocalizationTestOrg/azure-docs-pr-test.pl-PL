---
title: "Samouczek: tworzenie potoku za pomocą działania kopiowania przy użyciu programu Visual Studio | Microsoft Docs"
description: "Ten samouczek zawiera instrukcje tworzenia potoku usługi Azure Data Factory za pomocą działania kopiowania przy użyciu programu Visual Studio."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 1751185b-ce0a-4ab2-a9c3-e37b4d149ca3
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: d99d8875807bab41f5122ab95a09f83f82923529
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-create-a-pipeline-with-copy-activity-using-visual-studio"></a><span data-ttu-id="c83e9-103">Samouczek: tworzenie potoku za pomocą działania kopiowania przy użyciu programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c83e9-103">Tutorial: Create a pipeline with Copy Activity using Visual Studio</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c83e9-104">Przegląd i wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="c83e9-104">Overview and prerequisites</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [<span data-ttu-id="c83e9-105">Kreator kopiowania</span><span class="sxs-lookup"><span data-stu-id="c83e9-105">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
> * [<span data-ttu-id="c83e9-106">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="c83e9-106">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [<span data-ttu-id="c83e9-107">Program Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c83e9-107">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [<span data-ttu-id="c83e9-108">Program PowerShell</span><span class="sxs-lookup"><span data-stu-id="c83e9-108">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
> * [<span data-ttu-id="c83e9-109">Szablon usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c83e9-109">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [<span data-ttu-id="c83e9-110">Interfejs API REST</span><span class="sxs-lookup"><span data-stu-id="c83e9-110">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [<span data-ttu-id="c83e9-111">Interfejs API .NET</span><span class="sxs-lookup"><span data-stu-id="c83e9-111">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)
> 
> 

<span data-ttu-id="c83e9-112">W tym artykule dowiesz się, jak toouse hello toocreate programu Microsoft Visual Studio fabryki danych z potok, który kopiuje dane z bazy danych Azure SQL tooan magazynu obiektów blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c83e9-112">In this article, you learn how toouse hello Microsoft Visual Studio toocreate a data factory with a pipeline that copies data from an Azure blob storage tooan Azure SQL database.</span></span> <span data-ttu-id="c83e9-113">Jeśli nowy tooAzure fabryki danych, zapoznaj się z artykułem hello [tooAzure wprowadzenie fabryki danych](data-factory-introduction.md) artykuł przed wykonaniem tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="c83e9-113">If you are new tooAzure Data Factory, read through hello [Introduction tooAzure Data Factory](data-factory-introduction.md) article before doing this tutorial.</span></span>   

<span data-ttu-id="c83e9-114">W tym samouczku opisano tworzenie potoku z jednym działaniem (Działanie kopiowania).</span><span class="sxs-lookup"><span data-stu-id="c83e9-114">In this tutorial, you create a pipeline with one activity in it: Copy Activity.</span></span> <span data-ttu-id="c83e9-115">działanie kopiowania Hello kopiuje dane z magazynu danych obsługiwanych ujścia magazynu tooa obsługiwane dane.</span><span class="sxs-lookup"><span data-stu-id="c83e9-115">hello copy activity copies data from a supported data store tooa supported sink data store.</span></span> <span data-ttu-id="c83e9-116">Aby zapoznać się z listą magazynów danych obsługiwanych jako źródła i ujścia, zobacz [obsługiwane magazyny danych](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="c83e9-116">For a list of data stores supported as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="c83e9-117">działanie Hello jest obsługiwany przez ogólnie dostępna usługa, która można skopiować dane między różnych magazynach danych w sposób bezpieczny, niezawodny i skalowalności.</span><span class="sxs-lookup"><span data-stu-id="c83e9-117">hello activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="c83e9-118">Aby uzyskać więcej informacji na temat hello działanie kopiowania, zobacz [działań przepływu danych](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="c83e9-118">For more information about hello Copy Activity, see [Data Movement Activities](data-factory-data-movement-activities.md).</span></span>

<span data-ttu-id="c83e9-119">Potok może obejmować więcej niż jedno działanie.</span><span class="sxs-lookup"><span data-stu-id="c83e9-119">A pipeline can have more than one activity.</span></span> <span data-ttu-id="c83e9-120">I tworzenia łańcucha dwa działania (Uruchom jedno działanie po drugim), ustawiając hello wyjściowy zestaw danych z jednego działania jako hello wejściowy zestaw danych z hello innych działań.</span><span class="sxs-lookup"><span data-stu-id="c83e9-120">And, you can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="c83e9-121">Aby uzyskać więcej informacji, zobacz sekcję dotyczącą [wielu działań w potoku](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span><span class="sxs-lookup"><span data-stu-id="c83e9-121">For more information, see [multiple activities in a pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span>

> [!NOTE] 
> <span data-ttu-id="c83e9-122">Witaj potoku danych w tym samouczku kopiuje dane z magazynu danych źródła danych magazynu tooa docelowego.</span><span class="sxs-lookup"><span data-stu-id="c83e9-122">hello data pipeline in this tutorial copies data from a source data store tooa destination data store.</span></span> <span data-ttu-id="c83e9-123">Samouczek na temat danych tootransform przy użyciu fabryki danych Azure, zobacz [samouczek: Tworzenie danych tootransform potoku, przy użyciu klastra usługi Hadoop](data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="c83e9-123">For a tutorial on how tootransform data using Azure Data Factory, see [Tutorial: Build a pipeline tootransform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c83e9-124">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="c83e9-124">Prerequisites</span></span>
1. <span data-ttu-id="c83e9-125">Zapoznaj się z artykułem [— samouczek Przegląd](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) artykułu i pełne hello **wymagań wstępnych** czynności.</span><span class="sxs-lookup"><span data-stu-id="c83e9-125">Read through [Tutorial Overview](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) article and complete hello **prerequisite** steps.</span></span>       
2. <span data-ttu-id="c83e9-126">toocreate wystąpienia fabryki danych, musi być członkiem hello [współautora fabryki danych](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) roli na poziomie grupy zasobów subskrypcji hello.</span><span class="sxs-lookup"><span data-stu-id="c83e9-126">toocreate Data Factory instances, you must be a member of hello [Data Factory Contributor](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) role at hello subscription/resource group level.</span></span>
3. <span data-ttu-id="c83e9-127">Musi mieć zainstalowane na komputerze następujące hello:</span><span class="sxs-lookup"><span data-stu-id="c83e9-127">You must have hello following installed on your computer:</span></span> 
   * <span data-ttu-id="c83e9-128">Visual Studio 2013 lub Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="c83e9-128">Visual Studio 2013 or Visual Studio 2015</span></span>
   * <span data-ttu-id="c83e9-129">Pobierz zestaw Azure SDK dla programu Visual Studio 2013 lub Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="c83e9-129">Download Azure SDK for Visual Studio 2013 or Visual Studio 2015.</span></span> <span data-ttu-id="c83e9-130">Przejdź za[strony pobierania Azure](https://azure.microsoft.com/downloads/) i kliknij przycisk **VS 2013** lub **VS 2015** w hello **.NET** sekcji.</span><span class="sxs-lookup"><span data-stu-id="c83e9-130">Navigate too[Azure Download Page](https://azure.microsoft.com/downloads/) and click **VS 2013** or **VS 2015** in hello **.NET** section.</span></span>
   * <span data-ttu-id="c83e9-131">Pobierz najnowszy dodatek fabryki danych Azure hello for Visual Studio: [VS 2013](https://visualstudiogallery.msdn.microsoft.com/754d998c-8f92-4aa7-835b-e89c8c954aa5) lub [VS 2015](https://visualstudiogallery.msdn.microsoft.com/371a4cf9-0093-40fa-b7dd-be3c74f49005).</span><span class="sxs-lookup"><span data-stu-id="c83e9-131">Download hello latest Azure Data Factory plugin for Visual Studio: [VS 2013](https://visualstudiogallery.msdn.microsoft.com/754d998c-8f92-4aa7-835b-e89c8c954aa5) or [VS 2015](https://visualstudiogallery.msdn.microsoft.com/371a4cf9-0093-40fa-b7dd-be3c74f49005).</span></span> <span data-ttu-id="c83e9-132">Można także zaktualizować hello wtyczki, wykonując następujące kroki hello: polecenie hello menu **narzędzia** -> **rozszerzenia i aktualizacje** -> **Online**  ->  **Galerii programu visual Studio** -> **narzędzia fabryki danych Microsoft Azure dla programu Visual Studio** -> **aktualizacji**.</span><span class="sxs-lookup"><span data-stu-id="c83e9-132">You can also update hello plugin by doing hello following steps: On hello menu, click **Tools** -> **Extensions and Updates** -> **Online** -> **Visual Studio Gallery** -> **Microsoft Azure Data Factory Tools for Visual Studio** -> **Update**.</span></span>

## <a name="steps"></a><span data-ttu-id="c83e9-133">Kroki</span><span class="sxs-lookup"><span data-stu-id="c83e9-133">Steps</span></span>
<span data-ttu-id="c83e9-134">Poniżej przedstawiono kroki hello, które należy wykonać w ramach tego samouczka:</span><span class="sxs-lookup"><span data-stu-id="c83e9-134">Here are hello steps you perform as part of this tutorial:</span></span>

1. <span data-ttu-id="c83e9-135">Utwórz **połączone usługi** w fabryce danych hello.</span><span class="sxs-lookup"><span data-stu-id="c83e9-135">Create **linked services** in hello data factory.</span></span> <span data-ttu-id="c83e9-136">Ten krok polega na utworzeniu dwóch połączonych usług: Azure Storage i Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="c83e9-136">In this step, you create two linked services of types: Azure Storage and Azure SQL Database.</span></span> 
    
    <span data-ttu-id="c83e9-137">Witaj AzureStorageLinkedService łączy fabrykę danych toohello konta magazynu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c83e9-137">hello AzureStorageLinkedService links your Azure storage account toohello data factory.</span></span> <span data-ttu-id="c83e9-138">Utworzono kontener i przekazany w ramach konta magazynu danych toothis [wymagania wstępne](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="c83e9-138">You created a container and uploaded data toothis storage account as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>   

    <span data-ttu-id="c83e9-139">AzureSqlLinkedService łączy fabrykę danych toohello bazy danych Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="c83e9-139">AzureSqlLinkedService links your Azure SQL database toohello data factory.</span></span> <span data-ttu-id="c83e9-140">dane Hello, który jest skopiowany z magazynu obiektów blob hello są przechowywane w tej bazie danych.</span><span class="sxs-lookup"><span data-stu-id="c83e9-140">hello data that is copied from hello blob storage is stored in this database.</span></span> <span data-ttu-id="c83e9-141">W ramach [wymagań wstępnych](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) w tej bazie danych została utworzona tabela SQL.</span><span class="sxs-lookup"><span data-stu-id="c83e9-141">You created a SQL table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>     
2. <span data-ttu-id="c83e9-142">Utwórz dane wejściowe i wyjściowe **zestawów danych** w fabryce danych hello.</span><span class="sxs-lookup"><span data-stu-id="c83e9-142">Create input and output **datasets** in hello data factory.</span></span>  
    
    <span data-ttu-id="c83e9-143">Hello Azure połączoną usługą magazynu określa parametry połączenia hello, która używa usługi fabryka danych w czasie wykonywania tooconnect tooyour kontem magazynu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c83e9-143">hello Azure storage linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="c83e9-144">I zestawu danych wejściowych obiektu blob hello określa hello kontenera i folderu hello, który zawiera hello danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="c83e9-144">And, hello input blob dataset specifies hello container and hello folder that contains hello input data.</span></span>  

    <span data-ttu-id="c83e9-145">Podobnie hello usługi baza danych SQL Azure połączone określa hello parametry połączenia, które korzysta z usługi fabryka danych w czasie wykonywania tooconnect tooyour — bazy danych Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="c83e9-145">Similarly, hello Azure SQL Database linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure SQL database.</span></span> <span data-ttu-id="c83e9-146">I tabeli hello hello bazy danych toowhich hello danych z magazynu obiektów blob hello jest kopiowany określa hello danych wyjściowych SQL tabeli dataset.</span><span class="sxs-lookup"><span data-stu-id="c83e9-146">And, hello output SQL table dataset specifies hello table in hello database toowhich hello data from hello blob storage is copied.</span></span>
3. <span data-ttu-id="c83e9-147">Utwórz **potoku** w fabryce danych hello.</span><span class="sxs-lookup"><span data-stu-id="c83e9-147">Create a **pipeline** in hello data factory.</span></span> <span data-ttu-id="c83e9-148">W tym kroku jest tworzony potok za pomocą działania kopiowania.</span><span class="sxs-lookup"><span data-stu-id="c83e9-148">In this step, you create a pipeline with a copy activity.</span></span>   
    
    <span data-ttu-id="c83e9-149">działanie kopiowania Hello kopiuje dane z obiektu blob w tabeli tooa magazynu obiektów blob platformy Azure hello w bazie danych Azure SQL hello.</span><span class="sxs-lookup"><span data-stu-id="c83e9-149">hello copy activity copies data from a blob in hello Azure blob storage tooa table in hello Azure SQL database.</span></span> <span data-ttu-id="c83e9-150">Działanie kopiowania służy w potoku danych toocopy z dowolnego miejsca docelowego tooany obsługiwane obsługiwanej źródłowej.</span><span class="sxs-lookup"><span data-stu-id="c83e9-150">You can use a copy activity in a pipeline toocopy data from any supported source tooany supported destination.</span></span> <span data-ttu-id="c83e9-151">Listę obsługiwanych magazynów danych można znaleźć w artykule [Działania związane z przenoszeniem danych](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="c83e9-151">For a list of supported data stores, see [data movement activities](data-factory-data-movement-activities.md#supported-data-stores-and-formats) article.</span></span> 
4. <span data-ttu-id="c83e9-152">Utworzenie **fabryki danych** Azure podczas wdrażania jednostek usługi Data Factory (połączone usługi, zestawy danych/tabele i potoki).</span><span class="sxs-lookup"><span data-stu-id="c83e9-152">Create an Azure **data factory** when deploying Data Factory entities (linked services, datasets/tables, and pipelines).</span></span> 

## <a name="create-visual-studio-project"></a><span data-ttu-id="c83e9-153">Tworzenie projektu programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c83e9-153">Create Visual Studio project</span></span>
1. <span data-ttu-id="c83e9-154">Uruchom program **Visual Studio 2015**.</span><span class="sxs-lookup"><span data-stu-id="c83e9-154">Launch **Visual Studio 2015**.</span></span> <span data-ttu-id="c83e9-155">Kliknij przycisk **pliku**, punktu zbyt**nowy**i kliknij przycisk **projektu**.</span><span class="sxs-lookup"><span data-stu-id="c83e9-155">Click **File**, point too**New**, and click **Project**.</span></span> <span data-ttu-id="c83e9-156">Powinny pojawić się hello **nowy projekt** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="c83e9-156">You should see hello **New Project** dialog box.</span></span>  
2. <span data-ttu-id="c83e9-157">W hello **nowy projekt** okno dialogowe, wybierz opcję hello **DataFactory** szablonu, a następnie kliknij przycisk **pusty projekt fabryki danych**.</span><span class="sxs-lookup"><span data-stu-id="c83e9-157">In hello **New Project** dialog, select hello **DataFactory** template, and click **Empty Data Factory Project**.</span></span>  
   
    ![Okno dialogowe Nowy projekt](./media/data-factory-copy-activity-tutorial-using-visual-studio/new-project-dialog.png)
3. <span data-ttu-id="c83e9-159">Określ nazwę hello hello projektu, lokalizacji dla rozwiązania hello i hello rozwiązania, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="c83e9-159">Specify hello name of hello project, location for hello solution, and name of hello solution, and then click **OK**.</span></span>
   
    ![Eksplorator rozwiązań](./media/data-factory-copy-activity-tutorial-using-visual-studio/solution-explorer.png)    

## <a name="create-linked-services"></a><span data-ttu-id="c83e9-161">Tworzenie połączonych usług</span><span class="sxs-lookup"><span data-stu-id="c83e9-161">Create linked services</span></span>
<span data-ttu-id="c83e9-162">Połączone usługi są tworzone w toolink fabryki danych dane są przechowywane i obliczeniowe fabryki danych toohello usług.</span><span class="sxs-lookup"><span data-stu-id="c83e9-162">You create linked services in a data factory toolink your data stores and compute services toohello data factory.</span></span> <span data-ttu-id="c83e9-163">W tym samouczku nie przedstawiono korzystania z żadnych usług obliczeniowych, takich jak Azure HDInsight czy Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="c83e9-163">In this tutorial, you don't use any compute service such as Azure HDInsight or Azure Data Lake Analytics.</span></span> <span data-ttu-id="c83e9-164">Zostają użyte dwa magazyny danych typu Azure Storage (źródło) i Azure SQL Database (lokalizacja docelowa).</span><span class="sxs-lookup"><span data-stu-id="c83e9-164">You use two data stores of type Azure Storage (source) and Azure SQL Database (destination).</span></span> 

<span data-ttu-id="c83e9-165">Tak więc tworzy się dwie połączone usługi: AzureStorage i AzureSqlDatabase.</span><span class="sxs-lookup"><span data-stu-id="c83e9-165">Therefore, you create two linked services of types: AzureStorage and AzureSqlDatabase.</span></span>  

<span data-ttu-id="c83e9-166">Hello Azure Storage połączone usługi łączy fabrykę danych toohello konta magazynu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c83e9-166">hello Azure Storage linked service links your Azure storage account toohello data factory.</span></span> <span data-ttu-id="c83e9-167">To konto magazynu jest hello jedną w którym utworzono kontener i hello dane przekazane jako część [wymagania wstępne](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="c83e9-167">This storage account is hello one in which you created a container and uploaded hello data as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>   

<span data-ttu-id="c83e9-168">Azure SQL połączone usługi łączy fabrykę danych toohello bazy danych Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="c83e9-168">Azure SQL linked service links your Azure SQL database toohello data factory.</span></span> <span data-ttu-id="c83e9-169">dane Hello, który jest skopiowany z magazynu obiektów blob hello są przechowywane w tej bazie danych.</span><span class="sxs-lookup"><span data-stu-id="c83e9-169">hello data that is copied from hello blob storage is stored in this database.</span></span> <span data-ttu-id="c83e9-170">Utworzono hello pustych elementów tabeli w tej bazie danych jako część [wymagania wstępne](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="c83e9-170">You created hello emp table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>

<span data-ttu-id="c83e9-171">Połączone usługi łączenie magazyny danych lub obliczeniowe fabryki danych Azure tooan usług.</span><span class="sxs-lookup"><span data-stu-id="c83e9-171">Linked services link data stores or compute services tooan Azure data factory.</span></span> <span data-ttu-id="c83e9-172">Zobacz [obsługiwane magazyny danych](data-factory-data-movement-activities.md#supported-data-stores-and-formats) dla wszystkich hello źródeł i wychwytywanie obsługiwane przez hello działanie kopiowania.</span><span class="sxs-lookup"><span data-stu-id="c83e9-172">See [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) for all hello sources and sinks supported by hello Copy Activity.</span></span> <span data-ttu-id="c83e9-173">Zobacz [obliczeniowe połączonych usług](data-factory-compute-linked-services.md) hello lista usługi obliczeniowe obsługiwane przez fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="c83e9-173">See [compute linked services](data-factory-compute-linked-services.md) for hello list of compute services supported by Data Factory.</span></span> <span data-ttu-id="c83e9-174">Ten samouczek nie obejmuje używania żadnej usługi obliczeniowej.</span><span class="sxs-lookup"><span data-stu-id="c83e9-174">In this tutorial, you do not use any compute service.</span></span> 

### <a name="create-hello-azure-storage-linked-service"></a><span data-ttu-id="c83e9-175">Utwórz hello połączoną usługą magazynu Azure</span><span class="sxs-lookup"><span data-stu-id="c83e9-175">Create hello Azure Storage linked service</span></span>
1. <span data-ttu-id="c83e9-176">W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy **połączonych usług**, punktu zbyt**Dodaj**i kliknij przycisk **nowy element**.</span><span class="sxs-lookup"><span data-stu-id="c83e9-176">In **Solution Explorer**, right-click **Linked Services**, point too**Add**, and click **New Item**.</span></span>      
2. <span data-ttu-id="c83e9-177">W hello **Dodaj nowy element** okno dialogowe, wybierz opcję **połączonej usługi magazynu Azure** hello listy i kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="c83e9-177">In hello **Add New Item** dialog box, select **Azure Storage Linked Service** from hello list, and click **Add**.</span></span> 
   
    ![Nowa połączona usługa](./media/data-factory-copy-activity-tutorial-using-visual-studio/new-linked-service-dialog.png)
3. <span data-ttu-id="c83e9-179">Zastąp `<accountname>` i `<accountkey>`* hello nazwą konta magazynu Azure i klucza.</span><span class="sxs-lookup"><span data-stu-id="c83e9-179">Replace `<accountname>` and `<accountkey>`* with hello name of your Azure storage account and its key.</span></span> 
   
    ![Połączona usługa Azure Storage](./media/data-factory-copy-activity-tutorial-using-visual-studio/azure-storage-linked-service.png)
4. <span data-ttu-id="c83e9-181">Zapisz hello **AzureStorageLinkedService1.json** pliku.</span><span class="sxs-lookup"><span data-stu-id="c83e9-181">Save hello **AzureStorageLinkedService1.json** file.</span></span>

    <span data-ttu-id="c83e9-182">Aby uzyskać więcej informacji o właściwościach JSON w definicji usługi hello połączone, zobacz [łącznika usługi Azure Blob Storage](data-factory-azure-blob-connector.md#linked-service-properties) artykułu.</span><span class="sxs-lookup"><span data-stu-id="c83e9-182">For more information about JSON properties in hello linked service definition, see [Azure Blob Storage connector](data-factory-azure-blob-connector.md#linked-service-properties) article.</span></span>

### <a name="create-hello-azure-sql-linked-service"></a><span data-ttu-id="c83e9-183">Utwórz hello Azure połączoną usługą SQL</span><span class="sxs-lookup"><span data-stu-id="c83e9-183">Create hello Azure SQL linked service</span></span>
1. <span data-ttu-id="c83e9-184">Kliknij prawym przyciskiem myszy **połączonych usług** węzła w hello **Eksploratora rozwiązań** ponownie punktu zbyt**Dodaj**i kliknij przycisk **nowy element**.</span><span class="sxs-lookup"><span data-stu-id="c83e9-184">Right-click on **Linked Services** node in hello **Solution Explorer** again, point too**Add**, and click **New Item**.</span></span> 
2. <span data-ttu-id="c83e9-185">Tym razem wybierz pozycję **Połączona usługa SQL Azure** i kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="c83e9-185">This time, select **Azure SQL Linked Service**, and click **Add**.</span></span> 
3. <span data-ttu-id="c83e9-186">W hello **pliku AzureSqlLinkedService1.json**, Zastąp `<servername>`, `<databasename>`, `<username@servername>`, i `<password>` z nazwy serwera Azure SQL, bazy danych, konto użytkownika i hasło.</span><span class="sxs-lookup"><span data-stu-id="c83e9-186">In hello **AzureSqlLinkedService1.json file**, replace `<servername>`, `<databasename>`, `<username@servername>`, and `<password>` with names of your Azure SQL server, database, user account, and password.</span></span>    
4. <span data-ttu-id="c83e9-187">Zapisz hello **AzureSqlLinkedService1.json** pliku.</span><span class="sxs-lookup"><span data-stu-id="c83e9-187">Save hello **AzureSqlLinkedService1.json** file.</span></span> 
    
    <span data-ttu-id="c83e9-188">Aby uzyskać więcej informacji o tych właściwościach JSON, zobacz artykuł dotyczący [łącznika usługi Azure SQL Database](data-factory-azure-sql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="c83e9-188">For more information about these JSON properties, see [Azure SQL Database connector](data-factory-azure-sql-connector.md#linked-service-properties).</span></span>


## <a name="create-datasets"></a><span data-ttu-id="c83e9-189">Tworzenie zestawów danych</span><span class="sxs-lookup"><span data-stu-id="c83e9-189">Create datasets</span></span>
<span data-ttu-id="c83e9-190">W poprzednim kroku hello utworzono toolink połączone usługi konta magazynu Azure i fabryki danych tooyour bazy danych Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="c83e9-190">In hello previous step, you created linked services toolink your Azure Storage account and Azure SQL database tooyour data factory.</span></span> <span data-ttu-id="c83e9-191">W tym kroku należy zdefiniować dwa zestawy danych o nazwie InputDataset i OutputDataset reprezentujące danych wejściowych i wyjściowych danych przechowywanych w magazynach danych hello odwołuje się AzureStorageLinkedService1 i AzureSqlLinkedService1 odpowiednio.</span><span class="sxs-lookup"><span data-stu-id="c83e9-191">In this step, you define two datasets named InputDataset and OutputDataset that represent input and output data that is stored in hello data stores referred by AzureStorageLinkedService1 and AzureSqlLinkedService1 respectively.</span></span>

<span data-ttu-id="c83e9-192">Hello Azure połączoną usługą magazynu określa parametry połączenia hello, która używa usługi fabryka danych w czasie wykonywania tooconnect tooyour kontem magazynu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c83e9-192">hello Azure storage linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="c83e9-193">I zestawu danych wejściowych obiektu blob hello (InputDataset) określa hello kontenera i folderu hello, który zawiera hello danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="c83e9-193">And, hello input blob dataset (InputDataset) specifies hello container and hello folder that contains hello input data.</span></span>  

<span data-ttu-id="c83e9-194">Podobnie hello usługi baza danych SQL Azure połączone określa hello parametry połączenia, które korzysta z usługi fabryka danych w czasie wykonywania tooconnect tooyour — bazy danych Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="c83e9-194">Similarly, hello Azure SQL Database linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure SQL database.</span></span> <span data-ttu-id="c83e9-195">I hello danych wyjściowych SQL tabeli dataset (OututDataset) określa hello tabeli w hello bazy danych toowhich powitalne dane z magazynu obiektów blob hello są kopiowane.</span><span class="sxs-lookup"><span data-stu-id="c83e9-195">And, hello output SQL table dataset (OututDataset) specifies hello table in hello database toowhich hello data from hello blob storage is copied.</span></span> 

### <a name="create-input-dataset"></a><span data-ttu-id="c83e9-196">Tworzenie wejściowego zestawu danych</span><span class="sxs-lookup"><span data-stu-id="c83e9-196">Create input dataset</span></span>
<span data-ttu-id="c83e9-197">W tym kroku utworzysz zestaw danych o nazwie InputDataset, który wskazuje plik obiektu blob tooa (emp.txt) w folderze głównym hello kontenera obiektów blob (adftutorial) w hello reprezentowany przez hello AzureStorageLinkedService1 połączone usługi Magazyn Azure.</span><span class="sxs-lookup"><span data-stu-id="c83e9-197">In this step, you create a dataset named InputDataset that points tooa blob file (emp.txt) in hello root folder of a blob container (adftutorial) in hello Azure Storage represented by hello AzureStorageLinkedService1 linked service.</span></span> <span data-ttu-id="c83e9-198">Brak określić wartość dla nazwy pliku hello (lub Pomiń je), danych z wszystkich obiektów blob w folderze wejściowych hello są skopiowanych toohello docelowego.</span><span class="sxs-lookup"><span data-stu-id="c83e9-198">If you don't specify a value for hello fileName (or skip it), data from all blobs in hello input folder are copied toohello destination.</span></span> <span data-ttu-id="c83e9-199">W tym samouczku należy określić wartość dla hello fileName.</span><span class="sxs-lookup"><span data-stu-id="c83e9-199">In this tutorial, you specify a value for hello fileName.</span></span> 

<span data-ttu-id="c83e9-200">W tym miejscu możesz użyć hello termin "tabele" zamiast "zestawy danych".</span><span class="sxs-lookup"><span data-stu-id="c83e9-200">Here, you use hello term "tables" rather than "datasets".</span></span> <span data-ttu-id="c83e9-201">Tabela jest prostokątny zestawu danych i hello tylko typ zestawu danych obsługiwane w tej chwili.</span><span class="sxs-lookup"><span data-stu-id="c83e9-201">A table is a rectangular dataset and is hello only type of dataset supported right now.</span></span> 

1. <span data-ttu-id="c83e9-202">Kliknij prawym przyciskiem myszy **tabel** w hello **Eksploratora rozwiązań**, punktu zbyt**Dodaj**i kliknij przycisk **nowy element**.</span><span class="sxs-lookup"><span data-stu-id="c83e9-202">Right-click **Tables** in hello **Solution Explorer**, point too**Add**, and click **New Item**.</span></span>
2. <span data-ttu-id="c83e9-203">W hello **Dodaj nowy element** okno dialogowe, wybierz opcję **obiektów Blob platformy Azure**i kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="c83e9-203">In hello **Add New Item** dialog box, select **Azure Blob**, and click **Add**.</span></span>   
3. <span data-ttu-id="c83e9-204">Zamień tekst JSON hello hello następującego tekstu i Zapisz hello **AzureBlobLocation1.json** pliku.</span><span class="sxs-lookup"><span data-stu-id="c83e9-204">Replace hello JSON text with hello following text and save hello **AzureBlobLocation1.json** file.</span></span> 

  ```json   
  {
    "name": "InputDataset",
    "properties": {
      "structure": [
        {
          "name": "FirstName",
          "type": "String"
        },
        {
          "name": "LastName",
          "type": "String"
        }
      ],
      "type": "AzureBlob",
      "linkedServiceName": "AzureStorageLinkedService1",
      "typeProperties": {
        "folderPath": "adftutorial/",
        "format": {
          "type": "TextFormat",
          "columnDelimiter": ","
        }
      },
      "external": true,
      "availability": {
        "frequency": "Hour",
        "interval": 1
      }
    }
  }
  ``` 
    <span data-ttu-id="c83e9-205">Witaj Poniższa tabela zawiera opisy właściwości JSON hello używane we fragmencie hello:</span><span class="sxs-lookup"><span data-stu-id="c83e9-205">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

    | <span data-ttu-id="c83e9-206">Właściwość</span><span class="sxs-lookup"><span data-stu-id="c83e9-206">Property</span></span> | <span data-ttu-id="c83e9-207">Opis</span><span class="sxs-lookup"><span data-stu-id="c83e9-207">Description</span></span> |
    |:--- |:--- |
    | <span data-ttu-id="c83e9-208">type</span><span class="sxs-lookup"><span data-stu-id="c83e9-208">type</span></span> | <span data-ttu-id="c83e9-209">Właściwość type Hello ustawiono zbyt**AzureBlob** ponieważ danych znajduje się w magazynie obiektów blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c83e9-209">hello type property is set too**AzureBlob** because data resides in an Azure blob storage.</span></span> |
    | <span data-ttu-id="c83e9-210">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="c83e9-210">linkedServiceName</span></span> | <span data-ttu-id="c83e9-211">Odwołuje się toohello **AzureStorageLinkedService** utworzony wcześniej.</span><span class="sxs-lookup"><span data-stu-id="c83e9-211">Refers toohello **AzureStorageLinkedService** that you created earlier.</span></span> |
    | <span data-ttu-id="c83e9-212">folderPath</span><span class="sxs-lookup"><span data-stu-id="c83e9-212">folderPath</span></span> | <span data-ttu-id="c83e9-213">Określa obiekt blob hello **kontenera** i hello **folderu** zawiera obiekty BLOB wejściowego.</span><span class="sxs-lookup"><span data-stu-id="c83e9-213">Specifies hello blob **container** and hello **folder** that contains input blobs.</span></span> <span data-ttu-id="c83e9-214">W tym samouczku adftutorial jest hello kontenera obiektów blob i hello folderu głównego.</span><span class="sxs-lookup"><span data-stu-id="c83e9-214">In this tutorial, adftutorial is hello blob container and folder is hello root folder.</span></span> | 
    | <span data-ttu-id="c83e9-215">fileName</span><span class="sxs-lookup"><span data-stu-id="c83e9-215">fileName</span></span> | <span data-ttu-id="c83e9-216">Ta właściwość jest opcjonalna.</span><span class="sxs-lookup"><span data-stu-id="c83e9-216">This property is optional.</span></span> <span data-ttu-id="c83e9-217">W przypadku pominięcia tej właściwości, pobierane są wszystkie pliki z hello folderPath.</span><span class="sxs-lookup"><span data-stu-id="c83e9-217">If you omit this property, all files from hello folderPath are picked.</span></span> <span data-ttu-id="c83e9-218">W tym samouczku **emp.txt** określona dla hello nazwę pliku, tak aby plik zostaje pobrana do przetwarzania.</span><span class="sxs-lookup"><span data-stu-id="c83e9-218">In this tutorial, **emp.txt** is specified for hello fileName, so only that file is picked up for processing.</span></span> |
    | <span data-ttu-id="c83e9-219">format -> type</span><span class="sxs-lookup"><span data-stu-id="c83e9-219">format -> type</span></span> |<span data-ttu-id="c83e9-220">Plik wejściowy Hello jest w formacie tekstowym hello, więc używamy **TextFormat**.</span><span class="sxs-lookup"><span data-stu-id="c83e9-220">hello input file is in hello text format, so we use **TextFormat**.</span></span> |
    | <span data-ttu-id="c83e9-221">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="c83e9-221">columnDelimiter</span></span> | <span data-ttu-id="c83e9-222">Witaj kolumn w pliku wejściowym hello są rozdzielane **przecinka (`,`)**.</span><span class="sxs-lookup"><span data-stu-id="c83e9-222">hello columns in hello input file are delimited by **comma character (`,`)**.</span></span> |
    | <span data-ttu-id="c83e9-223">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="c83e9-223">frequency/interval</span></span> | <span data-ttu-id="c83e9-224">częstotliwość Hello ustawiono zbyt**godzina** i interwał jest ustawiany za**1**, co oznacza, że hello wejściowych dostępnych wycinków **co godzinę**.</span><span class="sxs-lookup"><span data-stu-id="c83e9-224">hello frequency is set too**Hour** and interval is  set too**1**, which means that hello input slices are available **hourly**.</span></span> <span data-ttu-id="c83e9-225">Innymi słowy, hello usługi fabryka danych sprawdza dane wejściowe co godzinę w folderze głównym hello kontenera obiektów blob (**adftutorial**) określone.</span><span class="sxs-lookup"><span data-stu-id="c83e9-225">In other words, hello Data Factory service looks for input data every hour in hello root folder of blob container (**adftutorial**) you specified.</span></span> <span data-ttu-id="c83e9-226">Wyszukuje hello danych w ramach hello potoku rozpoczęcia i zakończenia godzin, nie przed lub po tych godzinach.</span><span class="sxs-lookup"><span data-stu-id="c83e9-226">It looks for hello data within hello pipeline start and end times, not before or after these times.</span></span>  |
    | <span data-ttu-id="c83e9-227">external</span><span class="sxs-lookup"><span data-stu-id="c83e9-227">external</span></span> | <span data-ttu-id="c83e9-228">Ta właściwość jest ustawiona zbyt**true** czy hello danych nie jest generowany przez tego potoku.</span><span class="sxs-lookup"><span data-stu-id="c83e9-228">This property is set too**true** if hello data is not generated by this pipeline.</span></span> <span data-ttu-id="c83e9-229">Witaj danych wejściowych w tym samouczku jest hello emp.txt pliku, który nie jest generowany w tym potoku, możemy ustawić tootrue tej właściwości.</span><span class="sxs-lookup"><span data-stu-id="c83e9-229">hello input data in this tutorial is in hello emp.txt file, which is not generated by this pipeline, so we set this property tootrue.</span></span> |

    <span data-ttu-id="c83e9-230">Aby uzyskać więcej informacji o tych właściwościach JSON, zobacz [artykuł dotyczący łącznika obiektu blob platformy Azure](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="c83e9-230">For more information about these JSON properties, see [Azure Blob connector article](data-factory-azure-blob-connector.md#dataset-properties).</span></span>   

### <a name="create-output-dataset"></a><span data-ttu-id="c83e9-231">Tworzenie wyjściowego zestawu danych</span><span class="sxs-lookup"><span data-stu-id="c83e9-231">Create output dataset</span></span>
<span data-ttu-id="c83e9-232">W tym kroku tworzony jest wyjściowy zestaw danych o nazwie **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="c83e9-232">In this step, you create an output dataset named **OutputDataset**.</span></span> <span data-ttu-id="c83e9-233">Ten zestaw danych wskazuje tooa tabeli SQL w bazie danych Azure SQL hello reprezentowany przez **AzureSqlLinkedService1**.</span><span class="sxs-lookup"><span data-stu-id="c83e9-233">This dataset points tooa SQL table in hello Azure SQL database represented by **AzureSqlLinkedService1**.</span></span> 

1. <span data-ttu-id="c83e9-234">Kliknij prawym przyciskiem myszy **tabel** w hello **Eksploratora rozwiązań** ponownie punktu zbyt**Dodaj**i kliknij przycisk **nowy element**.</span><span class="sxs-lookup"><span data-stu-id="c83e9-234">Right-click **Tables** in hello **Solution Explorer** again, point too**Add**, and click **New Item**.</span></span>
2. <span data-ttu-id="c83e9-235">W hello **Dodaj nowy element** okno dialogowe, wybierz opcję **Azure SQL**i kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="c83e9-235">In hello **Add New Item** dialog box, select **Azure SQL**, and click **Add**.</span></span> 
3. <span data-ttu-id="c83e9-236">Zamień tekst JSON hello hello następującego formatu JSON i Zapisz hello **AzureSqlTableLocation1.json** pliku.</span><span class="sxs-lookup"><span data-stu-id="c83e9-236">Replace hello JSON text with hello following JSON and save hello **AzureSqlTableLocation1.json** file.</span></span>

  ```json
    {
     "name": "OutputDataset",
     "properties": {
       "structure": [
         {
           "name": "FirstName",
           "type": "String"
         },
         {
           "name": "LastName",
           "type": "String"
         }
       ],
       "type": "AzureSqlTable",
       "linkedServiceName": "AzureSqlLinkedService1",
       "typeProperties": {
         "tableName": "emp"
       },
       "availability": {
         "frequency": "Hour",
         "interval": 1
       }
     }
    }
    ```
    <span data-ttu-id="c83e9-237">Witaj Poniższa tabela zawiera opisy właściwości JSON hello używane we fragmencie hello:</span><span class="sxs-lookup"><span data-stu-id="c83e9-237">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

    | <span data-ttu-id="c83e9-238">Właściwość</span><span class="sxs-lookup"><span data-stu-id="c83e9-238">Property</span></span> | <span data-ttu-id="c83e9-239">Opis</span><span class="sxs-lookup"><span data-stu-id="c83e9-239">Description</span></span> |
    |:--- |:--- |
    | <span data-ttu-id="c83e9-240">type</span><span class="sxs-lookup"><span data-stu-id="c83e9-240">type</span></span> | <span data-ttu-id="c83e9-241">Właściwość type Hello ustawiono zbyt**AzureSqlTable** , ponieważ dane są kopiowane tooa tabeli w bazie danych Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="c83e9-241">hello type property is set too**AzureSqlTable** because data is copied tooa table in an Azure SQL database.</span></span> |
    | <span data-ttu-id="c83e9-242">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="c83e9-242">linkedServiceName</span></span> | <span data-ttu-id="c83e9-243">Odwołuje się toohello **AzureSqlLinkedService** utworzony wcześniej.</span><span class="sxs-lookup"><span data-stu-id="c83e9-243">Refers toohello **AzureSqlLinkedService** that you created earlier.</span></span> |
    | <span data-ttu-id="c83e9-244">tableName</span><span class="sxs-lookup"><span data-stu-id="c83e9-244">tableName</span></span> | <span data-ttu-id="c83e9-245">Określony hello **tabeli** toowhich hello dane są kopiowane.</span><span class="sxs-lookup"><span data-stu-id="c83e9-245">Specified hello **table** toowhich hello data is copied.</span></span> | 
    | <span data-ttu-id="c83e9-246">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="c83e9-246">frequency/interval</span></span> | <span data-ttu-id="c83e9-247">Witaj częstotliwość ustawiono zbyt**godzina** i interwał **1**, co oznacza, że wycinki danych wyjściowych hello są produkowane **co godzinę** między hello potoku rozpoczęcia i zakończenia godzin przed nie lub Po tych godzinach.</span><span class="sxs-lookup"><span data-stu-id="c83e9-247">hello frequency is set too**Hour** and interval is **1**, which means that hello output slices are produced **hourly** between hello pipeline start and end times, not before or after these times.</span></span>  |

    <span data-ttu-id="c83e9-248">Istnieją trzy kolumny — **identyfikator**, **imię**, i **nazwisko** — Witaj pustych elementów tabeli w bazie danych hello.</span><span class="sxs-lookup"><span data-stu-id="c83e9-248">There are three columns – **ID**, **FirstName**, and **LastName** – in hello emp table in hello database.</span></span> <span data-ttu-id="c83e9-249">Identyfikator jest kolumny tożsamości, więc musisz tylko toospecify **imię** i **nazwisko** tutaj.</span><span class="sxs-lookup"><span data-stu-id="c83e9-249">ID is an identity column, so you need toospecify only **FirstName** and **LastName** here.</span></span>

    <span data-ttu-id="c83e9-250">Aby uzyskać więcej informacji o tych właściwościach JSON, zobacz [artykuł dotyczący łącznika usługi Azure SQL](data-factory-azure-sql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="c83e9-250">For more information about these JSON properties, see [Azure SQL connector article](data-factory-azure-sql-connector.md#dataset-properties).</span></span>

## <a name="create-pipeline"></a><span data-ttu-id="c83e9-251">Tworzenie potoku</span><span class="sxs-lookup"><span data-stu-id="c83e9-251">Create pipeline</span></span>
<span data-ttu-id="c83e9-252">W tym kroku opisano tworzenie potoku za pomocą **działania kopiowania**, w którym parametr **InputDataset** jest używany jako dane wejściowe, a parametr **OutputDataset** jako dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="c83e9-252">In this step, you create a pipeline with a **copy activity** that uses **InputDataset** as an input and **OutputDataset** as an output.</span></span>

<span data-ttu-id="c83e9-253">Wyjściowy zestaw danych jest obecnie, jakie dysków hello harmonogramu.</span><span class="sxs-lookup"><span data-stu-id="c83e9-253">Currently, output dataset is what drives hello schedule.</span></span> <span data-ttu-id="c83e9-254">W tym samouczku wyjściowy zestaw danych jest skonfigurowane tooproduce wycinek godzinę.</span><span class="sxs-lookup"><span data-stu-id="c83e9-254">In this tutorial, output dataset is configured tooproduce a slice once an hour.</span></span> <span data-ttu-id="c83e9-255">potok Hello ma czas rozpoczęcia i godzina zakończenia, będące w ciągu jednego dnia od siebie, który wynosi 24 godziny.</span><span class="sxs-lookup"><span data-stu-id="c83e9-255">hello pipeline has a start time and end time that are one day apart, which is 24 hours.</span></span> <span data-ttu-id="c83e9-256">W związku z tym 24 wycinków wyjściowy zestaw danych są produkowane przez hello potoku.</span><span class="sxs-lookup"><span data-stu-id="c83e9-256">Therefore, 24 slices of output dataset are produced by hello pipeline.</span></span> 

1. <span data-ttu-id="c83e9-257">Kliknij prawym przyciskiem myszy **potoki** w hello **Eksploratora rozwiązań**, punktu zbyt**Dodaj**i kliknij przycisk **nowy element**.</span><span class="sxs-lookup"><span data-stu-id="c83e9-257">Right-click **Pipelines** in hello **Solution Explorer**, point too**Add**, and click **New Item**.</span></span>  
2. <span data-ttu-id="c83e9-258">Wybierz **kopiowania danych potoku** w hello **Dodaj nowy element** okno dialogowe i kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="c83e9-258">Select **Copy Data Pipeline** in hello **Add New Item** dialog box and click **Add**.</span></span> 
3. <span data-ttu-id="c83e9-259">Zamień hello JSON hello następującego formatu JSON i Zapisz hello **CopyActivity1.json** pliku.</span><span class="sxs-lookup"><span data-stu-id="c83e9-259">Replace hello JSON with hello following JSON and save hello **CopyActivity1.json** file.</span></span>

  ```json   
    {
     "name": "ADFTutorialPipeline",
     "properties": {
       "description": "Copy data from a blob tooAzure SQL table",
       "activities": [
         {
           "name": "CopyFromBlobToSQL",
           "type": "Copy",
           "inputs": [
             {
               "name": "InputDataset"
             }
           ],
           "outputs": [
             {
               "name": "OutputDataset"
             }
           ],
           "typeProperties": {
             "source": {
               "type": "BlobSource"
             },
             "sink": {
               "type": "SqlSink",
               "writeBatchSize": 10000,
               "writeBatchTimeout": "60:00:00"
             }
           },
           "Policy": {
             "concurrency": 1,
             "executionPriorityOrder": "NewestFirst",
             "style": "StartOfInterval",
             "retry": 0,
             "timeout": "01:00:00"
           }
         }
       ],
       "start": "2017-05-11T00:00:00Z",
       "end": "2017-05-12T00:00:00Z",
       "isPaused": false
     }
    }
    ```   
    - <span data-ttu-id="c83e9-260">W sekcji działania hello jest tylko jedno działanie którego **typu** ustawiono zbyt**kopiowania**.</span><span class="sxs-lookup"><span data-stu-id="c83e9-260">In hello activities section, there is only one activity whose **type** is set too**Copy**.</span></span> <span data-ttu-id="c83e9-261">Aby uzyskać więcej informacji o działaniu kopiowania hello, zobacz [działań przepływu danych](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="c83e9-261">For more information about hello copy activity, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="c83e9-262">W rozwiązaniach usługi Data Factory można również użyć [działań dotyczących przekształcania danych](data-factory-data-transformation-activities.md).</span><span class="sxs-lookup"><span data-stu-id="c83e9-262">In Data Factory solutions, you can also use [data transformation activities](data-factory-data-transformation-activities.md).</span></span>
    - <span data-ttu-id="c83e9-263">Dane wejściowe dla działania hello jest ustawiony za**InputDataset** i danych wyjściowych dla działania hello jest ustawiony za**OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="c83e9-263">Input for hello activity is set too**InputDataset** and output for hello activity is set too**OutputDataset**.</span></span> 
    - <span data-ttu-id="c83e9-264">W hello **typeProperties** sekcji **BlobSource** jest określony jako typ źródła hello i **SqlSink** jest określony jako typ ujścia hello.</span><span class="sxs-lookup"><span data-stu-id="c83e9-264">In hello **typeProperties** section, **BlobSource** is specified as hello source type and **SqlSink** is specified as hello sink type.</span></span> <span data-ttu-id="c83e9-265">Aby uzyskać pełną listę obsługiwanych przez działanie kopiowania hello jako źródła i wychwytywanie magazyny danych, zobacz [obsługiwane magazyny danych](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="c83e9-265">For a complete list of data stores supported by hello copy activity as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="c83e9-266">toolearn jak przechowywać toouse określonych danych obsługiwane jako źródło/ujście, kliknij łącze hello hello tabeli.</span><span class="sxs-lookup"><span data-stu-id="c83e9-266">toolearn how toouse a specific supported data store as a source/sink, click hello link in hello table.</span></span>  
     
    <span data-ttu-id="c83e9-267">Zastąp wartość hello hello **start** właściwość o hello bieżącego dnia i **zakończenia** wartości z hello następnego dnia.</span><span class="sxs-lookup"><span data-stu-id="c83e9-267">Replace hello value of hello **start** property with hello current day and **end** value with hello next day.</span></span> <span data-ttu-id="c83e9-268">Można określić tylko część daty hello i Pomiń hello czas część hello Data i godzina.</span><span class="sxs-lookup"><span data-stu-id="c83e9-268">You can specify only hello date part and skip hello time part of hello date time.</span></span> <span data-ttu-id="c83e9-269">Na przykład "2016-02-03", która odpowiada za "2016-02-03T00:00:00Z"</span><span class="sxs-lookup"><span data-stu-id="c83e9-269">For example, "2016-02-03", which is equivalent too"2016-02-03T00:00:00Z"</span></span>
     
    <span data-ttu-id="c83e9-270">Zarówno data/godzina rozpoczęcia, jak i data/godzina zakończenia muszą być w [formacie ISO](http://en.wikipedia.org/wiki/ISO_8601).</span><span class="sxs-lookup"><span data-stu-id="c83e9-270">Both start and end datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="c83e9-271">Przykładowo: 2016-10-14T16:32:41Z.</span><span class="sxs-lookup"><span data-stu-id="c83e9-271">For example: 2016-10-14T16:32:41Z.</span></span> <span data-ttu-id="c83e9-272">Witaj **zakończenia** czasu jest opcjonalne, ale możemy użyć w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="c83e9-272">hello **end** time is optional, but we use it in this tutorial.</span></span> 
     
    <span data-ttu-id="c83e9-273">Jeśli nie określisz wartości hello **zakończenia** właściwości, jest on obliczany jako "**start + 48 godzin**".</span><span class="sxs-lookup"><span data-stu-id="c83e9-273">If you do not specify value for hello **end** property, it is calculated as "**start + 48 hours**".</span></span> <span data-ttu-id="c83e9-274">potok hello toorun przez czas nieokreślony, określ **9999-09-09** jako wartość hello hello **zakończenia** właściwości.</span><span class="sxs-lookup"><span data-stu-id="c83e9-274">toorun hello pipeline indefinitely, specify **9999-09-09** as hello value for hello **end** property.</span></span>
     
    <span data-ttu-id="c83e9-275">W hello poprzedzających przykład istnieją 24 wycinków danych, jak każdy wycinek danych jest tworzone co godzinę.</span><span class="sxs-lookup"><span data-stu-id="c83e9-275">In hello preceding example, there are 24 data slices as each data slice is produced hourly.</span></span>

    <span data-ttu-id="c83e9-276">Opisy właściwości JSON w definicji potoku znajdują się w artykule dotyczącym [tworzenia potoków](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="c83e9-276">For descriptions of JSON properties in a pipeline definition, see [create pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="c83e9-277">Opisy właściwości JSON w definicji działania kopiowania znajdują się w artykule dotyczącym [działań związanych z przenoszeniem danych](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="c83e9-277">For descriptions of JSON properties in a copy activity definition, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="c83e9-278">Opisy właściwości JSON obsługiwanych przez BlobSource można znaleźć w [artykule dotyczącym łącznika usługi Azure Blob](data-factory-azure-blob-connector.md).</span><span class="sxs-lookup"><span data-stu-id="c83e9-278">For descriptions of JSON properties supported by BlobSource, see [Azure Blob connector article](data-factory-azure-blob-connector.md).</span></span> <span data-ttu-id="c83e9-279">Opisy właściwości JSON obsługiwanych przez SqlSink można znaleźć w artykule [dotyczącym łącznika usługi Azure SQL Database](data-factory-azure-sql-connector.md).</span><span class="sxs-lookup"><span data-stu-id="c83e9-279">For descriptions of JSON properties supported by SqlSink, see [Azure SQL Database connector article](data-factory-azure-sql-connector.md).</span></span>

## <a name="publishdeploy-data-factory-entities"></a><span data-ttu-id="c83e9-280">Publikowanie/wdrażanie jednostek usługi Fabryka danych</span><span class="sxs-lookup"><span data-stu-id="c83e9-280">Publish/deploy Data Factory entities</span></span>
<span data-ttu-id="c83e9-281">W tym kroku publikowane są utworzone wcześniej obiekty usługi Data Factory (połączone usługi, zestawy danych i potok).</span><span class="sxs-lookup"><span data-stu-id="c83e9-281">In this step, you publish Data Factory entities (linked services, datasets, and pipeline) you created earlier.</span></span> <span data-ttu-id="c83e9-282">Należy także określić nazwę hello hello nowe toobe fabryki danych utworzone toohold tych jednostek.</span><span class="sxs-lookup"><span data-stu-id="c83e9-282">You also specify hello name of hello new data factory toobe created toohold these entities.</span></span>  

1. <span data-ttu-id="c83e9-283">Kliknij prawym przyciskiem myszy projekt w Eksploratorze rozwiązań hello, a następnie kliknij przycisk **publikowania**.</span><span class="sxs-lookup"><span data-stu-id="c83e9-283">Right-click project in hello Solution Explorer, and click **Publish**.</span></span> 
2. <span data-ttu-id="c83e9-284">Jeśli widzisz **Zaloguj tooyour konta Microsoft** okno dialogowe, wprowadź swoje poświadczenia dla konta hello subskrypcji platformy Azure, a następnie kliknij przycisk **Zaloguj**.</span><span class="sxs-lookup"><span data-stu-id="c83e9-284">If you see **Sign in tooyour Microsoft account** dialog box, enter your credentials for hello account that has Azure subscription, and click **sign in**.</span></span>
3. <span data-ttu-id="c83e9-285">Powinny zostać wyświetlone następujące okno dialogowe hello:</span><span class="sxs-lookup"><span data-stu-id="c83e9-285">You should see hello following dialog box:</span></span>
   
   ![Okno dialogowe publikowania](./media/data-factory-copy-activity-tutorial-using-visual-studio/publish.png)
4. <span data-ttu-id="c83e9-287">W hello strony fabryki danych konfiguracji hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="c83e9-287">In hello Configure data factory page, do hello following steps:</span></span> 
   
   1. <span data-ttu-id="c83e9-288">Zaznacz opcję **Utwórz nową fabrykę danych**.</span><span class="sxs-lookup"><span data-stu-id="c83e9-288">select **Create New Data Factory** option.</span></span>
   2. <span data-ttu-id="c83e9-289">Wprowadź wartość **VSTutorialFactory** w polu **Nazwa**.</span><span class="sxs-lookup"><span data-stu-id="c83e9-289">Enter **VSTutorialFactory** for **Name**.</span></span>  
      
      > [!IMPORTANT]
      > <span data-ttu-id="c83e9-290">Nazwa fabryki danych Azure hello Hello musi być globalnie unikatowe.</span><span class="sxs-lookup"><span data-stu-id="c83e9-290">hello name of hello Azure data factory must be globally unique.</span></span> <span data-ttu-id="c83e9-291">Jeśli zostanie wyświetlony błąd o nazwie hello fabryki danych podczas publikowania, Zmień nazwę hello hello fabryki danych (na przykład yournameVSTutorialFactory) i spróbuj ponownie opublikować.</span><span class="sxs-lookup"><span data-stu-id="c83e9-291">If you receive an error about hello name of data factory when publishing, change hello name of hello data factory (for example, yournameVSTutorialFactory) and try publishing again.</span></span> <span data-ttu-id="c83e9-292">Artykuł [Data Factory — Naming Rules](data-factory-naming-rules.md) (Fabryka danych — zasady nazewnictwa) zawiera zasady nazewnictwa artefaktów usługi Fabryka danych.</span><span class="sxs-lookup"><span data-stu-id="c83e9-292">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>        
      > 
      > 
   3. <span data-ttu-id="c83e9-293">Wybierz subskrypcję platformy Azure dla hello **subskrypcji** pola.</span><span class="sxs-lookup"><span data-stu-id="c83e9-293">Select your Azure subscription for hello **Subscription** field.</span></span>
      
      > [!IMPORTANT]
      > <span data-ttu-id="c83e9-294">Jeśli nie ma żadnej subskrypcji. Upewnij się, czy użytkownik zalogowany przy użyciu konta administratora lub współadministratora subskrypcji hello.</span><span class="sxs-lookup"><span data-stu-id="c83e9-294">If you do not see any subscription, ensure that you logged in using an account that is an admin or co-admin of hello subscription.</span></span>  
      > 
      > 
   4. <span data-ttu-id="c83e9-295">Wybierz hello **grupy zasobów** dla toobe fabryki danych hello utworzony.</span><span class="sxs-lookup"><span data-stu-id="c83e9-295">Select hello **resource group** for hello data factory toobe created.</span></span> 
   5. <span data-ttu-id="c83e9-296">Wybierz hello **region** hello fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="c83e9-296">Select hello **region** for hello data factory.</span></span> <span data-ttu-id="c83e9-297">Tylko regiony obsługiwane przez hello usługi fabryka danych są wyświetlane na liście rozwijanej hello.</span><span class="sxs-lookup"><span data-stu-id="c83e9-297">Only regions supported by hello Data Factory service are shown in hello drop-down list.</span></span>
   6. <span data-ttu-id="c83e9-298">Kliknij przycisk **dalej** tooswitch toohello **publikowania elementów** strony.</span><span class="sxs-lookup"><span data-stu-id="c83e9-298">Click **Next** tooswitch toohello **Publish Items** page.</span></span>
      
       ![Strona konfiguracji fabryki danych](media/data-factory-copy-activity-tutorial-using-visual-studio/configure-data-factory-page.png)   
5. <span data-ttu-id="c83e9-300">W hello **publikowania elementów** upewnij się, że wszystkie hello fabryki danych jednostek są zaznaczone, a następnie kliknij przycisk **dalej** tooswitch toohello **Podsumowanie** strony.</span><span class="sxs-lookup"><span data-stu-id="c83e9-300">In hello **Publish Items** page, ensure that all hello Data Factories entities are selected, and click **Next** tooswitch toohello **Summary** page.</span></span>
   
   ![Strona publikowania elementów](media/data-factory-copy-activity-tutorial-using-visual-studio/publish-items-page.png)     
6. <span data-ttu-id="c83e9-302">Przejrzyj podsumowanie hello i kliknij przycisk **dalej** toostart hello wdrożenie procesu i sprawdź hello **stan wdrożenia**.</span><span class="sxs-lookup"><span data-stu-id="c83e9-302">Review hello summary and click **Next** toostart hello deployment process and view hello **Deployment Status**.</span></span>
   
   ![Strona publikowania podsumowania](media/data-factory-copy-activity-tutorial-using-visual-studio/publish-summary-page.png)
7. <span data-ttu-id="c83e9-304">W hello **stan wdrożenia** strony, powinien zostać wyświetlony stan hello hello procesu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="c83e9-304">In hello **Deployment Status** page, you should see hello status of hello deployment process.</span></span> <span data-ttu-id="c83e9-305">Po ukończeniu wdrażania hello, kliknij przycisk Zakończ.</span><span class="sxs-lookup"><span data-stu-id="c83e9-305">Click Finish after hello deployment is done.</span></span>
 
   ![Strona stanu wdrożenia](media/data-factory-copy-activity-tutorial-using-visual-studio/deployment-status.png)

<span data-ttu-id="c83e9-307">Należy zwrócić uwagę hello następujące punkty:</span><span class="sxs-lookup"><span data-stu-id="c83e9-307">Note hello following points:</span></span> 

* <span data-ttu-id="c83e9-308">Jeśli wystąpi błąd hello: "Ta subskrypcja nie jest zarejestrowany toouse przestrzeni nazw Microsoft.DataFactory", wykonaj jedną z następujących hello i spróbuj ponownie opublikować:</span><span class="sxs-lookup"><span data-stu-id="c83e9-308">If you receive hello error: "This subscription is not registered toouse namespace Microsoft.DataFactory", do one of hello following and try publishing again:</span></span> 
  
  * <span data-ttu-id="c83e9-309">W programie Azure PowerShell Uruchom hello następujące polecenia tooregister hello fabryki danych dostawcy.</span><span class="sxs-lookup"><span data-stu-id="c83e9-309">In Azure PowerShell, run hello following command tooregister hello Data Factory provider.</span></span> 

    ```PowerShell    
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```
    <span data-ttu-id="c83e9-310">Powitania po tooconfirm polecenie można uruchomić tego hello fabryki danych dostawca został zarejestrowany.</span><span class="sxs-lookup"><span data-stu-id="c83e9-310">You can run hello following command tooconfirm that hello Data Factory provider is registered.</span></span> 
    
    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * <span data-ttu-id="c83e9-311">Logowanie przy użyciu hello subskrypcji platformy Azure do hello [portalu Azure](https://portal.azure.com) i przejdź do bloku usługi fabryka danych tooa tworzenie fabryki danych w hello portalu Azure (lub).</span><span class="sxs-lookup"><span data-stu-id="c83e9-311">Login using hello Azure subscription into hello [Azure portal](https://portal.azure.com) and navigate tooa Data Factory blade (or) create a data factory in hello Azure portal.</span></span> <span data-ttu-id="c83e9-312">Ta akcja rejestruje automatycznie hello dostawcy dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="c83e9-312">This action automatically registers hello provider for you.</span></span>
* <span data-ttu-id="c83e9-313">Nazwa fabryki danych hello Hello mogą być zarejestrowana jako nazwa DNS w przyszłości hello i dlatego stać się publicznie widoczna.</span><span class="sxs-lookup"><span data-stu-id="c83e9-313">hello name of hello data factory may be registered as a DNS name in hello future and hence become publically visible.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c83e9-314">toocreate wystąpienia fabryki danych, należy toobe admin/współadministrator z hello subskrypcji platformy Azure</span><span class="sxs-lookup"><span data-stu-id="c83e9-314">toocreate Data Factory instances, you need toobe a admin/co-admin of hello Azure subscription</span></span>

## <a name="monitor-pipeline"></a><span data-ttu-id="c83e9-315">Monitorowanie potoku</span><span class="sxs-lookup"><span data-stu-id="c83e9-315">Monitor pipeline</span></span>
<span data-ttu-id="c83e9-316">Przejdź na stronę główną toohello fabrykę danych:</span><span class="sxs-lookup"><span data-stu-id="c83e9-316">Navigate toohello home page for your data factory:</span></span>

1. <span data-ttu-id="c83e9-317">Zaloguj się za[portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c83e9-317">Log in too[Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="c83e9-318">Kliknij przycisk **więcej usług** hello menu po lewej stronie i kliknij przycisk **fabryki danych**.</span><span class="sxs-lookup"><span data-stu-id="c83e9-318">Click **More services** on hello left menu, and click **Data factories**.</span></span>

    ![Przeglądanie fabryk danych](media/data-factory-copy-activity-tutorial-using-visual-studio/browse-data-factories.png)
3. <span data-ttu-id="c83e9-320">Wpisz nazwę hello w fabryce danych.</span><span class="sxs-lookup"><span data-stu-id="c83e9-320">Start typing hello name of your data factory.</span></span>

    ![Nazwa fabryki danych](media/data-factory-copy-activity-tutorial-using-visual-studio/enter-data-factory-name.png) 
4. <span data-ttu-id="c83e9-322">Kliknij przycisk fabrykę danych w hello wyniki listy toosee hello strony głównej fabryką danych.</span><span class="sxs-lookup"><span data-stu-id="c83e9-322">Click your data factory in hello results list toosee hello home page for your data factory.</span></span>

    ![Strona główna fabryki danych](media/data-factory-copy-activity-tutorial-using-visual-studio/data-factory-home-page.png)
5. <span data-ttu-id="c83e9-324">Postępuj zgodnie z instrukcjami [monitorowanie zestawów danych i potoku](data-factory-copy-activity-tutorial-using-azure-portal.md#monitor-pipeline) toomonitor hello potoku i zestawy danych zostały utworzone w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="c83e9-324">Follow instructions from [Monitor datasets and pipeline](data-factory-copy-activity-tutorial-using-azure-portal.md#monitor-pipeline) toomonitor hello pipeline and datasets you have created in this tutorial.</span></span> <span data-ttu-id="c83e9-325">Obecnie program Visual Studio nie obsługuje monitorowania potoków usługi Data Factory.</span><span class="sxs-lookup"><span data-stu-id="c83e9-325">Currently, Visual Studio does not support monitoring Data Factory pipelines.</span></span> 

## <a name="summary"></a><span data-ttu-id="c83e9-326">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="c83e9-326">Summary</span></span>
<span data-ttu-id="c83e9-327">W tym samouczku danych toocopy fabryki danych Azure została utworzona z bazy danych Azure SQL tooan obiektów blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c83e9-327">In this tutorial, you created an Azure data factory toocopy data from an Azure blob tooan Azure SQL database.</span></span> <span data-ttu-id="c83e9-328">Użyto fabryki danych hello toocreate programu Visual Studio, połączone usługi, zestawy danych i potoku.</span><span class="sxs-lookup"><span data-stu-id="c83e9-328">You used Visual Studio toocreate hello data factory, linked services, datasets, and a pipeline.</span></span> <span data-ttu-id="c83e9-329">Poniżej przedstawiono ogólne kroki hello, wykonane w tym samouczku:</span><span class="sxs-lookup"><span data-stu-id="c83e9-329">Here are hello high-level steps you performed in this tutorial:</span></span>  

1. <span data-ttu-id="c83e9-330">Tworzenie **fabryki danych** Azure.</span><span class="sxs-lookup"><span data-stu-id="c83e9-330">Created an Azure **data factory**.</span></span>
2. <span data-ttu-id="c83e9-331">Tworzenie **połączonych usług**:</span><span class="sxs-lookup"><span data-stu-id="c83e9-331">Created **linked services**:</span></span>
   1. <span data-ttu-id="c83e9-332">**Usługi Azure Storage** połączone konta magazynu Azure, która przechowuje dane wejściowe toolink usługi.</span><span class="sxs-lookup"><span data-stu-id="c83e9-332">An **Azure Storage** linked service toolink your Azure Storage account that holds input data.</span></span>     
   2. <span data-ttu-id="c83e9-333">**Azure SQL** połączone z bazy danych Azure SQL, która przechowuje dane wyjściowe hello toolink usługi.</span><span class="sxs-lookup"><span data-stu-id="c83e9-333">An **Azure SQL** linked service toolink your Azure SQL database that holds hello output data.</span></span> 
3. <span data-ttu-id="c83e9-334">Tworzenie **zestawów danych** opisujących dane wejściowe i wyjściowe dla potoków.</span><span class="sxs-lookup"><span data-stu-id="c83e9-334">Created **datasets**, which describe input data and output data for pipelines.</span></span>
4. <span data-ttu-id="c83e9-335">Tworzenie **potoku** za pomocą **działania kopiowania**, w którym źródłem jest element **BlobSource**, a ujściem element **SqlSink**.</span><span class="sxs-lookup"><span data-stu-id="c83e9-335">Created a **pipeline** with a **Copy Activity** with **BlobSource** as source and **SqlSink** as sink.</span></span> 

<span data-ttu-id="c83e9-336">toosee toouse danych tootransform działania Hive HDInsight przy użyciu klastra Azure HDInsight, zobacz temat [ samouczek: Tworzenie pierwszego potoku dane tootransform przy użyciu klastra usługi Hadoop](data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="c83e9-336">toosee how toouse a HDInsight Hive Activity tootransform data by using Azure HDInsight cluster, see [ Tutorial: Build your first pipeline tootransform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span>

<span data-ttu-id="c83e9-337">Powiązane z dwóch działań (Uruchom jedno działanie po drugim), ustawiając hello wyjściowy zestaw danych z jednego działania jako hello wejściowy zestaw danych z hello innych działań.</span><span class="sxs-lookup"><span data-stu-id="c83e9-337">You can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="c83e9-338">Szczegółowe informacje znajdują się w artykule [Scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md) (Planowanie i wykonywanie w usłudze Data Factory).</span><span class="sxs-lookup"><span data-stu-id="c83e9-338">See [Scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md) for detailed information.</span></span> 

## <a name="view-all-data-factories-in-server-explorer"></a><span data-ttu-id="c83e9-339">Wyświetlanie wszystkich fabryk danych w Eksploratorze serwera</span><span class="sxs-lookup"><span data-stu-id="c83e9-339">View all data factories in Server Explorer</span></span>
<span data-ttu-id="c83e9-340">W tej sekcji opisano sposób toouse hello Eksploratora serwera w Visual Studio tooview wszystkie hello fabryki danych w ramach subskrypcji platformy Azure i tworzenia projektu programu Visual Studio, w oparciu o istniejącą fabrykę danych.</span><span class="sxs-lookup"><span data-stu-id="c83e9-340">This section describes how toouse hello Server Explorer in Visual Studio tooview all hello data factories in your Azure subscription and create a Visual Studio project based on an existing data factory.</span></span> 

1. <span data-ttu-id="c83e9-341">W **programu Visual Studio**, kliknij przycisk **widoku** hello menu i kliknij przycisk **Eksploratora serwera**.</span><span class="sxs-lookup"><span data-stu-id="c83e9-341">In **Visual Studio**, click **View** on hello menu, and click **Server Explorer**.</span></span>
2. <span data-ttu-id="c83e9-342">W oknie Eksploratora serwera hello, rozwiń węzeł **Azure** i rozwiń **fabryki danych**.</span><span class="sxs-lookup"><span data-stu-id="c83e9-342">In hello Server Explorer window, expand **Azure** and expand **Data Factory**.</span></span> <span data-ttu-id="c83e9-343">Jeśli widzisz **Zaloguj tooVisual Studio**, wprowadź hello **konta** skojarzone z subskrypcją platformy Azure i kliknij przycisk **Kontynuuj**.</span><span class="sxs-lookup"><span data-stu-id="c83e9-343">If you see **Sign in tooVisual Studio**, enter hello **account** associated with your Azure subscription and click **Continue**.</span></span> <span data-ttu-id="c83e9-344">Wprowadź **hasło** i kliknij przycisk **Zaloguj**.</span><span class="sxs-lookup"><span data-stu-id="c83e9-344">Enter **password**, and click **Sign in**.</span></span> <span data-ttu-id="c83e9-345">Visual Studio próbuje tooget informacji na temat wszystkich fabryki danych Azure w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="c83e9-345">Visual Studio tries tooget information about all Azure data factories in your subscription.</span></span> <span data-ttu-id="c83e9-346">Zobacz hello stan tej operacji w hello **listy zadań fabryki danych** okna.</span><span class="sxs-lookup"><span data-stu-id="c83e9-346">You see hello status of this operation in hello **Data Factory Task List** window.</span></span>

    ![Eksplorator serwera](./media/data-factory-copy-activity-tutorial-using-visual-studio/server-explorer.png)

## <a name="create-a-visual-studio-project-for-an-existing-data-factory"></a><span data-ttu-id="c83e9-348">Tworzenie projektu programu Visual Studio dla istniejącej fabryki danych</span><span class="sxs-lookup"><span data-stu-id="c83e9-348">Create a Visual Studio project for an existing data factory</span></span>

- <span data-ttu-id="c83e9-349">Kliknij prawym przyciskiem myszy w Eksploratorze serwera fabryki danych i wybierz **tooNew wyeksportować fabryki danych projektu** toocreate na istniejącą fabrykę danych na podstawie projektu programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c83e9-349">Right-click a data factory in Server Explorer, and select **Export Data Factory tooNew Project** toocreate a Visual Studio project based on an existing data factory.</span></span>

    ![Eksportowanie projektu programu VS tooa fabryki danych](./media/data-factory-copy-activity-tutorial-using-visual-studio/export-data-factory-menu.png)  

## <a name="update-data-factory-tools-for-visual-studio"></a><span data-ttu-id="c83e9-351">Aktualizacja narzędzi usługi Fabryka danych dla programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c83e9-351">Update Data Factory tools for Visual Studio</span></span>
<span data-ttu-id="c83e9-352">tooupdate fabryki danych Azure tools dla programu Visual Studio hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="c83e9-352">tooupdate Azure Data Factory tools for Visual Studio, do hello following steps:</span></span>

1. <span data-ttu-id="c83e9-353">Kliknij przycisk **narzędzia** na powitania menu i wybierz **rozszerzenia i aktualizacje**.</span><span class="sxs-lookup"><span data-stu-id="c83e9-353">Click **Tools** on hello menu and select **Extensions and Updates**.</span></span> 
2. <span data-ttu-id="c83e9-354">Wybierz **aktualizacje** w lewym okienku hello, a następnie wybierz **galerii programu Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="c83e9-354">Select **Updates** in hello left pane and then select **Visual Studio Gallery**.</span></span>
3. <span data-ttu-id="c83e9-355">Wybierz pozycję **Narzędzia usługi Fabryka danych Azure dla programu Visual Studio** i kliknij przycisk **Aktualizuj**.</span><span class="sxs-lookup"><span data-stu-id="c83e9-355">Select **Azure Data Factory tools for Visual Studio** and click **Update**.</span></span> <span data-ttu-id="c83e9-356">Jeśli tego wpisu nie jest widoczny, masz już najnowszą wersję narzędzia hello hello.</span><span class="sxs-lookup"><span data-stu-id="c83e9-356">If you do not see this entry, you already have hello latest version of hello tools.</span></span> 

## <a name="use-configuration-files"></a><span data-ttu-id="c83e9-357">Korzystanie z plików konfiguracji</span><span class="sxs-lookup"><span data-stu-id="c83e9-357">Use configuration files</span></span>
<span data-ttu-id="c83e9-358">Pliki konfiguracji w programie Visual Studio tooconfigure właściwości można użyć dla połączonej usługi/tabel/potoków inaczej dla każdego środowiska.</span><span class="sxs-lookup"><span data-stu-id="c83e9-358">You can use configuration files in Visual Studio tooconfigure properties for linked services/tables/pipelines differently for each environment.</span></span>

<span data-ttu-id="c83e9-359">Należy wziąć pod uwagę powitania po definicji JSON połączoną usługą magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="c83e9-359">Consider hello following JSON definition for an Azure Storage linked service.</span></span> <span data-ttu-id="c83e9-360">toospecify **connectionString** z różnych wartości accountname i accountkey oparte na powitania środowiska (deweloperów testu/produkcja) toowhich wdrażasz jednostek fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="c83e9-360">toospecify **connectionString** with different values for accountname and accountkey based on hello environment (Dev/Test/Production) toowhich you are deploying Data Factory entities.</span></span> <span data-ttu-id="c83e9-361">Możesz uzyskać takie zachowanie, stosując oddzielny plik konfiguracji dla każdego środowiska.</span><span class="sxs-lookup"><span data-stu-id="c83e9-361">You can achieve this behavior by using separate configuration file for each environment.</span></span>

```json
{
    "name": "StorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "description": "",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
        }
    }
}
```

### <a name="add-a-configuration-file"></a><span data-ttu-id="c83e9-362">Dodawanie pliku konfiguracji</span><span class="sxs-lookup"><span data-stu-id="c83e9-362">Add a configuration file</span></span>
<span data-ttu-id="c83e9-363">Dodaj plik konfiguracji dla każdego środowiska, wykonując następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="c83e9-363">Add a configuration file for each environment by performing hello following steps:</span></span>   

1. <span data-ttu-id="c83e9-364">Kliknij prawym przyciskiem myszy hello fabryki danych projektu w rozwiązaniu programu Visual Studio, wskaż zbyt**Dodaj**i kliknij przycisk **nowy element**.</span><span class="sxs-lookup"><span data-stu-id="c83e9-364">Right-click hello Data Factory project in your Visual Studio solution, point too**Add**, and click **New item**.</span></span>
2. <span data-ttu-id="c83e9-365">Wybierz **konfiguracji** z listy hello zainstalowane szablony powitania po lewej stronie, wybierz **pliku konfiguracyjnego**, wprowadź **nazwa** hello konfiguracji pliku, a następnie kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="c83e9-365">Select **Config** from hello list of installed templates on hello left, select **Configuration File**, enter a **name** for hello configuration file, and click **Add**.</span></span>

    ![Dodawanie pliku konfiguracji](./media/data-factory-build-your-first-pipeline-using-vs/add-config-file.png)
3. <span data-ttu-id="c83e9-367">Dodaj parametry konfiguracji i ich wartości hello następującego formatu:</span><span class="sxs-lookup"><span data-stu-id="c83e9-367">Add configuration parameters and their values in hello following format:</span></span>

    ```json
    {
        "$schema": "http://datafactories.schema.management.azure.com/vsschemas/V1/Microsoft.DataFactory.Config.json",
        "AzureStorageLinkedService1": [
            {
                "name": "$.properties.typeProperties.connectionString",
                "value": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
            }
        ],
        "AzureSqlLinkedService1": [
            {
                "name": "$.properties.typeProperties.connectionString",
                "value":  "Server=tcp:spsqlserver.database.windows.net,1433;Database=spsqldb;User ID=spelluru;Password=Sowmya123;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
            }
        ]
    }
    ```

    <span data-ttu-id="c83e9-368">W tym przykładzie opisano konfigurację właściwości connectionString połączonej usługi Azure Storage oraz połączonej usługi SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="c83e9-368">This example configures connectionString property of an Azure Storage linked service and an Azure SQL linked service.</span></span> <span data-ttu-id="c83e9-369">Zwróć uwagę, że składnia hello określania nazwy jest [JsonPath](http://goessner.net/articles/JsonPath/).</span><span class="sxs-lookup"><span data-stu-id="c83e9-369">Notice that hello syntax for specifying name is [JsonPath](http://goessner.net/articles/JsonPath/).</span></span>   

    <span data-ttu-id="c83e9-370">Jeśli JSON ma właściwość, która ma tablicę wartości, jak pokazano w hello następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="c83e9-370">If JSON has a property that has an array of values as shown in hello following code:</span></span>  

    ```json
    "structure": [
          {
              "name": "FirstName",
            "type": "String"
          },
          {
            "name": "LastName",
            "type": "String"
        }
    ],
    ```

    <span data-ttu-id="c83e9-371">Skonfiguruj właściwości, jak pokazano w hello następującego pliku konfiguracji (Użyj liczony od zera indeksowania):</span><span class="sxs-lookup"><span data-stu-id="c83e9-371">Configure properties as shown in hello following configuration file (use zero-based indexing):</span></span>

    ```json
    {
        "name": "$.properties.structure[0].name",
        "value": "FirstName"
    }
    {
        "name": "$.properties.structure[0].type",
        "value": "String"
    }
    {
        "name": "$.properties.structure[1].name",
        "value": "LastName"
    }
    {
        "name": "$.properties.structure[1].type",
        "value": "String"
    }
    ```

### <a name="property-names-with-spaces"></a><span data-ttu-id="c83e9-372">Nazwy właściwości zawierające spacje</span><span class="sxs-lookup"><span data-stu-id="c83e9-372">Property names with spaces</span></span>
<span data-ttu-id="c83e9-373">Jeśli nazwa właściwości zawiera spacje, Użyj nawiasów kwadratowych, jak pokazano w hello poniższy przykład (nazwa serwera bazy danych):</span><span class="sxs-lookup"><span data-stu-id="c83e9-373">If a property name has spaces in it, use square brackets as shown in hello following example (Database server name):</span></span>

```json
 {
     "name": "$.properties.activities[1].typeProperties.webServiceParameters.['Database server name']",
     "value": "MyAsqlServer.database.windows.net"
 }
```

### <a name="deploy-solution-using-a-configuration"></a><span data-ttu-id="c83e9-374">Wdrożenie rozwiązania przy użyciu konfiguracji</span><span class="sxs-lookup"><span data-stu-id="c83e9-374">Deploy solution using a configuration</span></span>
<span data-ttu-id="c83e9-375">Publikując jednostek fabryki danych Azure w wersji programu VS, można będzie określić konfigurację hello mają toouse dla tej operacji publikowania.</span><span class="sxs-lookup"><span data-stu-id="c83e9-375">When you are publishing Azure Data Factory entities in VS, you can specify hello configuration that you want toouse for that publishing operation.</span></span>

<span data-ttu-id="c83e9-376">toopublish jednostki w projekcie usługi fabryka danych Azure przy użyciu pliku konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="c83e9-376">toopublish entities in an Azure Data Factory project using configuration file:</span></span>   

1. <span data-ttu-id="c83e9-377">Kliknij prawym przyciskiem myszy projekt fabryki danych i kliknij przycisk **publikowania** toosee hello **publikowania elementów** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="c83e9-377">Right-click Data Factory project and click **Publish** toosee hello **Publish Items** dialog box.</span></span>
2. <span data-ttu-id="c83e9-378">Wybierz istniejącą fabrykę danych lub określ wartości dla tworzenie fabryki danych na powitania **fabryki danych skonfiguruj** , a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="c83e9-378">Select an existing data factory or specify values for creating a data factory on hello **Configure data factory** page, and click **Next**.</span></span>   
3. <span data-ttu-id="c83e9-379">Na powitania **publikowania elementów** stron: Zobacz listy rozwijanej z dostępnych konfiguracji hello **Wybieranie konfiguracji wdrożenia** pola.</span><span class="sxs-lookup"><span data-stu-id="c83e9-379">On hello **Publish Items** page: you see a drop-down list with available configurations for hello **Select Deployment Config** field.</span></span>

    ![Wybieranie pliku konfiguracji](./media/data-factory-build-your-first-pipeline-using-vs/select-config-file.png)
4. <span data-ttu-id="c83e9-381">Wybierz hello **pliku konfiguracyjnego** czy chcesz toouse i kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="c83e9-381">Select hello **configuration file** that you would like toouse and click **Next**.</span></span>
5. <span data-ttu-id="c83e9-382">Upewnij się, że widoczne hello nazwę pliku JSON w hello **Podsumowanie** i kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="c83e9-382">Confirm that you see hello name of JSON file in hello **Summary** page and click **Next**.</span></span>
6. <span data-ttu-id="c83e9-383">Kliknij przycisk **Zakończ** po zakończeniu operacji wdrażania hello.</span><span class="sxs-lookup"><span data-stu-id="c83e9-383">Click **Finish** after hello deployment operation is finished.</span></span>

<span data-ttu-id="c83e9-384">Podczas wdrażania, hello wartości z pliku konfiguracji hello są używane tooset wartości właściwości w plikach JSON hello przed jednostek hello tooAzure wdrożonej usługi fabryka danych.</span><span class="sxs-lookup"><span data-stu-id="c83e9-384">When you deploy, hello values from hello configuration file are used tooset values for properties in hello JSON files before hello entities are deployed tooAzure Data Factory service.</span></span>   

## <a name="use-azure-key-vault"></a><span data-ttu-id="c83e9-385">Korzystanie z rozwiązania Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="c83e9-385">Use Azure Key Vault</span></span>
<span data-ttu-id="c83e9-386">Nie jest zalecane i często przed poufnych danych toocommit zasad zabezpieczeń takich jak repozytorium kodu toohello ciągów połączenia.</span><span class="sxs-lookup"><span data-stu-id="c83e9-386">It is not advisable and often against security policy toocommit sensitive data such as connection strings toohello code repository.</span></span> <span data-ttu-id="c83e9-387">Zobacz [ADF bezpiecznego publikowania](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ADFSecurePublish) w toolearn GitHub o poufne informacje są przechowywane w magazynie kluczy Azure i używa go podczas publikowania jednostek fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="c83e9-387">See [ADF Secure Publish](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ADFSecurePublish) sample on GitHub toolearn about storing sensitive information in Azure Key Vault and using it while publishing Data Factory entities.</span></span> <span data-ttu-id="c83e9-388">Hello bezpiecznego publikowania rozszerzenia dla programu Visual Studio umożliwia toobe kluczy tajnych hello przechowywane w magazynie klucza i tylko toothem odwołania są określone w połączonych usług / konfiguracji wdrażania.</span><span class="sxs-lookup"><span data-stu-id="c83e9-388">hello Secure Publish extension for Visual Studio allows hello secrets toobe stored in Key Vault and only references toothem are specified in linked services/ deployment configurations.</span></span> <span data-ttu-id="c83e9-389">Te odwołania są rozpoznawane podczas publikowania tooAzure jednostek fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="c83e9-389">These references are resolved when you publish Data Factory entities tooAzure.</span></span> <span data-ttu-id="c83e9-390">Te pliki mogą być następnie repozytorium zatwierdzone toosource bez narażania żadnych kluczy tajnych.</span><span class="sxs-lookup"><span data-stu-id="c83e9-390">These files can then be committed toosource repository without exposing any secrets.</span></span>


## <a name="next-steps"></a><span data-ttu-id="c83e9-391">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c83e9-391">Next steps</span></span>
<span data-ttu-id="c83e9-392">W tym samouczku użyto magazynu obiektów blob platformy Azure jako magazynu danych źródła oraz bazy danych SQL na platformie Azure jako magazynu danych docelowych w operacji kopiowania.</span><span class="sxs-lookup"><span data-stu-id="c83e9-392">In this tutorial, you used Azure blob storage as a source data store and an Azure SQL database as a destination data store in a copy operation.</span></span> <span data-ttu-id="c83e9-393">Witaj Poniższa tabela zawiera listę magazynów danych obsługiwane jako źródeł i miejsc docelowych przez działanie kopiowania hello:</span><span class="sxs-lookup"><span data-stu-id="c83e9-393">hello following table provides a list of data stores supported as sources and destinations by hello copy activity:</span></span> 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

<span data-ttu-id="c83e9-394">toolearn o jak magazyn danych toocopy z danych, kliknij łącze hello hello magazynu danych w tabeli hello.</span><span class="sxs-lookup"><span data-stu-id="c83e9-394">toolearn about how toocopy data to/from a data store, click hello link for hello data store in hello table.</span></span>
