---
title: "Samouczek: Tworzenie potoku toomove danych przy użyciu programu Azure PowerShell | Dokumentacja firmy Microsoft"
description: "Ten samouczek zawiera instrukcje tworzenia potoku usługi Azure Data Factory za pomocą działania kopiowania przy użyciu programu Azure PowerShell."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 71087349-9365-4e95-9847-170658216ed8
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 21406d7dfaa0c555b2538fbb52839d761c140fc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-create-a-data-factory-pipeline-that-moves-data-by-using-azure-powershell"></a><span data-ttu-id="6592d-103">Samouczek: tworzenie potoku usługi Data Factory przenoszącego dane przy użyciu programu Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="6592d-103">Tutorial: Create a Data Factory pipeline that moves data by using Azure PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6592d-104">Przegląd i wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="6592d-104">Overview and prerequisites</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [<span data-ttu-id="6592d-105">Kreator kopiowania</span><span class="sxs-lookup"><span data-stu-id="6592d-105">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
> * [<span data-ttu-id="6592d-106">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="6592d-106">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [<span data-ttu-id="6592d-107">Program Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6592d-107">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [<span data-ttu-id="6592d-108">Program PowerShell</span><span class="sxs-lookup"><span data-stu-id="6592d-108">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
> * [<span data-ttu-id="6592d-109">Szablon usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="6592d-109">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [<span data-ttu-id="6592d-110">Interfejs API REST</span><span class="sxs-lookup"><span data-stu-id="6592d-110">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [<span data-ttu-id="6592d-111">Interfejs API .NET</span><span class="sxs-lookup"><span data-stu-id="6592d-111">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)
>
>

<span data-ttu-id="6592d-112">W tym artykule dowiesz się, jak toouse PowerShell toocreate fabryki danych z potok, który kopiuje dane z bazy danych Azure SQL tooan magazynu obiektów blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6592d-112">In this article, you learn how toouse PowerShell toocreate a data factory with a pipeline that copies data from an Azure blob storage tooan Azure SQL database.</span></span> <span data-ttu-id="6592d-113">Jeśli nowy tooAzure fabryki danych, zapoznaj się z artykułem hello [tooAzure wprowadzenie fabryki danych](data-factory-introduction.md) artykuł przed wykonaniem tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="6592d-113">If you are new tooAzure Data Factory, read through hello [Introduction tooAzure Data Factory](data-factory-introduction.md) article before doing this tutorial.</span></span>   

<span data-ttu-id="6592d-114">W tym samouczku opisano tworzenie potoku z jednym działaniem (Działanie kopiowania).</span><span class="sxs-lookup"><span data-stu-id="6592d-114">In this tutorial, you create a pipeline with one activity in it: Copy Activity.</span></span> <span data-ttu-id="6592d-115">działanie kopiowania Hello kopiuje dane z magazynu danych obsługiwanych ujścia magazynu tooa obsługiwane dane.</span><span class="sxs-lookup"><span data-stu-id="6592d-115">hello copy activity copies data from a supported data store tooa supported sink data store.</span></span> <span data-ttu-id="6592d-116">Aby zapoznać się z listą magazynów danych obsługiwanych jako źródła i ujścia, zobacz [obsługiwane magazyny danych](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="6592d-116">For a list of data stores supported as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="6592d-117">działanie Hello jest obsługiwany przez ogólnie dostępna usługa, która można skopiować dane między różnych magazynach danych w sposób bezpieczny, niezawodny i skalowalności.</span><span class="sxs-lookup"><span data-stu-id="6592d-117">hello activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="6592d-118">Aby uzyskać więcej informacji na temat hello działanie kopiowania, zobacz [działań przepływu danych](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="6592d-118">For more information about hello Copy Activity, see [Data Movement Activities](data-factory-data-movement-activities.md).</span></span>

<span data-ttu-id="6592d-119">Potok może obejmować więcej niż jedno działanie.</span><span class="sxs-lookup"><span data-stu-id="6592d-119">A pipeline can have more than one activity.</span></span> <span data-ttu-id="6592d-120">I tworzenia łańcucha dwa działania (Uruchom jedno działanie po drugim), ustawiając hello wyjściowy zestaw danych z jednego działania jako hello wejściowy zestaw danych z hello innych działań.</span><span class="sxs-lookup"><span data-stu-id="6592d-120">And, you can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="6592d-121">Aby uzyskać więcej informacji, zobacz sekcję dotyczącą [wielu działań w potoku](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span><span class="sxs-lookup"><span data-stu-id="6592d-121">For more information, see [multiple activities in a pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span>

> [!NOTE]
> <span data-ttu-id="6592d-122">W tym artykule nie opisano wszystkich poleceń cmdlet fabryki danych hello.</span><span class="sxs-lookup"><span data-stu-id="6592d-122">This article does not cover all hello Data Factory cmdlets.</span></span> <span data-ttu-id="6592d-123">Pełna dokumentacja dotycząca tych poleceń cmdlet znajduje się w artykule [Dokumentacja dotycząca poleceń cmdlet usługi Data Factory](/powershell/module/azurerm.datafactories).</span><span class="sxs-lookup"><span data-stu-id="6592d-123">See [Data Factory Cmdlet Reference](/powershell/module/azurerm.datafactories) for comprehensive documentation on these cmdlets.</span></span>
> 
> <span data-ttu-id="6592d-124">Witaj potoku danych w tym samouczku kopiuje dane z magazynu danych źródła danych magazynu tooa docelowego.</span><span class="sxs-lookup"><span data-stu-id="6592d-124">hello data pipeline in this tutorial copies data from a source data store tooa destination data store.</span></span> <span data-ttu-id="6592d-125">Samouczek na temat danych tootransform przy użyciu fabryki danych Azure, zobacz [samouczek: Tworzenie danych tootransform potoku, przy użyciu klastra usługi Hadoop](data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="6592d-125">For a tutorial on how tootransform data using Azure Data Factory, see [Tutorial: Build a pipeline tootransform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6592d-126">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="6592d-126">Prerequisites</span></span>
- <span data-ttu-id="6592d-127">Wymagania wstępne wymienione w hello ukończyć [wymagania wstępne dotyczące samouczka](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="6592d-127">Complete prerequisites listed in hello [tutorial prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) article.</span></span>
- <span data-ttu-id="6592d-128">Zainstaluj program **Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="6592d-128">Install **Azure PowerShell**.</span></span> <span data-ttu-id="6592d-129">Postępuj zgodnie z instrukcjami hello [jak tooinstall i konfigurowanie programu Azure PowerShell](../powershell-install-configure.md).</span><span class="sxs-lookup"><span data-stu-id="6592d-129">Follow hello instructions in [How tooinstall and configure Azure PowerShell](../powershell-install-configure.md).</span></span>

## <a name="steps"></a><span data-ttu-id="6592d-130">Kroki</span><span class="sxs-lookup"><span data-stu-id="6592d-130">Steps</span></span>
<span data-ttu-id="6592d-131">Poniżej przedstawiono kroki hello, które należy wykonać w ramach tego samouczka:</span><span class="sxs-lookup"><span data-stu-id="6592d-131">Here are hello steps you perform as part of this tutorial:</span></span>

1. <span data-ttu-id="6592d-132">Utworzenie **fabryki danych** na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="6592d-132">Create an Azure **data factory**.</span></span> <span data-ttu-id="6592d-133">W tym kroku jest tworzona fabryka danych o nazwie ADFTutorialDataFactoryPSH.</span><span class="sxs-lookup"><span data-stu-id="6592d-133">In this step, you create a data factory named ADFTutorialDataFactoryPSH.</span></span> 
2. <span data-ttu-id="6592d-134">Utwórz **połączone usługi** w fabryce danych hello.</span><span class="sxs-lookup"><span data-stu-id="6592d-134">Create **linked services** in hello data factory.</span></span> <span data-ttu-id="6592d-135">Ten krok polega na utworzeniu dwóch połączonych usług: Azure Storage i Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="6592d-135">In this step, you create two linked services of types: Azure Storage and Azure SQL Database.</span></span> 
    
    <span data-ttu-id="6592d-136">Witaj AzureStorageLinkedService łączy fabrykę danych toohello konta magazynu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6592d-136">hello AzureStorageLinkedService links your Azure storage account toohello data factory.</span></span> <span data-ttu-id="6592d-137">Utworzono kontener i przekazany w ramach konta magazynu danych toothis [wymagania wstępne](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="6592d-137">You created a container and uploaded data toothis storage account as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>   

    <span data-ttu-id="6592d-138">AzureSqlLinkedService łączy fabrykę danych toohello bazy danych Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="6592d-138">AzureSqlLinkedService links your Azure SQL database toohello data factory.</span></span> <span data-ttu-id="6592d-139">dane Hello, który jest skopiowany z magazynu obiektów blob hello są przechowywane w tej bazie danych.</span><span class="sxs-lookup"><span data-stu-id="6592d-139">hello data that is copied from hello blob storage is stored in this database.</span></span> <span data-ttu-id="6592d-140">W ramach [wymagań wstępnych](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) w tej bazie danych została utworzona tabela SQL.</span><span class="sxs-lookup"><span data-stu-id="6592d-140">You created a SQL table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>   
3. <span data-ttu-id="6592d-141">Utwórz dane wejściowe i wyjściowe **zestawów danych** w fabryce danych hello.</span><span class="sxs-lookup"><span data-stu-id="6592d-141">Create input and output **datasets** in hello data factory.</span></span>  
    
    <span data-ttu-id="6592d-142">Hello Azure połączoną usługą magazynu określa parametry połączenia hello, która używa usługi fabryka danych w czasie wykonywania tooconnect tooyour kontem magazynu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6592d-142">hello Azure storage linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="6592d-143">I zestawu danych wejściowych obiektu blob hello określa hello kontenera i folderu hello, który zawiera hello danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="6592d-143">And, hello input blob dataset specifies hello container and hello folder that contains hello input data.</span></span>  

    <span data-ttu-id="6592d-144">Podobnie hello usługi baza danych SQL Azure połączone określa hello parametry połączenia, które korzysta z usługi fabryka danych w czasie wykonywania tooconnect tooyour — bazy danych Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="6592d-144">Similarly, hello Azure SQL Database linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure SQL database.</span></span> <span data-ttu-id="6592d-145">I tabeli hello hello bazy danych toowhich hello danych z magazynu obiektów blob hello jest kopiowany określa hello danych wyjściowych SQL tabeli dataset.</span><span class="sxs-lookup"><span data-stu-id="6592d-145">And, hello output SQL table dataset specifies hello table in hello database toowhich hello data from hello blob storage is copied.</span></span>
4. <span data-ttu-id="6592d-146">Utwórz **potoku** w fabryce danych hello.</span><span class="sxs-lookup"><span data-stu-id="6592d-146">Create a **pipeline** in hello data factory.</span></span> <span data-ttu-id="6592d-147">W tym kroku jest tworzony potok za pomocą działania kopiowania.</span><span class="sxs-lookup"><span data-stu-id="6592d-147">In this step, you create a pipeline with a copy activity.</span></span>   
    
    <span data-ttu-id="6592d-148">działanie kopiowania Hello kopiuje dane z obiektu blob w tabeli tooa magazynu obiektów blob platformy Azure hello w bazie danych Azure SQL hello.</span><span class="sxs-lookup"><span data-stu-id="6592d-148">hello copy activity copies data from a blob in hello Azure blob storage tooa table in hello Azure SQL database.</span></span> <span data-ttu-id="6592d-149">Działanie kopiowania służy w potoku danych toocopy z dowolnego miejsca docelowego tooany obsługiwane obsługiwanej źródłowej.</span><span class="sxs-lookup"><span data-stu-id="6592d-149">You can use a copy activity in a pipeline toocopy data from any supported source tooany supported destination.</span></span> <span data-ttu-id="6592d-150">Listę obsługiwanych magazynów danych można znaleźć w artykule [Działania związane z przenoszeniem danych](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="6592d-150">For a list of supported data stores, see [data movement activities](data-factory-data-movement-activities.md#supported-data-stores-and-formats) article.</span></span> 
5. <span data-ttu-id="6592d-151">Monitor hello potoku.</span><span class="sxs-lookup"><span data-stu-id="6592d-151">Monitor hello pipeline.</span></span> <span data-ttu-id="6592d-152">W tym kroku zostanie **monitor** hello wycinków wejściowych i wyjściowych zestawów danych przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6592d-152">In this step, you **monitor** hello slices of input and output datasets by using PowerShell.</span></span>

## <a name="create-a-data-factory"></a><span data-ttu-id="6592d-153">Tworzenie fabryki danych</span><span class="sxs-lookup"><span data-stu-id="6592d-153">Create a data factory</span></span>
> [!IMPORTANT]
> <span data-ttu-id="6592d-154">Pełne [wymagania wstępne dotyczące samouczka hello](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) Jeśli jeszcze tego nie zrobiono.</span><span class="sxs-lookup"><span data-stu-id="6592d-154">Complete [prerequisites for hello tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) if you haven't already done so.</span></span>   

<span data-ttu-id="6592d-155">Fabryka danych może obejmować jeden lub wiele potoków.</span><span class="sxs-lookup"><span data-stu-id="6592d-155">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="6592d-156">Potok może obejmować jedno lub wiele działań.</span><span class="sxs-lookup"><span data-stu-id="6592d-156">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="6592d-157">Na przykład toocopy działanie kopiowania danych z magazynu danych docelowy tooa źródłowego i HDInsight Hive działania toorun tootransform skryptu Hive wejściowe dane wyjściowe tooproduct danych.</span><span class="sxs-lookup"><span data-stu-id="6592d-157">For example, a Copy Activity toocopy data from a source tooa destination data store and a HDInsight Hive activity toorun a Hive script tootransform input data tooproduct output data.</span></span> <span data-ttu-id="6592d-158">Zacznijmy od utworzenia hello fabryki danych w tym kroku.</span><span class="sxs-lookup"><span data-stu-id="6592d-158">Let's start with creating hello data factory in this step.</span></span>

1. <span data-ttu-id="6592d-159">Uruchom program **PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="6592d-159">Launch **PowerShell**.</span></span> <span data-ttu-id="6592d-160">Nie zamykaj programu Azure PowerShell do momentu zakończenia hello tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="6592d-160">Keep Azure PowerShell open until hello end of this tutorial.</span></span> <span data-ttu-id="6592d-161">Zamknij i otwórz ponownie, należy najpierw polecenia hello toorun ponownie.</span><span class="sxs-lookup"><span data-stu-id="6592d-161">If you close and reopen, you need toorun hello commands again.</span></span>

    <span data-ttu-id="6592d-162">Uruchom następujące polecenie hello i wprowadź hello nazwę użytkownika i hasło, użyj toosign w toohello portalu Azure:</span><span class="sxs-lookup"><span data-stu-id="6592d-162">Run hello following command, and enter hello user name and password that you use toosign in toohello Azure portal:</span></span>

    ```PowerShell
    Login-AzureRmAccount
    ```   
   
    <span data-ttu-id="6592d-163">Uruchom następujące polecenie tooview hello wszystkie subskrypcje powitania dla tego konta:</span><span class="sxs-lookup"><span data-stu-id="6592d-163">Run hello following command tooview all hello subscriptions for this account:</span></span>

    ```PowerShell
    Get-AzureRmSubscription
    ```

    <span data-ttu-id="6592d-164">Uruchom następujące polecenie tooselect hello subskrypcję, która ma toowork z hello.</span><span class="sxs-lookup"><span data-stu-id="6592d-164">Run hello following command tooselect hello subscription that you want toowork with.</span></span> <span data-ttu-id="6592d-165">Zastąp  **&lt;NameOfAzureSubscription** &gt; o nazwie hello subskrypcji platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="6592d-165">Replace **&lt;NameOfAzureSubscription**&gt; with hello name of your Azure subscription:</span></span>

    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <NameOfAzureSubscription> | Set-AzureRmContext
    ```
2. <span data-ttu-id="6592d-166">Tworzenie grupy zasobów platformy Azure o nazwie **ADFTutorialResourceGroup** , uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="6592d-166">Create an Azure resource group named **ADFTutorialResourceGroup** by running hello following command:</span></span>

    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```
    
    <span data-ttu-id="6592d-167">Niektóre kroki hello w tym samouczku Załóżmy, że hello grupy zasobów o nazwie **ADFTutorialResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="6592d-167">Some of hello steps in this tutorial assume that you use hello resource group named **ADFTutorialResourceGroup**.</span></span> <span data-ttu-id="6592d-168">Jeśli używasz innej grupie zasobów, należy toouse go zamiast ADFTutorialResourceGroup w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="6592d-168">If you use a different resource group, you need toouse it in place of ADFTutorialResourceGroup in this tutorial.</span></span>
3. <span data-ttu-id="6592d-169">Uruchom hello **AzureRmDataFactory nowy** toocreate polecenia cmdlet fabryki danych o nazwie **ADFTutorialDataFactoryPSH**:</span><span class="sxs-lookup"><span data-stu-id="6592d-169">Run hello **New-AzureRmDataFactory** cmdlet toocreate a data factory named **ADFTutorialDataFactoryPSH**:</span></span>  

    ```PowerShell
    $df=New-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name ADFTutorialDataFactoryPSH –Location "West US"
    ```
    <span data-ttu-id="6592d-170">Ta nazwa może już być używana.</span><span class="sxs-lookup"><span data-stu-id="6592d-170">This name may already have been taken.</span></span> <span data-ttu-id="6592d-171">W związku z tym upewnić hello nazwa fabryki danych hello unikatowy przez dodanie prefiksu lub sufiksu (na przykład: ADFTutorialDataFactoryPSH05152017) i uruchom ponownie polecenie hello.</span><span class="sxs-lookup"><span data-stu-id="6592d-171">Therefore, make hello name of hello data factory unique by adding a prefix or suffix (for example: ADFTutorialDataFactoryPSH05152017) and run hello command again.</span></span>  

<span data-ttu-id="6592d-172">Należy zwrócić uwagę hello następujące punkty:</span><span class="sxs-lookup"><span data-stu-id="6592d-172">Note hello following points:</span></span>

* <span data-ttu-id="6592d-173">Nazwa fabryki danych Azure hello Hello musi być globalnie unikatowe.</span><span class="sxs-lookup"><span data-stu-id="6592d-173">hello name of hello Azure data factory must be globally unique.</span></span> <span data-ttu-id="6592d-174">Jeśli zostanie wyświetlony następujący błąd hello, Zmień nazwę hello (na przykład yournameADFTutorialDataFactoryPSH).</span><span class="sxs-lookup"><span data-stu-id="6592d-174">If you receive hello following error, change hello name (for example, yournameADFTutorialDataFactoryPSH).</span></span> <span data-ttu-id="6592d-175">Użyj tej nazwy zamiast ADFTutorialFactoryPSH podczas wykonywania kroków w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="6592d-175">Use this name in place of ADFTutorialFactoryPSH while performing steps in this tutorial.</span></span> <span data-ttu-id="6592d-176">Aby uzyskać informacje o artefaktach usługi Data Factory, zobacz artykuł [Data Factory — Naming Rules](data-factory-naming-rules.md) (Data Factory — reguły nazewnictwa).</span><span class="sxs-lookup"><span data-stu-id="6592d-176">See [Data Factory - Naming Rules](data-factory-naming-rules.md) for Data Factory artifacts.</span></span>

    ```
    Data factory name “ADFTutorialDataFactoryPSH” is not available
    ```
* <span data-ttu-id="6592d-177">toocreate wystąpienia fabryki danych, musi być współautora lub administratora hello subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6592d-177">toocreate Data Factory instances, you must be a contributor or administrator of hello Azure subscription.</span></span>
* <span data-ttu-id="6592d-178">Nazwa fabryki danych hello Hello mogą być zarejestrowana jako nazwa DNS w przyszłości hello i dlatego stać się publicznie widoczna.</span><span class="sxs-lookup"><span data-stu-id="6592d-178">hello name of hello data factory may be registered as a DNS name in hello future, and hence become publicly visible.</span></span>
* <span data-ttu-id="6592d-179">Może pojawić się hello następujący błąd: "**Ta subskrypcja nie jest zarejestrowany toouse przestrzeni nazw Microsoft.DataFactory.**"</span><span class="sxs-lookup"><span data-stu-id="6592d-179">You may receive hello following error: "**This subscription is not registered toouse namespace Microsoft.DataFactory.**"</span></span> <span data-ttu-id="6592d-180">Wykonaj jedną z następujących hello, a następnie spróbuj opublikować ponownie:</span><span class="sxs-lookup"><span data-stu-id="6592d-180">Do one of hello following, and try publishing again:</span></span>

  * <span data-ttu-id="6592d-181">W programie Azure PowerShell Uruchom hello następujące polecenia tooregister hello fabryki danych dostawcy:</span><span class="sxs-lookup"><span data-stu-id="6592d-181">In Azure PowerShell, run hello following command tooregister hello Data Factory provider:</span></span>

    ```PowerShell
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```

    <span data-ttu-id="6592d-182">Uruchom następujące polecenie tooconfirm hello tej fabryki danych w zarejestrowany dostawca hello:</span><span class="sxs-lookup"><span data-stu-id="6592d-182">Run hello following command tooconfirm that hello Data Factory provider is registered:</span></span>

    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * <span data-ttu-id="6592d-183">Zaloguj się przy użyciu hello toohello subskrypcji platformy Azure [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6592d-183">Sign in by using hello Azure subscription toohello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="6592d-184">Przejdź do bloku fabryki danych tooa lub tworzenie fabryki danych w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="6592d-184">Go tooa Data Factory blade, or create a data factory in hello Azure portal.</span></span> <span data-ttu-id="6592d-185">Ta akcja rejestruje automatycznie hello dostawcy dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="6592d-185">This action automatically registers hello provider for you.</span></span>

## <a name="create-linked-services"></a><span data-ttu-id="6592d-186">Tworzenie połączonych usług</span><span class="sxs-lookup"><span data-stu-id="6592d-186">Create linked services</span></span>
<span data-ttu-id="6592d-187">Połączone usługi są tworzone w toolink fabryki danych dane są przechowywane i obliczeniowe fabryki danych toohello usług.</span><span class="sxs-lookup"><span data-stu-id="6592d-187">You create linked services in a data factory toolink your data stores and compute services toohello data factory.</span></span> <span data-ttu-id="6592d-188">W tym samouczku nie przedstawiono korzystania z żadnych usług obliczeniowych, takich jak Azure HDInsight czy Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="6592d-188">In this tutorial, you don't use any compute service such as Azure HDInsight or Azure Data Lake Analytics.</span></span> <span data-ttu-id="6592d-189">Zostają użyte dwa magazyny danych typu Azure Storage (źródło) i Azure SQL Database (lokalizacja docelowa).</span><span class="sxs-lookup"><span data-stu-id="6592d-189">You use two data stores of type Azure Storage (source) and Azure SQL Database (destination).</span></span> 

<span data-ttu-id="6592d-190">W związku z tym tworzy się dwie połączone usługi o nazwie AzureStorageLinkedService i AzureSqlLinkedService typu: AzureStorage i AzureSqlDatabase.</span><span class="sxs-lookup"><span data-stu-id="6592d-190">Therefore, you create two linked services named AzureStorageLinkedService and AzureSqlLinkedService of types: AzureStorage and AzureSqlDatabase.</span></span>  

<span data-ttu-id="6592d-191">Witaj AzureStorageLinkedService łączy fabrykę danych toohello konta magazynu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6592d-191">hello AzureStorageLinkedService links your Azure storage account toohello data factory.</span></span> <span data-ttu-id="6592d-192">To konto magazynu jest hello jedną w którym utworzono kontener i hello dane przekazane jako część [wymagania wstępne](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="6592d-192">This storage account is hello one in which you created a container and uploaded hello data as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>   

<span data-ttu-id="6592d-193">AzureSqlLinkedService łączy fabrykę danych toohello bazy danych Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="6592d-193">AzureSqlLinkedService links your Azure SQL database toohello data factory.</span></span> <span data-ttu-id="6592d-194">dane Hello, który jest skopiowany z magazynu obiektów blob hello są przechowywane w tej bazie danych.</span><span class="sxs-lookup"><span data-stu-id="6592d-194">hello data that is copied from hello blob storage is stored in this database.</span></span> <span data-ttu-id="6592d-195">Utworzono hello pustych elementów tabeli w tej bazie danych jako część [wymagania wstępne](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="6592d-195">You created hello emp table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span> 

### <a name="create-a-linked-service-for-an-azure-storage-account"></a><span data-ttu-id="6592d-196">Tworzenie połączonej usługi dla konta magazynu Azure</span><span class="sxs-lookup"><span data-stu-id="6592d-196">Create a linked service for an Azure storage account</span></span>
<span data-ttu-id="6592d-197">W tym kroku możesz połączyć fabrykę danych tooyour konta magazynu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6592d-197">In this step, you link your Azure storage account tooyour data factory.</span></span>

1. <span data-ttu-id="6592d-198">Utwórz plik JSON o nazwie **AzureStorageLinkedService.json** w **C:\ADFGetStartedPSH** folder o hello następującej zawartości: (Utwórz hello folder ADFGetStartedPSH, jeśli jeszcze nie istnieje).</span><span class="sxs-lookup"><span data-stu-id="6592d-198">Create a JSON file named **AzureStorageLinkedService.json** in **C:\ADFGetStartedPSH** folder with hello following content: (Create hello folder ADFGetStartedPSH if it does not already exist.)</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="6592d-199">Zastąp &lt;accountname&gt; i &lt;accountkey&gt; z nazwy i klucza konta magazynu Azure przed zapisaniem pliku hello.</span><span class="sxs-lookup"><span data-stu-id="6592d-199">Replace &lt;accountname&gt; and &lt;accountkey&gt; with name and key of your Azure storage account before saving hello file.</span></span> 

    ```json
    {
        "name": "AzureStorageLinkedService",
        "properties": {
            "type": "AzureStorage",
            "typeProperties": {
                "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
            }
        }
     }
    ``` 
2. <span data-ttu-id="6592d-200">W **programu Azure PowerShell**, Przełącz toohello **ADFGetStartedPSH** folderu.</span><span class="sxs-lookup"><span data-stu-id="6592d-200">In **Azure PowerShell**, switch toohello **ADFGetStartedPSH** folder.</span></span>
4. <span data-ttu-id="6592d-201">Uruchom hello **AzureRmDataFactoryLinkedService nowy** hello toocreate polecenia cmdlet połączonej usługi: **AzureStorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="6592d-201">Run hello **New-AzureRmDataFactoryLinkedService** cmdlet toocreate hello linked service: **AzureStorageLinkedService**.</span></span> <span data-ttu-id="6592d-202">To polecenie cmdlet i innych poleceń cmdlet z fabryki danych użycia w ramach tego samouczka wymaga wartości toopass dla hello **ResourceGroupName** i **DataFactoryName** parametrów.</span><span class="sxs-lookup"><span data-stu-id="6592d-202">This cmdlet, and other Data Factory cmdlets you use in this tutorial requires you toopass values for hello **ResourceGroupName** and **DataFactoryName** parameters.</span></span> <span data-ttu-id="6592d-203">Alternatywnie można przekazać obiektu DataFactory hello zwróconych przez polecenie cmdlet New-AzureRmDataFactory hello bez wprowadzania ResourceGroupName i DataFactoryName każdorazowo po uruchomieniu polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="6592d-203">Alternatively, you can pass hello DataFactory object returned by hello New-AzureRmDataFactory cmdlet without typing ResourceGroupName and DataFactoryName each time you run a cmdlet.</span></span> 

    ```PowerShell
    New-AzureRmDataFactoryLinkedService $df -File .\AzureStorageLinkedService.json
    ```
    <span data-ttu-id="6592d-204">Oto hello przykładowe dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="6592d-204">Here is hello sample output:</span></span>

    ```
    LinkedServiceName : AzureStorageLinkedService
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    Properties        : Microsoft.Azure.Management.DataFactories.Models.LinkedServiceProperties
    ProvisioningState : Succeeded
    ``` 

    <span data-ttu-id="6592d-205">Inny sposób tworzenia tej połączonej usługi jest nazwa grupy zasobów toospecify i nazwa fabryki danych zamiast określania obiektu DataFactory hello.</span><span class="sxs-lookup"><span data-stu-id="6592d-205">Other way of creating this linked service is toospecify resource group name and data factory name instead of specifying hello DataFactory object.</span></span>  

    ```PowerShell
    New-AzureRmDataFactoryLinkedService -ResourceGroupName ADFTutorialResourceGroup -DataFactoryName <Name of your data factory> -File .\AzureStorageLinkedService.json
    ```

### <a name="create-a-linked-service-for-an-azure-sql-database"></a><span data-ttu-id="6592d-206">Tworzenie połączonej usługi dla bazy danych SQL Azure</span><span class="sxs-lookup"><span data-stu-id="6592d-206">Create a linked service for an Azure SQL database</span></span>
<span data-ttu-id="6592d-207">W tym kroku możesz połączyć fabrykę danych tooyour bazy danych Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="6592d-207">In this step, you link your Azure SQL database tooyour data factory.</span></span>

1. <span data-ttu-id="6592d-208">Utwórz plik JSON o nazwie AzureSqlLinkedService.json w folderze C:\ADFGetStartedPSH z hello następującej zawartości:</span><span class="sxs-lookup"><span data-stu-id="6592d-208">Create a JSON file named AzureSqlLinkedService.json in C:\ADFGetStartedPSH folder with hello following content:</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="6592d-209">Zastąp wartości &lt;servername&gt;, &lt;databasename&gt;, &lt;username@servername&gt; oraz &lt;password&gt; nazwą serwera SQL Azure, nazwą bazy danych, nazwą użytkownika i hasłem.</span><span class="sxs-lookup"><span data-stu-id="6592d-209">Replace &lt;servername&gt;, &lt;databasename&gt;, &lt;username@servername&gt;, and &lt;password&gt; with names of your Azure SQL server, database, user account, and password.</span></span>
    
    ```json
    {
        "name": "AzureSqlLinkedService",
        "properties": {
            "type": "AzureSqlDatabase",
            "typeProperties": {
                "connectionString": "Server=tcp:<server>.database.windows.net,1433;Database=<databasename>;User ID=<user>@<server>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
            }
        }
     }
    ```
2. <span data-ttu-id="6592d-210">Uruchom następujące polecenie toocreate hello połączonej usługi:</span><span class="sxs-lookup"><span data-stu-id="6592d-210">Run hello following command toocreate a linked service:</span></span>

    ```PowerShell
    New-AzureRmDataFactoryLinkedService $df -File .\AzureSqlLinkedService.json
    ```
    
    <span data-ttu-id="6592d-211">Oto hello przykładowe dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="6592d-211">Here is hello sample output:</span></span>

    ```
    LinkedServiceName : AzureSqlLinkedService
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    Properties        : Microsoft.Azure.Management.DataFactories.Models.LinkedServiceProperties
    ProvisioningState : Succeeded
    ```

   <span data-ttu-id="6592d-212">Upewnij się, że **dostęp do usług tooAzure** opcja jest włączona dla Twojej bazy danych programu SQL server.</span><span class="sxs-lookup"><span data-stu-id="6592d-212">Confirm that **Allow access tooAzure services** setting is turned on for your SQL database server.</span></span> <span data-ttu-id="6592d-213">tooverify i włącz ją, hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="6592d-213">tooverify and turn it on, do hello following steps:</span></span>

    1. <span data-ttu-id="6592d-214">Zaloguj się za toohello [portalu Azure](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="6592d-214">Log in toohello [Azure portal](https://portal.azure.com)</span></span>
    2. <span data-ttu-id="6592d-215">Kliknij przycisk **więcej usług >** na powitania po lewej, a następnie kliknij **serwerów SQL** w hello **baz danych** kategorii.</span><span class="sxs-lookup"><span data-stu-id="6592d-215">Click **More services >** on hello left, and click **SQL servers** in hello **DATABASES** category.</span></span>
    3. <span data-ttu-id="6592d-216">Wybierz serwer, na liście hello programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="6592d-216">Select your server in hello list of SQL servers.</span></span>
    4. <span data-ttu-id="6592d-217">W bloku serwera SQL hello, kliknij polecenie **Pokaż ustawienia zapory** łącza.</span><span class="sxs-lookup"><span data-stu-id="6592d-217">On hello SQL server blade, click **Show firewall settings** link.</span></span>
    5. <span data-ttu-id="6592d-218">W hello **ustawienia zapory** bloku, kliknij przycisk **ON** dla **dostęp do usług tooAzure**.</span><span class="sxs-lookup"><span data-stu-id="6592d-218">In hello **Firewall settings** blade, click **ON** for **Allow access tooAzure services**.</span></span>
    6. <span data-ttu-id="6592d-219">Kliknij przycisk **zapisać** na powitania narzędzi.</span><span class="sxs-lookup"><span data-stu-id="6592d-219">Click **Save** on hello toolbar.</span></span> 

## <a name="create-datasets"></a><span data-ttu-id="6592d-220">Tworzenie zestawów danych</span><span class="sxs-lookup"><span data-stu-id="6592d-220">Create datasets</span></span>
<span data-ttu-id="6592d-221">W poprzednim kroku hello utworzono toolink połączone usługi konta magazynu Azure i fabryki danych tooyour bazy danych Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="6592d-221">In hello previous step, you created linked services toolink your Azure Storage account and Azure SQL database tooyour data factory.</span></span> <span data-ttu-id="6592d-222">W tym kroku należy zdefiniować dwa zestawy danych o nazwie InputDataset i OutputDataset reprezentujące danych wejściowych i wyjściowych danych przechowywanych w magazynach danych hello odwołuje się AzureStorageLinkedService i AzureSqlLinkedService odpowiednio.</span><span class="sxs-lookup"><span data-stu-id="6592d-222">In this step, you define two datasets named InputDataset and OutputDataset that represent input and output data that is stored in hello data stores referred by AzureStorageLinkedService and AzureSqlLinkedService respectively.</span></span>

<span data-ttu-id="6592d-223">Hello Azure połączoną usługą magazynu określa parametry połączenia hello, która używa usługi fabryka danych w czasie wykonywania tooconnect tooyour kontem magazynu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6592d-223">hello Azure storage linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="6592d-224">I zestawu danych wejściowych obiektu blob hello (InputDataset) określa hello kontenera i folderu hello, który zawiera hello danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="6592d-224">And, hello input blob dataset (InputDataset) specifies hello container and hello folder that contains hello input data.</span></span>  

<span data-ttu-id="6592d-225">Podobnie hello usługi baza danych SQL Azure połączone określa hello parametry połączenia, które korzysta z usługi fabryka danych w czasie wykonywania tooconnect tooyour — bazy danych Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="6592d-225">Similarly, hello Azure SQL Database linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure SQL database.</span></span> <span data-ttu-id="6592d-226">I hello danych wyjściowych SQL tabeli dataset (OututDataset) określa hello tabeli w hello bazy danych toowhich powitalne dane z magazynu obiektów blob hello są kopiowane.</span><span class="sxs-lookup"><span data-stu-id="6592d-226">And, hello output SQL table dataset (OututDataset) specifies hello table in hello database toowhich hello data from hello blob storage is copied.</span></span> 

### <a name="create-an-input-dataset"></a><span data-ttu-id="6592d-227">Tworzenie wejściowego zestawu danych</span><span class="sxs-lookup"><span data-stu-id="6592d-227">Create an input dataset</span></span>
<span data-ttu-id="6592d-228">W tym kroku utworzysz zestaw danych o nazwie InputDataset, który wskazuje plik obiektu blob tooa (emp.txt) w folderze głównym hello kontenera obiektów blob (adftutorial) w hello reprezentowany przez hello AzureStorageLinkedService połączone usługi Magazyn Azure.</span><span class="sxs-lookup"><span data-stu-id="6592d-228">In this step, you create a dataset named InputDataset that points tooa blob file (emp.txt) in hello root folder of a blob container (adftutorial) in hello Azure Storage represented by hello AzureStorageLinkedService linked service.</span></span> <span data-ttu-id="6592d-229">Brak określić wartość dla nazwy pliku hello (lub Pomiń je), danych z wszystkich obiektów blob w folderze wejściowych hello są skopiowanych toohello docelowego.</span><span class="sxs-lookup"><span data-stu-id="6592d-229">If you don't specify a value for hello fileName (or skip it), data from all blobs in hello input folder are copied toohello destination.</span></span> <span data-ttu-id="6592d-230">W tym samouczku należy określić wartość dla hello fileName.</span><span class="sxs-lookup"><span data-stu-id="6592d-230">In this tutorial, you specify a value for hello fileName.</span></span>  

1. <span data-ttu-id="6592d-231">Utwórz plik JSON o nazwie **InputDataset.json** w hello **C:\ADFGetStartedPSH** folder z hello następującej zawartości:</span><span class="sxs-lookup"><span data-stu-id="6592d-231">Create a JSON file named **InputDataset.json** in hello **C:\ADFGetStartedPSH** folder, with hello following content:</span></span>

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
            "linkedServiceName": "AzureStorageLinkedService",
            "typeProperties": {
                "fileName": "emp.txt",
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

    <span data-ttu-id="6592d-232">Witaj Poniższa tabela zawiera opisy właściwości JSON hello używane we fragmencie hello:</span><span class="sxs-lookup"><span data-stu-id="6592d-232">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

    | <span data-ttu-id="6592d-233">Właściwość</span><span class="sxs-lookup"><span data-stu-id="6592d-233">Property</span></span> | <span data-ttu-id="6592d-234">Opis</span><span class="sxs-lookup"><span data-stu-id="6592d-234">Description</span></span> |
    |:--- |:--- |
    | <span data-ttu-id="6592d-235">type</span><span class="sxs-lookup"><span data-stu-id="6592d-235">type</span></span> | <span data-ttu-id="6592d-236">Właściwość type Hello ustawiono zbyt**AzureBlob** ponieważ danych znajduje się w magazynie obiektów blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6592d-236">hello type property is set too**AzureBlob** because data resides in an Azure blob storage.</span></span> |
    | <span data-ttu-id="6592d-237">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="6592d-237">linkedServiceName</span></span> | <span data-ttu-id="6592d-238">Odwołuje się toohello **AzureStorageLinkedService** utworzony wcześniej.</span><span class="sxs-lookup"><span data-stu-id="6592d-238">Refers toohello **AzureStorageLinkedService** that you created earlier.</span></span> |
    | <span data-ttu-id="6592d-239">folderPath</span><span class="sxs-lookup"><span data-stu-id="6592d-239">folderPath</span></span> | <span data-ttu-id="6592d-240">Określa obiekt blob hello **kontenera** i hello **folderu** zawiera obiekty BLOB wejściowego.</span><span class="sxs-lookup"><span data-stu-id="6592d-240">Specifies hello blob **container** and hello **folder** that contains input blobs.</span></span> <span data-ttu-id="6592d-241">W tym samouczku adftutorial jest hello kontenera obiektów blob i hello folderu głównego.</span><span class="sxs-lookup"><span data-stu-id="6592d-241">In this tutorial, adftutorial is hello blob container and folder is hello root folder.</span></span> | 
    | <span data-ttu-id="6592d-242">fileName</span><span class="sxs-lookup"><span data-stu-id="6592d-242">fileName</span></span> | <span data-ttu-id="6592d-243">Ta właściwość jest opcjonalna.</span><span class="sxs-lookup"><span data-stu-id="6592d-243">This property is optional.</span></span> <span data-ttu-id="6592d-244">W przypadku pominięcia tej właściwości, pobierane są wszystkie pliki z hello folderPath.</span><span class="sxs-lookup"><span data-stu-id="6592d-244">If you omit this property, all files from hello folderPath are picked.</span></span> <span data-ttu-id="6592d-245">W tym samouczku **emp.txt** określona dla hello nazwę pliku, tak aby plik zostaje pobrana do przetwarzania.</span><span class="sxs-lookup"><span data-stu-id="6592d-245">In this tutorial, **emp.txt** is specified for hello fileName, so only that file is picked up for processing.</span></span> |
    | <span data-ttu-id="6592d-246">format -> type</span><span class="sxs-lookup"><span data-stu-id="6592d-246">format -> type</span></span> |<span data-ttu-id="6592d-247">Plik wejściowy Hello jest w formacie tekstowym hello, więc używamy **TextFormat**.</span><span class="sxs-lookup"><span data-stu-id="6592d-247">hello input file is in hello text format, so we use **TextFormat**.</span></span> |
    | <span data-ttu-id="6592d-248">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="6592d-248">columnDelimiter</span></span> | <span data-ttu-id="6592d-249">Witaj kolumn w pliku wejściowym hello są rozdzielane **przecinka (`,`)**.</span><span class="sxs-lookup"><span data-stu-id="6592d-249">hello columns in hello input file are delimited by **comma character (`,`)**.</span></span> |
    | <span data-ttu-id="6592d-250">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="6592d-250">frequency/interval</span></span> | <span data-ttu-id="6592d-251">częstotliwość Hello ustawiono zbyt**godzina** i interwał jest ustawiany za**1**, co oznacza, że hello wejściowych dostępnych wycinków **co godzinę**.</span><span class="sxs-lookup"><span data-stu-id="6592d-251">hello frequency is set too**Hour** and interval is  set too**1**, which means that hello input slices are available **hourly**.</span></span> <span data-ttu-id="6592d-252">Innymi słowy, hello usługi fabryka danych sprawdza dane wejściowe co godzinę w folderze głównym hello kontenera obiektów blob (**adftutorial**) określone.</span><span class="sxs-lookup"><span data-stu-id="6592d-252">In other words, hello Data Factory service looks for input data every hour in hello root folder of blob container (**adftutorial**) you specified.</span></span> <span data-ttu-id="6592d-253">Wyszukuje hello danych w ramach hello potoku rozpoczęcia i zakończenia godzin, nie przed lub po tych godzinach.</span><span class="sxs-lookup"><span data-stu-id="6592d-253">It looks for hello data within hello pipeline start and end times, not before or after these times.</span></span>  |
    | <span data-ttu-id="6592d-254">external</span><span class="sxs-lookup"><span data-stu-id="6592d-254">external</span></span> | <span data-ttu-id="6592d-255">Ta właściwość jest ustawiona zbyt**true** czy hello danych nie jest generowany przez tego potoku.</span><span class="sxs-lookup"><span data-stu-id="6592d-255">This property is set too**true** if hello data is not generated by this pipeline.</span></span> <span data-ttu-id="6592d-256">Witaj danych wejściowych w tym samouczku jest hello emp.txt pliku, który nie jest generowany w tym potoku, możemy ustawić tootrue tej właściwości.</span><span class="sxs-lookup"><span data-stu-id="6592d-256">hello input data in this tutorial is in hello emp.txt file, which is not generated by this pipeline, so we set this property tootrue.</span></span> |

    <span data-ttu-id="6592d-257">Aby uzyskać więcej informacji o tych właściwościach JSON, zobacz [artykuł dotyczący łącznika obiektu blob platformy Azure](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="6592d-257">For more information about these JSON properties, see [Azure Blob connector article](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
2. <span data-ttu-id="6592d-258">Uruchom hello następujące polecenia toocreate hello fabryki danych w zestawie danych.</span><span class="sxs-lookup"><span data-stu-id="6592d-258">Run hello following command toocreate hello Data Factory dataset.</span></span>

    ```PowerShell  
    New-AzureRmDataFactoryDataset $df -File .\InputDataset.json
    ```
    <span data-ttu-id="6592d-259">Oto hello przykładowe dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="6592d-259">Here is hello sample output:</span></span>

    ```
    DatasetName       : InputDataset
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    Availability      : Microsoft.Azure.Management.DataFactories.Common.Models.Availability
    Location          : Microsoft.Azure.Management.DataFactories.Models.AzureBlobDataset
    Policy            : Microsoft.Azure.Management.DataFactories.Common.Models.Policy
    Structure         : {FirstName, LastName}
    Properties        : Microsoft.Azure.Management.DataFactories.Models.DatasetProperties
    ProvisioningState : Succeeded
    ```

### <a name="create-an-output-dataset"></a><span data-ttu-id="6592d-260">Tworzenie wyjściowego zestawu danych</span><span class="sxs-lookup"><span data-stu-id="6592d-260">Create an output dataset</span></span>
<span data-ttu-id="6592d-261">W tej części krok hello utworzyć wyjściowy zestaw danych o nazwie **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="6592d-261">In this part of hello step, you create an output dataset named **OutputDataset**.</span></span> <span data-ttu-id="6592d-262">Ten zestaw danych wskazuje tooa tabeli SQL w bazie danych Azure SQL hello reprezentowany przez **AzureSqlLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="6592d-262">This dataset points tooa SQL table in hello Azure SQL database represented by **AzureSqlLinkedService**.</span></span> 

1. <span data-ttu-id="6592d-263">Utwórz plik JSON o nazwie **OutputDataset.json** w hello **C:\ADFGetStartedPSH** folder o hello następującej zawartości:</span><span class="sxs-lookup"><span data-stu-id="6592d-263">Create a JSON file named **OutputDataset.json** in hello **C:\ADFGetStartedPSH** folder with hello following content:</span></span>

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
            "linkedServiceName": "AzureSqlLinkedService",
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

    <span data-ttu-id="6592d-264">Witaj Poniższa tabela zawiera opisy właściwości JSON hello używane we fragmencie hello:</span><span class="sxs-lookup"><span data-stu-id="6592d-264">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

    | <span data-ttu-id="6592d-265">Właściwość</span><span class="sxs-lookup"><span data-stu-id="6592d-265">Property</span></span> | <span data-ttu-id="6592d-266">Opis</span><span class="sxs-lookup"><span data-stu-id="6592d-266">Description</span></span> |
    |:--- |:--- |
    | <span data-ttu-id="6592d-267">type</span><span class="sxs-lookup"><span data-stu-id="6592d-267">type</span></span> | <span data-ttu-id="6592d-268">Właściwość type Hello ustawiono zbyt**AzureSqlTable** , ponieważ dane są kopiowane tooa tabeli w bazie danych Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="6592d-268">hello type property is set too**AzureSqlTable** because data is copied tooa table in an Azure SQL database.</span></span> |
    | <span data-ttu-id="6592d-269">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="6592d-269">linkedServiceName</span></span> | <span data-ttu-id="6592d-270">Odwołuje się toohello **AzureSqlLinkedService** utworzony wcześniej.</span><span class="sxs-lookup"><span data-stu-id="6592d-270">Refers toohello **AzureSqlLinkedService** that you created earlier.</span></span> |
    | <span data-ttu-id="6592d-271">tableName</span><span class="sxs-lookup"><span data-stu-id="6592d-271">tableName</span></span> | <span data-ttu-id="6592d-272">Określony hello **tabeli** toowhich hello dane są kopiowane.</span><span class="sxs-lookup"><span data-stu-id="6592d-272">Specified hello **table** toowhich hello data is copied.</span></span> | 
    | <span data-ttu-id="6592d-273">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="6592d-273">frequency/interval</span></span> | <span data-ttu-id="6592d-274">Witaj częstotliwość ustawiono zbyt**godzina** i interwał **1**, co oznacza, że wycinki danych wyjściowych hello są produkowane **co godzinę** między hello potoku rozpoczęcia i zakończenia godzin przed nie lub Po tych godzinach.</span><span class="sxs-lookup"><span data-stu-id="6592d-274">hello frequency is set too**Hour** and interval is **1**, which means that hello output slices are produced **hourly** between hello pipeline start and end times, not before or after these times.</span></span>  |

    <span data-ttu-id="6592d-275">Istnieją trzy kolumny — **identyfikator**, **imię**, i **nazwisko** — Witaj pustych elementów tabeli w bazie danych hello.</span><span class="sxs-lookup"><span data-stu-id="6592d-275">There are three columns – **ID**, **FirstName**, and **LastName** – in hello emp table in hello database.</span></span> <span data-ttu-id="6592d-276">Identyfikator jest kolumny tożsamości, więc musisz tylko toospecify **imię** i **nazwisko** tutaj.</span><span class="sxs-lookup"><span data-stu-id="6592d-276">ID is an identity column, so you need toospecify only **FirstName** and **LastName** here.</span></span>

    <span data-ttu-id="6592d-277">Aby uzyskać więcej informacji o tych właściwościach JSON, zobacz [artykuł dotyczący łącznika usługi Azure SQL](data-factory-azure-sql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="6592d-277">For more information about these JSON properties, see [Azure SQL connector article](data-factory-azure-sql-connector.md#dataset-properties).</span></span>
2. <span data-ttu-id="6592d-278">Hello uruchom następujące polecenie toocreate hello data factory w zestawie danych.</span><span class="sxs-lookup"><span data-stu-id="6592d-278">Run hello following command toocreate hello data factory dataset.</span></span>

    ```PowerShell   
    New-AzureRmDataFactoryDataset $df -File .\OutputDataset.json
    ```

    <span data-ttu-id="6592d-279">Oto hello przykładowe dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="6592d-279">Here is hello sample output:</span></span>

    ```
    DatasetName       : OutputDataset
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    Availability      : Microsoft.Azure.Management.DataFactories.Common.Models.Availability
    Location          : Microsoft.Azure.Management.DataFactories.Models.AzureSqlTableDataset
    Policy            :
    Structure         : {FirstName, LastName}
    Properties        : Microsoft.Azure.Management.DataFactories.Models.DatasetProperties
    ProvisioningState : Succeeded
    ```

## <a name="create-a-pipeline"></a><span data-ttu-id="6592d-280">Tworzenie potoku</span><span class="sxs-lookup"><span data-stu-id="6592d-280">Create a pipeline</span></span>
<span data-ttu-id="6592d-281">W tym kroku opisano tworzenie potoku za pomocą **działania kopiowania**, w którym parametr **InputDataset** jest używany jako dane wejściowe, a parametr **OutputDataset** jako dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="6592d-281">In this step, you create a pipeline with a **copy activity** that uses **InputDataset** as an input and **OutputDataset** as an output.</span></span>

<span data-ttu-id="6592d-282">Wyjściowy zestaw danych jest obecnie, jakie dysków hello harmonogramu.</span><span class="sxs-lookup"><span data-stu-id="6592d-282">Currently, output dataset is what drives hello schedule.</span></span> <span data-ttu-id="6592d-283">W tym samouczku wyjściowy zestaw danych jest skonfigurowane tooproduce wycinek godzinę.</span><span class="sxs-lookup"><span data-stu-id="6592d-283">In this tutorial, output dataset is configured tooproduce a slice once an hour.</span></span> <span data-ttu-id="6592d-284">potok Hello ma czas rozpoczęcia i godzina zakończenia, będące w ciągu jednego dnia od siebie, który wynosi 24 godziny.</span><span class="sxs-lookup"><span data-stu-id="6592d-284">hello pipeline has a start time and end time that are one day apart, which is 24 hours.</span></span> <span data-ttu-id="6592d-285">W związku z tym 24 wycinków wyjściowy zestaw danych są produkowane przez hello potoku.</span><span class="sxs-lookup"><span data-stu-id="6592d-285">Therefore, 24 slices of output dataset are produced by hello pipeline.</span></span> 


1. <span data-ttu-id="6592d-286">Utwórz plik JSON o nazwie **ADFTutorialPipeline.json** w hello **C:\ADFGetStartedPSH** folder z hello następującej zawartości:</span><span class="sxs-lookup"><span data-stu-id="6592d-286">Create a JSON file named **ADFTutorialPipeline.json** in hello **C:\ADFGetStartedPSH** folder, with hello following content:</span></span>

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
              "retry": 0,
              "timeout": "01:00:00"
            }
          }
        ],
        "start": "2017-05-11T00:00:00Z",
        "end": "2017-05-12T00:00:00Z"
      }
    } 
    ```
    <span data-ttu-id="6592d-287">Należy zwrócić uwagę hello następujące punkty:</span><span class="sxs-lookup"><span data-stu-id="6592d-287">Note hello following points:</span></span>
   
    - <span data-ttu-id="6592d-288">W sekcji działania hello jest tylko jedno działanie którego **typu** ustawiono zbyt**kopiowania**.</span><span class="sxs-lookup"><span data-stu-id="6592d-288">In hello activities section, there is only one activity whose **type** is set too**Copy**.</span></span> <span data-ttu-id="6592d-289">Aby uzyskać więcej informacji o działaniu kopiowania hello, zobacz [działań przepływu danych](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="6592d-289">For more information about hello copy activity, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="6592d-290">W rozwiązaniach usługi Data Factory można również użyć [działań dotyczących przekształcania danych](data-factory-data-transformation-activities.md).</span><span class="sxs-lookup"><span data-stu-id="6592d-290">In Data Factory solutions, you can also use [data transformation activities](data-factory-data-transformation-activities.md).</span></span>
    - <span data-ttu-id="6592d-291">Dane wejściowe dla działania hello jest ustawiony za**InputDataset** i danych wyjściowych dla działania hello jest ustawiony za**OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="6592d-291">Input for hello activity is set too**InputDataset** and output for hello activity is set too**OutputDataset**.</span></span> 
    - <span data-ttu-id="6592d-292">W hello **typeProperties** sekcji **BlobSource** jest określony jako typ źródła hello i **SqlSink** jest określony jako typ ujścia hello.</span><span class="sxs-lookup"><span data-stu-id="6592d-292">In hello **typeProperties** section, **BlobSource** is specified as hello source type and **SqlSink** is specified as hello sink type.</span></span> <span data-ttu-id="6592d-293">Aby uzyskać pełną listę obsługiwanych przez działanie kopiowania hello jako źródła i wychwytywanie magazyny danych, zobacz [obsługiwane magazyny danych](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="6592d-293">For a complete list of data stores supported by hello copy activity as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="6592d-294">toolearn jak przechowywać toouse określonych danych obsługiwane jako źródło/ujście, kliknij łącze hello hello tabeli.</span><span class="sxs-lookup"><span data-stu-id="6592d-294">toolearn how toouse a specific supported data store as a source/sink, click hello link in hello table.</span></span>  
     
    <span data-ttu-id="6592d-295">Zastąp wartość hello hello **start** właściwość o hello bieżącego dnia i **zakończenia** wartości z hello następnego dnia.</span><span class="sxs-lookup"><span data-stu-id="6592d-295">Replace hello value of hello **start** property with hello current day and **end** value with hello next day.</span></span> <span data-ttu-id="6592d-296">Można określić tylko część daty hello i Pomiń hello czas część hello Data i godzina.</span><span class="sxs-lookup"><span data-stu-id="6592d-296">You can specify only hello date part and skip hello time part of hello date time.</span></span> <span data-ttu-id="6592d-297">Na przykład "2016-02-03", która odpowiada za "2016-02-03T00:00:00Z"</span><span class="sxs-lookup"><span data-stu-id="6592d-297">For example, "2016-02-03", which is equivalent too"2016-02-03T00:00:00Z"</span></span>
     
    <span data-ttu-id="6592d-298">Zarówno data/godzina rozpoczęcia, jak i data/godzina zakończenia muszą być w [formacie ISO](http://en.wikipedia.org/wiki/ISO_8601).</span><span class="sxs-lookup"><span data-stu-id="6592d-298">Both start and end datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="6592d-299">Przykładowo: 2016-10-14T16:32:41Z.</span><span class="sxs-lookup"><span data-stu-id="6592d-299">For example: 2016-10-14T16:32:41Z.</span></span> <span data-ttu-id="6592d-300">Witaj **zakończenia** czasu jest opcjonalne, ale możemy użyć w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="6592d-300">hello **end** time is optional, but we use it in this tutorial.</span></span> 
     
    <span data-ttu-id="6592d-301">Jeśli nie określisz wartości hello **zakończenia** właściwości, jest on obliczany jako "**start + 48 godzin**".</span><span class="sxs-lookup"><span data-stu-id="6592d-301">If you do not specify value for hello **end** property, it is calculated as "**start + 48 hours**".</span></span> <span data-ttu-id="6592d-302">potok hello toorun przez czas nieokreślony, określ **9999-09-09** jako wartość hello hello **zakończenia** właściwości.</span><span class="sxs-lookup"><span data-stu-id="6592d-302">toorun hello pipeline indefinitely, specify **9999-09-09** as hello value for hello **end** property.</span></span>
     
    <span data-ttu-id="6592d-303">W hello poprzedzających przykład istnieją 24 wycinków danych, jak każdy wycinek danych jest tworzone co godzinę.</span><span class="sxs-lookup"><span data-stu-id="6592d-303">In hello preceding example, there are 24 data slices as each data slice is produced hourly.</span></span>

    <span data-ttu-id="6592d-304">Opisy właściwości JSON w definicji potoku znajdują się w artykule dotyczącym [tworzenia potoków](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="6592d-304">For descriptions of JSON properties in a pipeline definition, see [create pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="6592d-305">Opisy właściwości JSON w definicji działania kopiowania znajdują się w artykule dotyczącym [działań związanych z przenoszeniem danych](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="6592d-305">For descriptions of JSON properties in a copy activity definition, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="6592d-306">Opisy właściwości JSON obsługiwanych przez BlobSource można znaleźć w [artykule dotyczącym łącznika usługi Azure Blob](data-factory-azure-blob-connector.md).</span><span class="sxs-lookup"><span data-stu-id="6592d-306">For descriptions of JSON properties supported by BlobSource, see [Azure Blob connector article](data-factory-azure-blob-connector.md).</span></span> <span data-ttu-id="6592d-307">Opisy właściwości JSON obsługiwanych przez SqlSink można znaleźć w artykule [dotyczącym łącznika usługi Azure SQL Database](data-factory-azure-sql-connector.md).</span><span class="sxs-lookup"><span data-stu-id="6592d-307">For descriptions of JSON properties supported by SqlSink, see [Azure SQL Database connector article](data-factory-azure-sql-connector.md).</span></span>
2. <span data-ttu-id="6592d-308">Witaj uruchom następujące polecenie tabeli fabryki danych hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="6592d-308">Run hello following command toocreate hello data factory table.</span></span>

    ```PowerShell   
    New-AzureRmDataFactoryPipeline $df -File .\ADFTutorialPipeline.json
    ```

    <span data-ttu-id="6592d-309">Oto hello przykładowe dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="6592d-309">Here is hello sample output:</span></span> 

    ```
    PipelineName      : ADFTutorialPipeline
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    Properties        : Microsoft.Azure.Management.DataFactories.Models.PipelinePropertie
    ProvisioningState : Succeeded
    ```

<span data-ttu-id="6592d-310">**Gratulacje!**</span><span class="sxs-lookup"><span data-stu-id="6592d-310">**Congratulations!**</span></span> <span data-ttu-id="6592d-311">Pomyślnie utworzono fabryki danych Azure z potoku toocopy danych z bazy danych Azure SQL tooan magazynu obiektów blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6592d-311">You have successfully created an Azure data factory with a pipeline toocopy data from an Azure blob storage tooan Azure SQL database.</span></span> 

## <a name="monitor-hello-pipeline"></a><span data-ttu-id="6592d-312">Monitor hello potoku</span><span class="sxs-lookup"><span data-stu-id="6592d-312">Monitor hello pipeline</span></span>
<span data-ttu-id="6592d-313">W tym kroku użyjesz programu Azure PowerShell toomonitor co się dzieje w fabryce danych Azure.</span><span class="sxs-lookup"><span data-stu-id="6592d-313">In this step, you use Azure PowerShell toomonitor what’s going on in an Azure data factory.</span></span>

1. <span data-ttu-id="6592d-314">Zastąp &lt;DataFactoryName&gt; o nazwie hello fabryki danych i uruchom **Get-AzureRmDataFactory**i przypisz tooa dane wyjściowe hello $df zmiennej.</span><span class="sxs-lookup"><span data-stu-id="6592d-314">Replace &lt;DataFactoryName&gt; with hello name of your data factory and run **Get-AzureRmDataFactory**, and assign hello output tooa variable $df.</span></span>

    ```PowerShell  
    $df=Get-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name <DataFactoryName>
    ```

    <span data-ttu-id="6592d-315">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="6592d-315">For example:</span></span>
    ```PowerShell
    $df=Get-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name ADFTutorialDataFactoryPSH0516
    ```
    
    <span data-ttu-id="6592d-316">Następnie uruchom hello drukowania zawartości hello toosee $df następujące dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="6592d-316">Then, run print hello contents of $df toosee hello following output:</span></span> 
    
    ```
    PS C:\ADFGetStartedPSH> $df
    
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    DataFactoryId     : 6f194b34-03b3-49ab-8f03-9f8a7b9d3e30
    ResourceGroupName : ADFTutorialResourceGroup
    Location          : West US
    Tags              : {}
    Properties        : Microsoft.Azure.Management.DataFactories.Models.DataFactoryProperties
    ProvisioningState : Succeeded
    ```
2. <span data-ttu-id="6592d-317">Uruchom **Get-AzureRmDataFactorySlice** tooget szczegóły wszystkie fragmenty hello **OutputDataset**, która jest hello wyjściowego zestawu danych potoku hello.</span><span class="sxs-lookup"><span data-stu-id="6592d-317">Run **Get-AzureRmDataFactorySlice** tooget details about all slices of hello **OutputDataset**, which is hello output dataset of hello pipeline.</span></span>  

    ```PowerShell   
    Get-AzureRmDataFactorySlice $df -DatasetName OutputDataset -StartDateTime 2017-05-11T00:00:00Z
    ```

   <span data-ttu-id="6592d-318">To ustawienie powinno być zgodne hello **Start** wartość w potoku hello JSON.</span><span class="sxs-lookup"><span data-stu-id="6592d-318">This setting should match hello **Start** value in hello pipeline JSON.</span></span> <span data-ttu-id="6592d-319">Powinna zostać wyświetlona 24 wycinków, po jednej dla każdej godziny od 00: 00 z too12 bieżącego dnia hello UŻYWAM programu hello następnego dnia.</span><span class="sxs-lookup"><span data-stu-id="6592d-319">You should see 24 slices, one for each hour from 12 AM of hello current day too12 AM of hello next day.</span></span>

   <span data-ttu-id="6592d-320">Poniżej przedstawiono trzy wycinków próbki z danych wyjściowych hello:</span><span class="sxs-lookup"><span data-stu-id="6592d-320">Here are three sample slices from hello output:</span></span> 

    ``` 
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    DatasetName       : OutputDataset
    Start             : 5/11/2017 11:00:00 PM
    End               : 5/12/2017 12:00:00 AM
    RetryCount        : 0
    State             : Ready
    SubState          :
    LatencyStatus     :
    LongRetryCount    : 0

    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    DatasetName       : OutputDataset
    Start             : 5/11/2017 9:00:00 PM
    End               : 5/11/2017 10:00:00 PM
    RetryCount        : 0
    State             : InProgress
    SubState          :
    LatencyStatus     :
    LongRetryCount    : 0   

    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    DatasetName       : OutputDataset
    Start             : 5/11/2017 8:00:00 PM
    End               : 5/11/2017 9:00:00 PM
    RetryCount        : 0
    State             : Waiting
    SubState          : ConcurrencyLimit
    LatencyStatus     :
    LongRetryCount    : 0
    ```
3. <span data-ttu-id="6592d-321">Uruchom **Get-AzureRmDataFactoryRun** tooget hello szczegółów działania trwający **określonych** wycinka.</span><span class="sxs-lookup"><span data-stu-id="6592d-321">Run **Get-AzureRmDataFactoryRun** tooget hello details of activity runs for a **specific** slice.</span></span> <span data-ttu-id="6592d-322">Skopiuj wartość daty i godziny hello z danych wyjściowych hello hello poprzednie polecenie toospecify hello wartości dla parametru StartDateTime hello.</span><span class="sxs-lookup"><span data-stu-id="6592d-322">Copy hello date-time value from hello output of hello previous command toospecify hello value for hello StartDateTime parameter.</span></span> 

    ```PowerShell  
    Get-AzureRmDataFactoryRun $df -DatasetName OutputDataset -StartDateTime "5/11/2017 09:00:00 PM"
    ```

   <span data-ttu-id="6592d-323">Oto hello przykładowe dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="6592d-323">Here is hello sample output:</span></span> 

    ```
    Id                  : c0ddbd75-d0c7-4816-a775-704bbd7c7eab_636301332000000000_636301368000000000_OutputDataset
    ResourceGroupName   : ADFTutorialResourceGroup
    DataFactoryName     : ADFTutorialDataFactoryPSH0516
    DatasetName         : OutputDataset
    ProcessingStartTime : 5/16/2017 8:00:33 PM
    ProcessingEndTime   : 5/16/2017 8:01:36 PM
    PercentComplete     : 100
    DataSliceStart      : 5/11/2017 9:00:00 PM
    DataSliceEnd        : 5/11/2017 10:00:00 PM
    Status              : Succeeded
    Timestamp           : 5/16/2017 8:00:33 PM
    RetryAttempt        : 0
    Properties          : {}
    ErrorMessage        :
    ActivityName        : CopyFromBlobToSQL
    PipelineName        : ADFTutorialPipeline
    Type                : Copy  
    ```

<span data-ttu-id="6592d-324">Pełną dokumentację poleceń cmdlet można znaleźć w artykule [Dokumentacja poleceń cmdlet usługi Data Factory](/powershell/module/azurerm.datafactories).</span><span class="sxs-lookup"><span data-stu-id="6592d-324">For comprehensive documentation on Data Factory cmdlets, see [Data Factory Cmdlet Reference](/powershell/module/azurerm.datafactories).</span></span>

## <a name="summary"></a><span data-ttu-id="6592d-325">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="6592d-325">Summary</span></span>
<span data-ttu-id="6592d-326">W tym samouczku danych toocopy fabryki danych Azure została utworzona z bazy danych Azure SQL tooan obiektów blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6592d-326">In this tutorial, you created an Azure data factory toocopy data from an Azure blob tooan Azure SQL database.</span></span> <span data-ttu-id="6592d-327">Użyto fabryki danych hello toocreate programu PowerShell, połączone usługi, zestawy danych i potoku.</span><span class="sxs-lookup"><span data-stu-id="6592d-327">You used PowerShell toocreate hello data factory, linked services, datasets, and a pipeline.</span></span> <span data-ttu-id="6592d-328">Poniżej przedstawiono ogólne kroki hello, wykonane w tym samouczku:</span><span class="sxs-lookup"><span data-stu-id="6592d-328">Here are hello high-level steps you performed in this tutorial:</span></span>  

1. <span data-ttu-id="6592d-329">Tworzenie **fabryki danych** Azure.</span><span class="sxs-lookup"><span data-stu-id="6592d-329">Created an Azure **data factory**.</span></span>
2. <span data-ttu-id="6592d-330">Tworzenie **połączonych usług**:</span><span class="sxs-lookup"><span data-stu-id="6592d-330">Created **linked services**:</span></span>

   <span data-ttu-id="6592d-331">a.</span><span class="sxs-lookup"><span data-stu-id="6592d-331">a.</span></span> <span data-ttu-id="6592d-332">**Usługi Azure Storage** połączone konta magazynu Azure, która przechowuje dane wejściowe toolink usługi.</span><span class="sxs-lookup"><span data-stu-id="6592d-332">An **Azure Storage** linked service toolink your Azure storage account that holds input data.</span></span>     
   <span data-ttu-id="6592d-333">b.</span><span class="sxs-lookup"><span data-stu-id="6592d-333">b.</span></span> <span data-ttu-id="6592d-334">**Azure SQL** połączone usługi toolink Twojej bazy danych SQL, która przechowuje dane wyjściowe hello.</span><span class="sxs-lookup"><span data-stu-id="6592d-334">An **Azure SQL** linked service toolink your SQL database that holds hello output data.</span></span>
3. <span data-ttu-id="6592d-335">Tworzenie **zestawów danych** opisujących dane wejściowe i wyjściowe dla potoków.</span><span class="sxs-lookup"><span data-stu-id="6592d-335">Created **datasets** that describe input data and output data for pipelines.</span></span>
4. <span data-ttu-id="6592d-336">Utworzony **potoku** z **działanie kopiowania**, z **BlobSource** jako źródło hello i **SqlSink** jako hello ujścia.</span><span class="sxs-lookup"><span data-stu-id="6592d-336">Created a **pipeline** with **Copy Activity**, with **BlobSource** as hello source and **SqlSink** as hello sink.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6592d-337">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6592d-337">Next steps</span></span>
<span data-ttu-id="6592d-338">W tym samouczku użyto magazynu obiektów blob platformy Azure jako magazynu danych źródła oraz bazy danych SQL na platformie Azure jako magazynu danych docelowych w operacji kopiowania.</span><span class="sxs-lookup"><span data-stu-id="6592d-338">In this tutorial, you used Azure blob storage as a source data store and an Azure SQL database as a destination data store in a copy operation.</span></span> <span data-ttu-id="6592d-339">Witaj Poniższa tabela zawiera listę magazynów danych obsługiwane jako źródeł i miejsc docelowych przez działanie kopiowania hello:</span><span class="sxs-lookup"><span data-stu-id="6592d-339">hello following table provides a list of data stores supported as sources and destinations by hello copy activity:</span></span> 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

<span data-ttu-id="6592d-340">toolearn o jak magazyn danych toocopy z danych, kliknij łącze hello hello magazynu danych w tabeli hello.</span><span class="sxs-lookup"><span data-stu-id="6592d-340">toolearn about how toocopy data to/from a data store, click hello link for hello data store in hello table.</span></span> 

