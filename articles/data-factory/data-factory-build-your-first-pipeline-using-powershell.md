---
title: aaaBuild pierwszy fabryki danych (PowerShell) | Dokumentacja firmy Microsoft
description: "W tym samouczku przedstawiono tworzenie przykładowego potoku usługi Azure Data Factory przy użyciu programu Azure PowerShell."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 22ec1236-ea86-4eb7-b903-0e79a58b90c7
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 626260798b56d590577b3c4b24f7cf52873c9f80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-build-your-first-azure-data-factory-using-azure-powershell"></a><span data-ttu-id="5873d-103">Samouczek: tworzenie pierwszej fabryki danych platformy Azure przy użyciu programu Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="5873d-103">Tutorial: Build your first Azure data factory using Azure PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="5873d-104">Przegląd i wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="5873d-104">Overview and prerequisites</span></span>](data-factory-build-your-first-pipeline.md)
> * [<span data-ttu-id="5873d-105">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="5873d-105">Azure portal</span></span>](data-factory-build-your-first-pipeline-using-editor.md)
> * [<span data-ttu-id="5873d-106">Program Visual Studio</span><span class="sxs-lookup"><span data-stu-id="5873d-106">Visual Studio</span></span>](data-factory-build-your-first-pipeline-using-vs.md)
> * [<span data-ttu-id="5873d-107">Program PowerShell</span><span class="sxs-lookup"><span data-stu-id="5873d-107">PowerShell</span></span>](data-factory-build-your-first-pipeline-using-powershell.md)
> * [<span data-ttu-id="5873d-108">Szablon usługi Resource Manager</span><span class="sxs-lookup"><span data-stu-id="5873d-108">Resource Manager Template</span></span>](data-factory-build-your-first-pipeline-using-arm.md)
> * [<span data-ttu-id="5873d-109">Interfejs API REST</span><span class="sxs-lookup"><span data-stu-id="5873d-109">REST API</span></span>](data-factory-build-your-first-pipeline-using-rest-api.md)
>
>

<span data-ttu-id="5873d-110">W tym artykule Użyj programu Azure PowerShell toocreate Twojego pierwszego fabryki danych Azure.</span><span class="sxs-lookup"><span data-stu-id="5873d-110">In this article, you use Azure PowerShell toocreate your first Azure data factory.</span></span> <span data-ttu-id="5873d-111">Samouczek hello toodo przy użyciu innych narzędzi/SDK, wybierz jedną z opcji hello z listy rozwijanej hello.</span><span class="sxs-lookup"><span data-stu-id="5873d-111">toodo hello tutorial using other tools/SDKs, select one of hello options from hello drop-down list.</span></span>

<span data-ttu-id="5873d-112">Witaj potoku, w tym samouczku ma jedno działanie: **działania HDInsight Hive**.</span><span class="sxs-lookup"><span data-stu-id="5873d-112">hello pipeline in this tutorial has one activity: **HDInsight Hive activity**.</span></span> <span data-ttu-id="5873d-113">To działanie uruchamia skrypt hive w klastrze Azure HDInsight czy transformacji wejściowych danych wyjściowych tooproduce danych.</span><span class="sxs-lookup"><span data-stu-id="5873d-113">This activity runs a hive script on an Azure HDInsight cluster that transforms input data tooproduce output data.</span></span> <span data-ttu-id="5873d-114">potok Hello jest zaplanowane toorun po miesiącu między hello określono godziny rozpoczęcia i zakończenia.</span><span class="sxs-lookup"><span data-stu-id="5873d-114">hello pipeline is scheduled toorun once a month between hello specified start and end times.</span></span> 

> [!NOTE]
> <span data-ttu-id="5873d-115">Witaj potoku danych w tym samouczku przekształca dane wyjściowe tooproduce danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="5873d-115">hello data pipeline in this tutorial transforms input data tooproduce output data.</span></span> <span data-ttu-id="5873d-116">Nie kopiuje danych z magazynu danych źródła danych magazynu tooa docelowego.</span><span class="sxs-lookup"><span data-stu-id="5873d-116">It does not copy data from a source data store tooa destination data store.</span></span> <span data-ttu-id="5873d-117">Samouczek na temat danych toocopy przy użyciu fabryki danych Azure, zobacz [samouczek: kopiowanie danych z magazynu obiektów Blob tooSQL bazy danych](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="5873d-117">For a tutorial on how toocopy data using Azure Data Factory, see [Tutorial: Copy data from Blob Storage tooSQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
> 
> <span data-ttu-id="5873d-118">Potok może obejmować więcej niż jedno działanie.</span><span class="sxs-lookup"><span data-stu-id="5873d-118">A pipeline can have more than one activity.</span></span> <span data-ttu-id="5873d-119">I tworzenia łańcucha dwa działania (Uruchom jedno działanie po drugim), ustawiając hello wyjściowy zestaw danych z jednego działania jako hello wejściowy zestaw danych z hello innych działań.</span><span class="sxs-lookup"><span data-stu-id="5873d-119">And, you can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="5873d-120">Więcej informacji znajduje się w artykule dotyczącym [planowania i wykonywania w usłudze Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span><span class="sxs-lookup"><span data-stu-id="5873d-120">For more information, see [scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5873d-121">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="5873d-121">Prerequisites</span></span>
* <span data-ttu-id="5873d-122">Zapoznaj się z artykułem [— samouczek Przegląd](data-factory-build-your-first-pipeline.md) artykułu i pełne hello **wymagań wstępnych** czynności.</span><span class="sxs-lookup"><span data-stu-id="5873d-122">Read through [Tutorial Overview](data-factory-build-your-first-pipeline.md) article and complete hello **prerequisite** steps.</span></span>
* <span data-ttu-id="5873d-123">Postępuj zgodnie z instrukcjami wyświetlanymi w [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview) artykułu tooinstall najnowszą wersję programu Azure PowerShell na komputerze.</span><span class="sxs-lookup"><span data-stu-id="5873d-123">Follow instructions in [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) article tooinstall latest version of Azure PowerShell on your computer.</span></span>
* <span data-ttu-id="5873d-124">(opcjonalnie) W tym artykule nie opisano wszystkich poleceń cmdlet fabryki danych hello.</span><span class="sxs-lookup"><span data-stu-id="5873d-124">(optional) This article does not cover all hello Data Factory cmdlets.</span></span> <span data-ttu-id="5873d-125">Pełna dokumentacja dotycząca poleceń cmdlet dla usługi Fabryka danych znajduje się w artykule [Data Factory Cmdlet Reference](/powershell/module/azurerm.datafactories) (Dokumentacja dotycząca poleceń cmdlet dla usługi Fabryka danych).</span><span class="sxs-lookup"><span data-stu-id="5873d-125">See [Data Factory Cmdlet Reference](/powershell/module/azurerm.datafactories) for comprehensive documentation on Data Factory cmdlets.</span></span>

## <a name="create-data-factory"></a><span data-ttu-id="5873d-126">Tworzenie fabryki danych</span><span class="sxs-lookup"><span data-stu-id="5873d-126">Create data factory</span></span>
<span data-ttu-id="5873d-127">W tym kroku użyjesz programu Azure PowerShell toocreate fabryki danych Azure o nazwie **FirstDataFactoryPSH**.</span><span class="sxs-lookup"><span data-stu-id="5873d-127">In this step, you use Azure PowerShell toocreate an Azure Data Factory named **FirstDataFactoryPSH**.</span></span> <span data-ttu-id="5873d-128">Fabryka danych może obejmować jeden lub wiele potoków.</span><span class="sxs-lookup"><span data-stu-id="5873d-128">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="5873d-129">Potok może obejmować jedno lub wiele działań.</span><span class="sxs-lookup"><span data-stu-id="5873d-129">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="5873d-130">Na przykład dane wejściowe toocopy działanie kopiowania danych z magazynu danych docelowy tooa źródłowego i HDInsight Hive działania toorun tootransform skryptu Hive.</span><span class="sxs-lookup"><span data-stu-id="5873d-130">For example, a Copy Activity toocopy data from a source tooa destination data store and a HDInsight Hive activity toorun a Hive script tootransform input data.</span></span> <span data-ttu-id="5873d-131">Zacznijmy od utworzenia hello fabryki danych w tym kroku.</span><span class="sxs-lookup"><span data-stu-id="5873d-131">Let's start with creating hello data factory in this step.</span></span>

1. <span data-ttu-id="5873d-132">Uruchom program Azure PowerShell i uruchom następujące polecenie hello.</span><span class="sxs-lookup"><span data-stu-id="5873d-132">Start Azure PowerShell and run hello following command.</span></span> <span data-ttu-id="5873d-133">Nie zamykaj programu Azure PowerShell do momentu zakończenia hello tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="5873d-133">Keep Azure PowerShell open until hello end of this tutorial.</span></span> <span data-ttu-id="5873d-134">Zamknij i otwórz ponownie, należy najpierw toorun tych poleceń ponownie.</span><span class="sxs-lookup"><span data-stu-id="5873d-134">If you close and reopen, you need toorun these commands again.</span></span>
   * <span data-ttu-id="5873d-135">Uruchom następujące polecenie hello, a następnie wprowadź hello nazwy użytkownika i hasła, użyj toosign w toohello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="5873d-135">Run hello following command and enter hello user name and password that you use toosign in toohello Azure portal.</span></span>
    ```PowerShell
    Login-AzureRmAccount
    ```    
   * <span data-ttu-id="5873d-136">Uruchom następujące polecenie tooview hello wszystkie subskrypcje powitania dla tego konta.</span><span class="sxs-lookup"><span data-stu-id="5873d-136">Run hello following command tooview all hello subscriptions for this account.</span></span>
    ```PowerShell
    Get-AzureRmSubscription 
    ```
   * <span data-ttu-id="5873d-137">Uruchom następujące polecenie tooselect hello subskrypcję, która ma toowork z hello.</span><span class="sxs-lookup"><span data-stu-id="5873d-137">Run hello following command tooselect hello subscription that you want toowork with.</span></span> <span data-ttu-id="5873d-138">Ta subskrypcja powinien Witaj, taka sama, jak hello jedną używaną w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="5873d-138">This subscription should be hello same as hello one you used in hello Azure portal.</span></span>
    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <SUBSCRIPTION NAME> | Set-AzureRmContext
    ```     
2. <span data-ttu-id="5873d-139">Tworzenie grupy zasobów platformy Azure o nazwie **ADFTutorialResourceGroup** , uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="5873d-139">Create an Azure resource group named **ADFTutorialResourceGroup** by running hello following command:</span></span>
    
    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```
    <span data-ttu-id="5873d-140">Niektóre kroki hello w tym samouczku Załóżmy, że hello grupy zasobów o nazwie ADFTutorialResourceGroup.</span><span class="sxs-lookup"><span data-stu-id="5873d-140">Some of hello steps in this tutorial assume that you use hello resource group named ADFTutorialResourceGroup.</span></span> <span data-ttu-id="5873d-141">Jeśli używasz innej grupie zasobów, należy toouse go zamiast ADFTutorialResourceGroup w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="5873d-141">If you use a different resource group, you need toouse it in place of ADFTutorialResourceGroup in this tutorial.</span></span>
3. <span data-ttu-id="5873d-142">Uruchom hello **AzureRmDataFactory nowy** polecenie cmdlet tworzy fabrykę danych o nazwie **FirstDataFactoryPSH**.</span><span class="sxs-lookup"><span data-stu-id="5873d-142">Run hello **New-AzureRmDataFactory** cmdlet that creates a data factory named **FirstDataFactoryPSH**.</span></span>

    ```PowerShell
    New-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name FirstDataFactoryPSH –Location "West US"
    ```
<span data-ttu-id="5873d-143">Należy zwrócić uwagę hello następujące punkty:</span><span class="sxs-lookup"><span data-stu-id="5873d-143">Note hello following points:</span></span>

* <span data-ttu-id="5873d-144">Nazwa Hello hello fabryki danych Azure musi być globalnie unikatowe.</span><span class="sxs-lookup"><span data-stu-id="5873d-144">hello name of hello Azure Data Factory must be globally unique.</span></span> <span data-ttu-id="5873d-145">Jeśli wystąpi błąd hello **nazwa fabryki danych "FirstDataFactoryPSH" nie jest dostępna**, Zmień nazwę hello (na przykład yournameFirstDataFactoryPSH).</span><span class="sxs-lookup"><span data-stu-id="5873d-145">If you receive hello error **Data factory name “FirstDataFactoryPSH” is not available**, change hello name (for example, yournameFirstDataFactoryPSH).</span></span> <span data-ttu-id="5873d-146">Użyj tej nazwy zamiast ADFTutorialFactoryPSH podczas wykonywania kroków w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="5873d-146">Use this name in place of ADFTutorialFactoryPSH while performing steps in this tutorial.</span></span> <span data-ttu-id="5873d-147">Artykuł [Data Factory — Naming Rules](data-factory-naming-rules.md) (Fabryka danych — zasady nazewnictwa) zawiera zasady nazewnictwa artefaktów usługi Fabryka danych.</span><span class="sxs-lookup"><span data-stu-id="5873d-147">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>
* <span data-ttu-id="5873d-148">toocreate wystąpienia fabryki danych, należy toobe współautora/administrator hello subskrypcji platformy Azure</span><span class="sxs-lookup"><span data-stu-id="5873d-148">toocreate Data Factory instances, you need toobe a contributor/administrator of hello Azure subscription</span></span>
* <span data-ttu-id="5873d-149">Nazwa fabryki danych hello Hello mogą być zarejestrowana jako nazwa DNS w przyszłości hello i dlatego stać się publicznie widoczna.</span><span class="sxs-lookup"><span data-stu-id="5873d-149">hello name of hello data factory may be registered as a DNS name in hello future and hence become publically visible.</span></span>
* <span data-ttu-id="5873d-150">Jeśli wystąpi błąd hello: "**Ta subskrypcja nie jest zarejestrowany toouse przestrzeni nazw Microsoft.DataFactory**", wykonaj jedną z następujących hello i spróbuj ponownie opublikować:</span><span class="sxs-lookup"><span data-stu-id="5873d-150">If you receive hello error: "**This subscription is not registered toouse namespace Microsoft.DataFactory**", do one of hello following and try publishing again:</span></span>

  * <span data-ttu-id="5873d-151">W programie Azure PowerShell Uruchom hello następujące polecenia tooregister hello fabryki danych dostawcy:</span><span class="sxs-lookup"><span data-stu-id="5873d-151">In Azure PowerShell, run hello following command tooregister hello Data Factory provider:</span></span>

    ```PowerShell
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```
      <span data-ttu-id="5873d-152">Powitania po tooconfirm polecenie można uruchomić tej fabryki danych w zarejestrowany dostawca hello:</span><span class="sxs-lookup"><span data-stu-id="5873d-152">You can run hello following command tooconfirm that hello Data Factory provider is registered:</span></span>

    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * <span data-ttu-id="5873d-153">Logowanie przy użyciu hello subskrypcji platformy Azure do hello [portalu Azure](https://portal.azure.com) i przejdź do bloku usługi fabryka danych tooa tworzenie fabryki danych w hello portalu Azure (lub).</span><span class="sxs-lookup"><span data-stu-id="5873d-153">Login using hello Azure subscription into hello [Azure portal](https://portal.azure.com) and navigate tooa Data Factory blade (or) create a data factory in hello Azure portal.</span></span> <span data-ttu-id="5873d-154">Ta akcja rejestruje automatycznie hello dostawcy dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="5873d-154">This action automatically registers hello provider for you.</span></span>

<span data-ttu-id="5873d-155">Przed utworzeniem potoku, należy toocreate kilku jednostek fabryki danych najpierw.</span><span class="sxs-lookup"><span data-stu-id="5873d-155">Before creating a pipeline, you need toocreate a few Data Factory entities first.</span></span> <span data-ttu-id="5873d-156">Najpierw utwórz danych toolink połączonych usług danych tooyour magazyny/oblicza przechowywania, zdefiniuj dane wejściowe i zestawów danych toorepresent wejścia/wyjścia dane w magazynach połączone dane wyjściowe, a następnie utwórz hello potoku do działania, która używa tych zestawów danych.</span><span class="sxs-lookup"><span data-stu-id="5873d-156">You first create linked services toolink data stores/computes tooyour data store, define input and output datasets toorepresent input/output data in linked data stores, and then create hello pipeline with an activity that uses these datasets.</span></span>

## <a name="create-linked-services"></a><span data-ttu-id="5873d-157">Tworzenie połączonych usług</span><span class="sxs-lookup"><span data-stu-id="5873d-157">Create linked services</span></span>
<span data-ttu-id="5873d-158">W tym kroku możesz połączyć konta magazynu Azure i fabrykę danych tooyour klastra Azure HDInsight na żądanie.</span><span class="sxs-lookup"><span data-stu-id="5873d-158">In this step, you link your Azure Storage account and an on-demand Azure HDInsight cluster tooyour data factory.</span></span> <span data-ttu-id="5873d-159">blokady konta usługi Azure Storage Hello hello danych wejściowych i wyjściowych do potoku hello w tym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="5873d-159">hello Azure Storage account holds hello input and output data for hello pipeline in this sample.</span></span> <span data-ttu-id="5873d-160">Hello usługi HDInsight połączony jest używane toorun określony w działaniu hello hello potoku, w tym przykładzie skrypt Hive.</span><span class="sxs-lookup"><span data-stu-id="5873d-160">hello HDInsight linked service is used toorun a Hive script specified in hello activity of hello pipeline in this sample.</span></span> <span data-ttu-id="5873d-161">Określenie, jakie dane magazynu/obliczeń usług są używane w danym scenariuszu i łączenie fabryki danych toohello tych usług za tworzenie połączonych usług.</span><span class="sxs-lookup"><span data-stu-id="5873d-161">Identify what data store/compute services are used in your scenario and link those services toohello data factory by creating linked services.</span></span>

### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="5873d-162">Tworzenie połączonej usługi Azure Storage</span><span class="sxs-lookup"><span data-stu-id="5873d-162">Create Azure Storage linked service</span></span>
<span data-ttu-id="5873d-163">W tym kroku możesz połączyć fabrykę danych tooyour konta magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="5873d-163">In this step, you link your Azure Storage account tooyour data factory.</span></span> <span data-ttu-id="5873d-164">Użyj hello tego samego konta magazynu Azure toostore wejścia/wyjścia danych i hello HQL plik skryptu.</span><span class="sxs-lookup"><span data-stu-id="5873d-164">You use hello same Azure Storage account toostore input/output data and hello HQL script file.</span></span>

1. <span data-ttu-id="5873d-165">Utwórz plik JSON o nazwie StorageLinkedService.json w folderze C:\ADFGetStarted hello z powitania po zawartości.</span><span class="sxs-lookup"><span data-stu-id="5873d-165">Create a JSON file named StorageLinkedService.json in hello C:\ADFGetStarted folder with hello following content.</span></span> <span data-ttu-id="5873d-166">Utwórz hello folder ADFGetStarted, jeśli jeszcze nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="5873d-166">Create hello folder ADFGetStarted if it does not already exist.</span></span>

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
    <span data-ttu-id="5873d-167">Zastąp **nazwa konta** hello nazwą konta magazynu Azure i **klucz konta** z klucz dostępu hello hello kontem magazynu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="5873d-167">Replace **account name** with hello name of your Azure storage account and **account key** with hello access key of hello Azure storage account.</span></span> <span data-ttu-id="5873d-168">toolearn sposób dostępu do magazynu tooget klucza, zobacz hello informacji na temat sposobu tooview, kopiowania i regenerate magazynu dostępu do kluczy w [Zarządzanie kontem magazynu](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="5873d-168">toolearn how tooget your storage access key, see hello information about how tooview, copy, and regenerate storage access keys in [Manage your storage account](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>
2. <span data-ttu-id="5873d-169">W programie Azure PowerShell przełącznika toohello ADFGetStarted folderu.</span><span class="sxs-lookup"><span data-stu-id="5873d-169">In Azure PowerShell, switch toohello ADFGetStarted folder.</span></span>
3. <span data-ttu-id="5873d-170">Można użyć hello **AzureRmDataFactoryLinkedService nowy** polecenie cmdlet tworzy połączonej usługi.</span><span class="sxs-lookup"><span data-stu-id="5873d-170">You can use hello **New-AzureRmDataFactoryLinkedService** cmdlet that creates a linked service.</span></span> <span data-ttu-id="5873d-171">To polecenie cmdlet i innych poleceń cmdlet z fabryki danych użycia w ramach tego samouczka wymaga wartości toopass dla hello *ResourceGroupName* i *DataFactoryName* parametrów.</span><span class="sxs-lookup"><span data-stu-id="5873d-171">This cmdlet and other Data Factory cmdlets you use in this tutorial requires you toopass values for hello *ResourceGroupName* and *DataFactoryName* parameters.</span></span> <span data-ttu-id="5873d-172">Alternatywnie można użyć **Get-AzureRmDataFactory** tooget **DataFactory** obiektu i przekazać obiekt hello bez wprowadzania *ResourceGroupName* i  *DataFactoryName* zawsze należy uruchomić polecenie cmdlet.</span><span class="sxs-lookup"><span data-stu-id="5873d-172">Alternatively, you can use **Get-AzureRmDataFactory** tooget a **DataFactory** object and pass hello object without typing *ResourceGroupName* and *DataFactoryName* each time you run a cmdlet.</span></span> <span data-ttu-id="5873d-173">Witaj uruchom następujące polecenie dane wyjściowe hello tooassign hello **Get-AzureRmDataFactory** tooa polecenia cmdlet **$df** zmiennej.</span><span class="sxs-lookup"><span data-stu-id="5873d-173">Run hello following command tooassign hello output of hello **Get-AzureRmDataFactory** cmdlet tooa **$df** variable.</span></span>

    ```PowerShell
    $df=Get-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name FirstDataFactoryPSH
    ```
4. <span data-ttu-id="5873d-174">Teraz uruchom hello **AzureRmDataFactoryLinkedService nowy** połączone polecenie cmdlet tworzy hello **StorageLinkedService** usługi.</span><span class="sxs-lookup"><span data-stu-id="5873d-174">Now, run hello **New-AzureRmDataFactoryLinkedService** cmdlet that creates hello linked **StorageLinkedService** service.</span></span>

    ```PowerShell
    New-AzureRmDataFactoryLinkedService $df -File .\StorageLinkedService.json
    ```
    <span data-ttu-id="5873d-175">Jeżeli nie uruchomisz hello **Get-AzureRmDataFactory** toohello wyjściowe polecenia cmdlet i przypisane hello **$df** zmiennej, konieczne będzie toospecify wartości hello *ResourceGroupName*i *DataFactoryName* parametrów w następujący sposób.</span><span class="sxs-lookup"><span data-stu-id="5873d-175">If you hadn't run hello **Get-AzureRmDataFactory** cmdlet and assigned hello output toohello **$df** variable, you would have toospecify values for hello *ResourceGroupName* and *DataFactoryName* parameters as follows.</span></span>

    ```PowerShell
    New-AzureRmDataFactoryLinkedService -ResourceGroupName ADFTutorialResourceGroup -DataFactoryName FirstDataFactoryPSH -File .\StorageLinkedService.json
    ```
    <span data-ttu-id="5873d-176">Jeśli zamkniesz programu Azure PowerShell w środku hello samouczka hello masz toorun hello **Get-AzureRmDataFactory** polecenia cmdlet następnym uruchomieniu programu Azure PowerShell toocomplete hello samouczka.</span><span class="sxs-lookup"><span data-stu-id="5873d-176">If you close Azure PowerShell in hello middle of hello tutorial, you have toorun hello **Get-AzureRmDataFactory** cmdlet next time you start Azure PowerShell toocomplete hello tutorial.</span></span>

### <a name="create-azure-hdinsight-linked-service"></a><span data-ttu-id="5873d-177">Tworzenie połączonej usługi Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="5873d-177">Create Azure HDInsight linked service</span></span>
<span data-ttu-id="5873d-178">W tym kroku możesz połączyć fabrykę danych tooyour klastra usługi HDInsight na żądanie.</span><span class="sxs-lookup"><span data-stu-id="5873d-178">In this step, you link an on-demand HDInsight cluster tooyour data factory.</span></span> <span data-ttu-id="5873d-179">klaster usługi HDInsight Hello jest automatycznie tworzone w czasie wykonywania i usuwane po zakończeniu przetwarzania i bezczynności hello określoną ilość czasu.</span><span class="sxs-lookup"><span data-stu-id="5873d-179">hello HDInsight cluster is automatically created at runtime and deleted after it is done processing and idle for hello specified amount of time.</span></span> <span data-ttu-id="5873d-180">Możesz użyć własnego klastra usługi HDInsight zamiast klastra usługi HDInsight na żądanie.</span><span class="sxs-lookup"><span data-stu-id="5873d-180">You could use your own HDInsight cluster instead of using an on-demand HDInsight cluster.</span></span> <span data-ttu-id="5873d-181">Szczegółowe informacje znajdują się w artykule [Compute Linked Services](data-factory-compute-linked-services.md) (Połączone usługi obliczeniowe).</span><span class="sxs-lookup"><span data-stu-id="5873d-181">See [Compute Linked Services](data-factory-compute-linked-services.md) for details.</span></span>

1. <span data-ttu-id="5873d-182">Utwórz plik JSON o nazwie **HDInsightOnDemandLinkedService**JSON w hello **C:\ADFGetStarted** folder o powitania po zawartości.</span><span class="sxs-lookup"><span data-stu-id="5873d-182">Create a JSON file named **HDInsightOnDemandLinkedService**.json in hello **C:\ADFGetStarted** folder with hello following content.</span></span>

    ```json
    {
        "name": "HDInsightOnDemandLinkedService",
        "properties": {
            "type": "HDInsightOnDemand",
            "typeProperties": {
                "version": "3.5",
                "clusterSize": 1,
                "timeToLive": "00:05:00",
                "osType": "Linux",
                "linkedServiceName": "StorageLinkedService"
            }
        }
    }
    ```
    <span data-ttu-id="5873d-183">Witaj Poniższa tabela zawiera opisy właściwości JSON hello używane we fragmencie hello:</span><span class="sxs-lookup"><span data-stu-id="5873d-183">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

   | <span data-ttu-id="5873d-184">Właściwość</span><span class="sxs-lookup"><span data-stu-id="5873d-184">Property</span></span> | <span data-ttu-id="5873d-185">Opis</span><span class="sxs-lookup"><span data-stu-id="5873d-185">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="5873d-186">ClusterSize</span><span class="sxs-lookup"><span data-stu-id="5873d-186">ClusterSize</span></span> |<span data-ttu-id="5873d-187">Określa rozmiar hello hello klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5873d-187">Specifies hello size of hello HDInsight cluster.</span></span> |
   | <span data-ttu-id="5873d-188">TimeToLive</span><span class="sxs-lookup"><span data-stu-id="5873d-188">TimeToLive</span></span> |<span data-ttu-id="5873d-189">Określa czas bezczynności tej hello hello klastra usługi HDInsight, przed usunięciem.</span><span class="sxs-lookup"><span data-stu-id="5873d-189">Specifies that hello idle time for hello HDInsight cluster, before it is deleted.</span></span> |
   | <span data-ttu-id="5873d-190">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="5873d-190">linkedServiceName</span></span> |<span data-ttu-id="5873d-191">Określa konto magazynu hello jest używany toostore hello dzienniki, generowanych przez usługi HDInsight</span><span class="sxs-lookup"><span data-stu-id="5873d-191">Specifies hello storage account that is used toostore hello logs that are generated by HDInsight</span></span> |

    <span data-ttu-id="5873d-192">Należy zwrócić uwagę hello następujące punkty:</span><span class="sxs-lookup"><span data-stu-id="5873d-192">Note hello following points:</span></span>

   * <span data-ttu-id="5873d-193">Witaj fabryki danych tworzy **opartych na systemie Linux** klastra usługi HDInsight za pomocą hello JSON.</span><span class="sxs-lookup"><span data-stu-id="5873d-193">hello Data Factory creates a **Linux-based** HDInsight cluster for you with hello JSON.</span></span> <span data-ttu-id="5873d-194">Szczegółowe informacje znajdują się w artykule [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) (Połączona usługa HDInsight na żądanie).</span><span class="sxs-lookup"><span data-stu-id="5873d-194">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>
   * <span data-ttu-id="5873d-195">Możesz użyć **własnego klastra usługi HDInsight** zamiast klastra usługi HDInsight na żądanie.</span><span class="sxs-lookup"><span data-stu-id="5873d-195">You could use **your own HDInsight cluster** instead of using an on-demand HDInsight cluster.</span></span> <span data-ttu-id="5873d-196">Szczegółowe informacje znajdują się w artykule [HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) (Połączona usługa HDInsight).</span><span class="sxs-lookup"><span data-stu-id="5873d-196">See [HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) for details.</span></span>
   * <span data-ttu-id="5873d-197">Tworzy klaster usługi HDInsight Hello **domyślny kontener** w magazynie obiektów blob hello określone w hello JSON (**linkedServiceName**).</span><span class="sxs-lookup"><span data-stu-id="5873d-197">hello HDInsight cluster creates a **default container** in hello blob storage you specified in hello JSON (**linkedServiceName**).</span></span> <span data-ttu-id="5873d-198">Po usunięciu klastra hello HDInsight nie usunie tego kontenera.</span><span class="sxs-lookup"><span data-stu-id="5873d-198">HDInsight does not delete this container when hello cluster is deleted.</span></span> <span data-ttu-id="5873d-199">To zachowanie jest celowe.</span><span class="sxs-lookup"><span data-stu-id="5873d-199">This behavior is by design.</span></span> <span data-ttu-id="5873d-200">W przypadku połączonej usługi HDInsight na żądanie klaster usługi HDInsight jest tworzony przy każdym przetwarzaniu wycinka — o ile w tym momencie nie istnieje aktywny klaster (**timeToLive**).</span><span class="sxs-lookup"><span data-stu-id="5873d-200">With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice is processed unless there is an existing live cluster (**timeToLive**).</span></span> <span data-ttu-id="5873d-201">klaster Hello są automatycznie usuwane po zakończeniu przetwarzania hello.</span><span class="sxs-lookup"><span data-stu-id="5873d-201">hello cluster is automatically deleted when hello processing is done.</span></span>

       <span data-ttu-id="5873d-202">Po przetworzeniu większej liczby wycinków w usłudze Azure Blob Storage będzie widocznych wiele kontenerów.</span><span class="sxs-lookup"><span data-stu-id="5873d-202">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="5873d-203">Jeśli nie ma potrzeby do rozwiązywania problemów hello zadań, możesz toodelete ich magazynu hello tooreduce kosztów.</span><span class="sxs-lookup"><span data-stu-id="5873d-203">If you do not need them for troubleshooting of hello jobs, you may want toodelete them tooreduce hello storage cost.</span></span> <span data-ttu-id="5873d-204">nazwy Hello kontenery wykonaj wzorca: "adf**yourdatafactoryname**-**linkedservicename**- datetimestamp".</span><span class="sxs-lookup"><span data-stu-id="5873d-204">hello names of these containers follow a pattern: "adf**yourdatafactoryname**-**linkedservicename**-datetimestamp".</span></span> <span data-ttu-id="5873d-205">Użyj narzędzia takiego jak [Eksploratora magazynu](http://storageexplorer.com/) magazynu obiektów blob toodelete kontenerów w platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="5873d-205">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) toodelete containers in your Azure blob storage.</span></span>

     <span data-ttu-id="5873d-206">Szczegółowe informacje znajdują się w artykule [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) (Połączona usługa HDInsight na żądanie).</span><span class="sxs-lookup"><span data-stu-id="5873d-206">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>
2. <span data-ttu-id="5873d-207">Uruchom hello **AzureRmDataFactoryLinkedService nowy** polecenie cmdlet tworzy hello połączona usługa o nazwie HDInsightOnDemandLinkedService.</span><span class="sxs-lookup"><span data-stu-id="5873d-207">Run hello **New-AzureRmDataFactoryLinkedService** cmdlet that creates hello linked service called HDInsightOnDemandLinkedService.</span></span>
    
    ```PowerShell
    New-AzureRmDataFactoryLinkedService $df -File .\HDInsightOnDemandLinkedService.json
    ```

## <a name="create-datasets"></a><span data-ttu-id="5873d-208">Tworzenie zestawów danych</span><span class="sxs-lookup"><span data-stu-id="5873d-208">Create datasets</span></span>
<span data-ttu-id="5873d-209">W tym kroku utwórz wprowadzania hello toorepresent zestawów danych i wysyłania danych do przetwarzania Hive.</span><span class="sxs-lookup"><span data-stu-id="5873d-209">In this step, you create datasets toorepresent hello input and output data for Hive processing.</span></span> <span data-ttu-id="5873d-210">Te zestawy danych można znaleźć toohello **StorageLinkedService** został utworzony we wcześniejszej części tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="5873d-210">These datasets refer toohello **StorageLinkedService** you have created earlier in this tutorial.</span></span> <span data-ttu-id="5873d-211">Witaj tooan punktów połączonej usługi konta usługi Azure Storage i zestawów danych, określ kontener, folder, nazwa pliku w magazynie hello, która przechowuje dane wejściowe i wyjściowe danych.</span><span class="sxs-lookup"><span data-stu-id="5873d-211">hello linked service points tooan Azure Storage account and datasets specify container, folder, file name in hello storage that holds input and output data.</span></span>

### <a name="create-input-dataset"></a><span data-ttu-id="5873d-212">Tworzenie wejściowego zestawu danych</span><span class="sxs-lookup"><span data-stu-id="5873d-212">Create input dataset</span></span>
1. <span data-ttu-id="5873d-213">Utwórz plik JSON o nazwie **InputTable.json** w hello **C:\ADFGetStarted** folder o hello następującej zawartości:</span><span class="sxs-lookup"><span data-stu-id="5873d-213">Create a JSON file named **InputTable.json** in hello **C:\ADFGetStarted** folder with hello following content:</span></span>

    ```json
    {
        "name": "AzureBlobInput",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "StorageLinkedService",
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
    <span data-ttu-id="5873d-214">Witaj JSON definiuje zestaw danych o nazwie **AzureBlobInput**, który reprezentuje dane wejściowe dla działania w potoku hello.</span><span class="sxs-lookup"><span data-stu-id="5873d-214">hello JSON defines a dataset named **AzureBlobInput**, which represents input data for an activity in hello pipeline.</span></span> <span data-ttu-id="5873d-215">Ponadto określa ona, że danych wejściowych hello znajduje się w kontenerze obiektów blob hello o nazwie **adfgetstarted** i hello folder o nazwie **inputdata**.</span><span class="sxs-lookup"><span data-stu-id="5873d-215">In addition, it specifies that hello input data is located in hello blob container called **adfgetstarted** and hello folder called **inputdata**.</span></span>

    <span data-ttu-id="5873d-216">Witaj Poniższa tabela zawiera opisy właściwości JSON hello używane we fragmencie hello:</span><span class="sxs-lookup"><span data-stu-id="5873d-216">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

   | <span data-ttu-id="5873d-217">Właściwość</span><span class="sxs-lookup"><span data-stu-id="5873d-217">Property</span></span> | <span data-ttu-id="5873d-218">Opis</span><span class="sxs-lookup"><span data-stu-id="5873d-218">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="5873d-219">type</span><span class="sxs-lookup"><span data-stu-id="5873d-219">type</span></span> |<span data-ttu-id="5873d-220">Witaj właściwość type ma wartość tooAzureBlob, ponieważ dane znajdują się w magazynie obiektów blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="5873d-220">hello type property is set tooAzureBlob because data resides in Azure blob storage.</span></span> |
   | <span data-ttu-id="5873d-221">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="5873d-221">linkedServiceName</span></span> |<span data-ttu-id="5873d-222">odwołuje się toohello StorageLinkedService utworzony wcześniej.</span><span class="sxs-lookup"><span data-stu-id="5873d-222">refers toohello StorageLinkedService you created earlier.</span></span> |
   | <span data-ttu-id="5873d-223">fileName</span><span class="sxs-lookup"><span data-stu-id="5873d-223">fileName</span></span> |<span data-ttu-id="5873d-224">Ta właściwość jest opcjonalna.</span><span class="sxs-lookup"><span data-stu-id="5873d-224">This property is optional.</span></span> <span data-ttu-id="5873d-225">W przypadku pominięcia tej właściwości, pobierane są wszystkie pliki hello z hello folderPath.</span><span class="sxs-lookup"><span data-stu-id="5873d-225">If you omit this property, all hello files from hello folderPath are picked.</span></span> <span data-ttu-id="5873d-226">W takim przypadku tylko input.log hello jest przetwarzany.</span><span class="sxs-lookup"><span data-stu-id="5873d-226">In this case, only hello input.log is processed.</span></span> |
   | <span data-ttu-id="5873d-227">type</span><span class="sxs-lookup"><span data-stu-id="5873d-227">type</span></span> |<span data-ttu-id="5873d-228">pliki dziennika Hello są w formacie tekstowym, więc używamy TextFormat.</span><span class="sxs-lookup"><span data-stu-id="5873d-228">hello log files are in text format, so we use TextFormat.</span></span> |
   | <span data-ttu-id="5873d-229">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="5873d-229">columnDelimiter</span></span> |<span data-ttu-id="5873d-230">kolumn w plikach dziennika hello są rozdzielone znakiem hello przecinkami (,).</span><span class="sxs-lookup"><span data-stu-id="5873d-230">columns in hello log files are delimited by hello comma character (,).</span></span> |
   | <span data-ttu-id="5873d-231">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="5873d-231">frequency/interval</span></span> |<span data-ttu-id="5873d-232">tooMonth Ustaw częstotliwość i interwał wynosi 1, co oznacza, że wejściowy wycinków hello są dostępne co miesiąc.</span><span class="sxs-lookup"><span data-stu-id="5873d-232">frequency set tooMonth and interval is 1, which means that hello input slices are available monthly.</span></span> |
   | <span data-ttu-id="5873d-233">external</span><span class="sxs-lookup"><span data-stu-id="5873d-233">external</span></span> |<span data-ttu-id="5873d-234">Ta właściwość ma wartość tootrue, jeśli dane wejściowe hello nie jest generowany przez hello usługi fabryka danych.</span><span class="sxs-lookup"><span data-stu-id="5873d-234">this property is set tootrue if hello input data is not generated by hello Data Factory service.</span></span> |
2. <span data-ttu-id="5873d-235">Uruchom następujące polecenie w środowiska Azure PowerShell toocreate hello fabryki danych w zestawie danych hello:</span><span class="sxs-lookup"><span data-stu-id="5873d-235">Run hello following command in Azure PowerShell toocreate hello Data Factory dataset:</span></span>

    ```PowerShell
    New-AzureRmDataFactoryDataset $df -File .\InputTable.json
    ```

### <a name="create-output-dataset"></a><span data-ttu-id="5873d-236">Tworzenie wyjściowego zestawu danych</span><span class="sxs-lookup"><span data-stu-id="5873d-236">Create output dataset</span></span>
<span data-ttu-id="5873d-237">Można teraz utworzyć hello wyjściowego zestawu danych toorepresent hello danych wyjściowych danych przechowywanych w hello magazynu obiektów Blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="5873d-237">Now, you create hello output dataset toorepresent hello output data stored in hello Azure Blob storage.</span></span>

1. <span data-ttu-id="5873d-238">Utwórz plik JSON o nazwie **OutputTable.json** w hello **C:\ADFGetStarted** folder o hello następującej zawartości:</span><span class="sxs-lookup"><span data-stu-id="5873d-238">Create a JSON file named **OutputTable.json** in hello **C:\ADFGetStarted** folder with hello following content:</span></span>

    ```json
    {
      "name": "AzureBlobOutput",
      "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
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
    <span data-ttu-id="5873d-239">Witaj JSON definiuje zestaw danych o nazwie **AzureBlobOutput**, który reprezentuje danych wyjściowych dla działania w potoku hello.</span><span class="sxs-lookup"><span data-stu-id="5873d-239">hello JSON defines a dataset named **AzureBlobOutput**, which represents output data for an activity in hello pipeline.</span></span> <span data-ttu-id="5873d-240">Ponadto określa ona, że wyniki hello są przechowywane w kontenerze obiektów blob hello o nazwie **adfgetstarted** i hello folder o nazwie **partitioneddata**.</span><span class="sxs-lookup"><span data-stu-id="5873d-240">In addition, it specifies that hello results are stored in hello blob container called **adfgetstarted** and hello folder called **partitioneddata**.</span></span> <span data-ttu-id="5873d-241">Witaj **dostępności** sekcja określa, że wyjściowy zestaw danych hello jest tworzony co miesiąc.</span><span class="sxs-lookup"><span data-stu-id="5873d-241">hello **availability** section specifies that hello output dataset is produced on a monthly basis.</span></span>
2. <span data-ttu-id="5873d-242">Uruchom następujące polecenie w środowiska Azure PowerShell toocreate hello fabryki danych w zestawie danych hello:</span><span class="sxs-lookup"><span data-stu-id="5873d-242">Run hello following command in Azure PowerShell toocreate hello Data Factory dataset:</span></span>

    ```PowerShell
    New-AzureRmDataFactoryDataset $df -File .\OutputTable.json
    ```

## <a name="create-pipeline"></a><span data-ttu-id="5873d-243">Tworzenie potoku</span><span class="sxs-lookup"><span data-stu-id="5873d-243">Create pipeline</span></span>
<span data-ttu-id="5873d-244">W tym kroku opisano tworzenie pierwszego potoku za pomocą działania **HDInsightHive**.</span><span class="sxs-lookup"><span data-stu-id="5873d-244">In this step, you create your first pipeline with a **HDInsightHive** activity.</span></span> <span data-ttu-id="5873d-245">Wejściowy jest dostępny co miesiąc (częstotliwość: miesiąc, interwał: 1), wycinek danych wyjściowych jest tworzony co miesiąc, a właściwość harmonogramu hello działania hello jest ustawić toomonthly.</span><span class="sxs-lookup"><span data-stu-id="5873d-245">Input slice is available monthly (frequency: Month, interval: 1), output slice is produced monthly, and hello scheduler property for hello activity is also set toomonthly.</span></span> <span data-ttu-id="5873d-246">Ustawienia Hello hello wyjściowego zestawu danych i harmonogram działania hello muszą być zgodne.</span><span class="sxs-lookup"><span data-stu-id="5873d-246">hello settings for hello output dataset and hello activity scheduler must match.</span></span> <span data-ttu-id="5873d-247">Wyjściowy zestaw danych jest obecnie, jakie dysków hello harmonogramu, dlatego należy utworzyć wyjściowy zestaw danych, nawet wtedy, gdy działanie hello nie generuje żadnego wyniku.</span><span class="sxs-lookup"><span data-stu-id="5873d-247">Currently, output dataset is what drives hello schedule, so you must create an output dataset even if hello activity does not produce any output.</span></span> <span data-ttu-id="5873d-248">Jeśli działanie hello nie przyjmuje żadnych danych, możesz pominąć tworzenie zestawu danych wejściowych hello.</span><span class="sxs-lookup"><span data-stu-id="5873d-248">If hello activity doesn't take any input, you can skip creating hello input dataset.</span></span> <span data-ttu-id="5873d-249">na końcu hello w tej sekcji opisano Hello właściwości używane w hello następującego formatu JSON.</span><span class="sxs-lookup"><span data-stu-id="5873d-249">hello properties used in hello following JSON are explained at hello end of this section.</span></span>

1. <span data-ttu-id="5873d-250">Utwórz plik JSON o nazwie MyFirstPipelinePSH.json w folderze C:\ADFGetStarted hello z powitania po zawartości:</span><span class="sxs-lookup"><span data-stu-id="5873d-250">Create a JSON file named MyFirstPipelinePSH.json in hello C:\ADFGetStarted folder with hello following content:</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="5873d-251">Zastąp **storageaccountname** hello nazwą konta magazynu w hello JSON.</span><span class="sxs-lookup"><span data-stu-id="5873d-251">Replace **storageaccountname** with hello name of your storage account in hello JSON.</span></span>
   >
   >

    ```json
    {
        "name": "MyFirstPipeline",
        "properties": {
            "description": "My first Azure Data Factory pipeline",
            "activities": [
                {
                    "type": "HDInsightHive",
                    "typeProperties": {
                        "scriptPath": "adfgetstarted/script/partitionweblogs.hql",
                        "scriptLinkedService": "StorageLinkedService",
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
    <span data-ttu-id="5873d-252">We fragmencie JSON hello tworzysz potok, który składa się z jednego działania używającej tooprocess Hive danych w klastrze usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5873d-252">In hello JSON snippet, you are creating a pipeline that consists of a single activity that uses Hive tooprocess Data on an HDInsight cluster.</span></span>

    <span data-ttu-id="5873d-253">plik skryptu Hive Hello, **partitionweblogs.hql**, są przechowywane w hello kontem magazynu platformy Azure (określonego przez element scriptLinkedService hello, nazywany **StorageLinkedService**) i w **skryptu**  folderu w kontenerze hello **adfgetstarted**.</span><span class="sxs-lookup"><span data-stu-id="5873d-253">hello Hive script file, **partitionweblogs.hql**, is stored in hello Azure storage account (specified by hello scriptLinkedService, called **StorageLinkedService**), and in **script** folder in hello container **adfgetstarted**.</span></span>

    <span data-ttu-id="5873d-254">Hello **definiuje** sekcja jest używane toospecify hello środowiska uruchomieniowego ustawień, które można przekazać skryptu hive toohello jako wartości konfiguracji gałąź (np. ${hiveconf: inputtable}, ${hiveconf:partitionedtable}).</span><span class="sxs-lookup"><span data-stu-id="5873d-254">hello **defines** section is used toospecify hello runtime settings that be passed toohello hive script as Hive configuration values (e.g ${hiveconf:inputtable}, ${hiveconf:partitionedtable}).</span></span>

    <span data-ttu-id="5873d-255">Witaj **start** i **zakończenia** hello aktywny okres potoku hello określa właściwości hello potoku.</span><span class="sxs-lookup"><span data-stu-id="5873d-255">hello **start** and **end** properties of hello pipeline specifies hello active period of hello pipeline.</span></span>

    <span data-ttu-id="5873d-256">W działaniu hello JSON, możesz określić, tego skryptu Hive hello zostanie uruchomiona na określony przez hello obliczeń hello **linkedServiceName** — **HDInsightOnDemandLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="5873d-256">In hello activity JSON, you specify that hello Hive script runs on hello compute specified by hello **linkedServiceName** – **HDInsightOnDemandLinkedService**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="5873d-257">Zobacz sekcję "JSON potoku" w [potoki i działań w fabryce danych Azure](data-factory-create-pipelines.md) szczegółowe informacje na temat właściwości JSON, które są używane w przykładzie hello.</span><span class="sxs-lookup"><span data-stu-id="5873d-257">See "Pipeline JSON" in [Pipelines and activities in Azure Data Factory](data-factory-create-pipelines.md) for details about JSON properties that are used in hello example.</span></span>

2. <span data-ttu-id="5873d-258">Upewnij się, że widoczny hello **input.log** pliku w hello **adfgetstarted/inputdata** folderu w hello magazynu obiektów blob platformy Azure i hello uruchom następujące polecenie toodeploy hello potoku.</span><span class="sxs-lookup"><span data-stu-id="5873d-258">Confirm that you see hello **input.log** file in hello **adfgetstarted/inputdata** folder in hello Azure blob storage, and run hello following command toodeploy hello pipeline.</span></span> <span data-ttu-id="5873d-259">Ponieważ hello **start** i **zakończenia** czasy są ustawiane w przeszłości hello i **isPaused** jest zestaw toofalse, potoku hello (działania w potoku hello) uruchamia natychmiast po wdrożeniu.</span><span class="sxs-lookup"><span data-stu-id="5873d-259">Since hello **start** and **end** times are set in hello past and **isPaused** is set toofalse, hello pipeline (activity in hello pipeline) runs immediately after you deploy.</span></span>

    ```PowerShell
    New-AzureRmDataFactoryPipeline $df -File .\MyFirstPipelinePSH.json
    ```
3. <span data-ttu-id="5873d-260">Gratulacje! Udało Ci się utworzyć pierwszy potok przy użyciu programu Azure PowerShell!</span><span class="sxs-lookup"><span data-stu-id="5873d-260">Congratulations, you have successfully created your first pipeline using Azure PowerShell!</span></span>

## <a name="monitor-pipeline"></a><span data-ttu-id="5873d-261">Monitorowanie potoku</span><span class="sxs-lookup"><span data-stu-id="5873d-261">Monitor pipeline</span></span>
<span data-ttu-id="5873d-262">W tym kroku użyjesz programu Azure PowerShell toomonitor co się dzieje w fabryce danych Azure.</span><span class="sxs-lookup"><span data-stu-id="5873d-262">In this step, you use Azure PowerShell toomonitor what’s going on in an Azure data factory.</span></span>

1. <span data-ttu-id="5873d-263">Uruchom **Get-AzureRmDataFactory** i przypisz hello dane wyjściowe tooa **$df** zmiennej.</span><span class="sxs-lookup"><span data-stu-id="5873d-263">Run **Get-AzureRmDataFactory** and assign hello output tooa **$df** variable.</span></span>

    ```PowerShell
    $df=Get-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name FirstDataFactoryPSH
    ```
2. <span data-ttu-id="5873d-264">Uruchom **Get-AzureRmDataFactorySlice** tooget szczegóły wszystkie fragmenty hello **EmpSQLTable**, która jest tabela wyjściowa hello hello potoku.</span><span class="sxs-lookup"><span data-stu-id="5873d-264">Run **Get-AzureRmDataFactorySlice** tooget details about all slices of hello **EmpSQLTable**, which is hello output table of hello pipeline.</span></span>

    ```PowerShell
    Get-AzureRmDataFactorySlice $df -DatasetName AzureBlobOutput -StartDateTime 2017-07-01
    ```
    <span data-ttu-id="5873d-265">Należy zauważyć, że hello StartDateTime określone w tym miejscu jest hello sam określono godzinę rozpoczęcia w potoku hello JSON.</span><span class="sxs-lookup"><span data-stu-id="5873d-265">Notice that hello StartDateTime you specify here is hello same start time specified in hello pipeline JSON.</span></span> <span data-ttu-id="5873d-266">Oto hello przykładowe dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="5873d-266">Here is hello sample output:</span></span>

    ```PowerShell
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : FirstDataFactoryPSH
    DatasetName       : AzureBlobOutput
    Start             : 7/1/2017 12:00:00 AM
    End               : 7/2/2017 12:00:00 AM
    RetryCount        : 0
    State             : InProgress
    SubState          :
    LatencyStatus     :
    LongRetryCount    : 0
    ```
3. <span data-ttu-id="5873d-267">Uruchom **Get-AzureRmDataFactoryRun** tooget hello szczegółów działania jest uruchamiana dla określonych wycinka.</span><span class="sxs-lookup"><span data-stu-id="5873d-267">Run **Get-AzureRmDataFactoryRun** tooget hello details of activity runs for a specific slice.</span></span>

    ```PowerShell
    Get-AzureRmDataFactoryRun $df -DatasetName AzureBlobOutput -StartDateTime 2017-07-01
    ```

    <span data-ttu-id="5873d-268">Oto hello przykładowe dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="5873d-268">Here is hello sample output:</span></span> 

    ```PowerShell
    Id                  : 0f6334f2-d56c-4d48-b427-d4f0fb4ef883_635268096000000000_635292288000000000_AzureBlobOutput
    ResourceGroupName   : ADFTutorialResourceGroup
    DataFactoryName     : FirstDataFactoryPSH
    DatasetName         : AzureBlobOutput
    ProcessingStartTime : 12/18/2015 4:50:33 AM
    ProcessingEndTime   : 12/31/9999 11:59:59 PM
    PercentComplete     : 0
    DataSliceStart      : 7/1/2017 12:00:00 AM
    DataSliceEnd        : 7/2/2017 12:00:00 AM
    Status              : AllocatingResources
    Timestamp           : 12/18/2015 4:50:33 AM
    RetryAttempt        : 0
    Properties          : {}
    ErrorMessage        :
    ActivityName        : RunSampleHiveActivity
    PipelineName        : MyFirstPipeline
    Type                : Script
    ```
    <span data-ttu-id="5873d-269">Możesz można zachować uruchomienie tego polecenia cmdlet do momentu wyświetlenia wycinek hello **gotowe** stanu lub **** stanu.</span><span class="sxs-lookup"><span data-stu-id="5873d-269">You can keep running this cmdlet until you see hello slice in **Ready** state or **Failed** state.</span></span> <span data-ttu-id="5873d-270">Gdy wycinek hello jest w stanie gotowe, sprawdź hello **partitioneddata** folderu w hello **adfgetstarted** kontenera w magazynie obiektów blob na powitania dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="5873d-270">When hello slice is in Ready state, check hello **partitioneddata** folder in hello **adfgetstarted** container in your blob storage for hello output data.</span></span>  <span data-ttu-id="5873d-271">Tworzenie klastra usługi HDInsight na żądanie zwykle zajmuje trochę czasu.</span><span class="sxs-lookup"><span data-stu-id="5873d-271">Creation of an on-demand HDInsight cluster usually takes some time.</span></span>

    ![Dane wyjściowe](./media/data-factory-build-your-first-pipeline-using-powershell/three-ouptut-files.png)

> [!IMPORTANT]
> <span data-ttu-id="5873d-273">Tworzenie klastra usługi HDInsight na żądanie zwykle trwa trochę czasu (około 20 minut).</span><span class="sxs-lookup"><span data-stu-id="5873d-273">Creation of an on-demand HDInsight cluster usually takes sometime (approximately 20 minutes).</span></span> <span data-ttu-id="5873d-274">W związku z tym spodziewać się hello potoku tootake **około 30 minut** tooprocess hello wycinka.</span><span class="sxs-lookup"><span data-stu-id="5873d-274">Therefore, expect hello pipeline tootake **approximately 30 minutes** tooprocess hello slice.</span></span>
>
> <span data-ttu-id="5873d-275">Plik wejściowy Hello zostaje usunięta, gdy hello wycinek jest przetwarzany pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="5873d-275">hello input file gets deleted when hello slice is processed successfully.</span></span> <span data-ttu-id="5873d-276">W związku z tym hello plik wejściowy (input.log) toohello inputdata folder kontenera adfgetstarted hello przekazywania wycinek hello toorerun lub Witaj ponownie samouczek.</span><span class="sxs-lookup"><span data-stu-id="5873d-276">Therefore, if you want toorerun hello slice or do hello tutorial again, upload hello input file (input.log) toohello inputdata folder of hello adfgetstarted container.</span></span>
>
>

## <a name="summary"></a><span data-ttu-id="5873d-277">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="5873d-277">Summary</span></span>
<span data-ttu-id="5873d-278">W tym samouczku danych tooprocess fabryki danych Azure została utworzona przez uruchomienie skryptu Hive w klastrze HDInsight hadoop.</span><span class="sxs-lookup"><span data-stu-id="5873d-278">In this tutorial, you created an Azure data factory tooprocess data by running Hive script on a HDInsight hadoop cluster.</span></span> <span data-ttu-id="5873d-279">Użyto hello Edytor fabryki danych w hello Azure toodo portalu hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="5873d-279">You used hello Data Factory Editor in hello Azure portal toodo hello following steps:</span></span>

1. <span data-ttu-id="5873d-280">Tworzenie **fabryki danych** Azure.</span><span class="sxs-lookup"><span data-stu-id="5873d-280">Created an Azure **data factory**.</span></span>
2. <span data-ttu-id="5873d-281">Utworzyć dwie **połączone usługi**:</span><span class="sxs-lookup"><span data-stu-id="5873d-281">Created two **linked services**:</span></span>
   1. <span data-ttu-id="5873d-282">**Usługa Azure Storage** połączone usługi toolink Twojego magazynu Azure blob storage przechowuje pliki danych wejściowych/wyjściowych toohello usługi fabryka danych.</span><span class="sxs-lookup"><span data-stu-id="5873d-282">**Azure Storage** linked service toolink your Azure blob storage that holds input/output files toohello data factory.</span></span>
   2. <span data-ttu-id="5873d-283">**Usługa Azure HDInsight** na żądanie połączone usługi toolink fabrykę danych toohello klastra usługi HDInsight Hadoop na żądanie.</span><span class="sxs-lookup"><span data-stu-id="5873d-283">**Azure HDInsight** on-demand linked service toolink an on-demand HDInsight Hadoop cluster toohello data factory.</span></span> <span data-ttu-id="5873d-284">Fabryka danych Azure tworzy HDInsight Hadoop dane wejściowe w czasie tooprocess klastra i danych wyjściowych produktu.</span><span class="sxs-lookup"><span data-stu-id="5873d-284">Azure Data Factory creates a HDInsight Hadoop cluster just-in-time tooprocess input data and produce output data.</span></span>
3. <span data-ttu-id="5873d-285">Utworzone dwie **zestawów danych**, które opisują danych wejściowych i wyjściowych dla działania HDInsight Hive w potoku hello.</span><span class="sxs-lookup"><span data-stu-id="5873d-285">Created two **datasets**, which describe input and output data for HDInsight Hive activity in hello pipeline.</span></span>
4. <span data-ttu-id="5873d-286">Utworzyć **potok** za pomocą działania **programu Hive w usłudze HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="5873d-286">Created a **pipeline** with a **HDInsight Hive** activity.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5873d-287">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5873d-287">Next steps</span></span>
<span data-ttu-id="5873d-288">W tym artykule opisano tworzenie potoku za pomocą działania przekształcania (działanie usługi HDInsight), które uruchamia skrypt programu Hive w klastrze usługi HDInsight platformy Azure na żądanie.</span><span class="sxs-lookup"><span data-stu-id="5873d-288">In this article, you have created a pipeline with a transformation activity (HDInsight Activity) that runs a Hive script on an on-demand Azure HDInsight cluster.</span></span> <span data-ttu-id="5873d-289">toosee toouse toocopy działanie kopiowania danych z tooAzure obiektów Blob platformy Azure SQL, zobacz temat [samouczek: kopiowanie danych z obiektu Blob Azure tooAzure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="5873d-289">toosee how toouse a Copy Activity toocopy data from an Azure Blob tooAzure SQL, see [Tutorial: Copy data from an Azure Blob tooAzure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="5873d-290">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="5873d-290">See Also</span></span>
| <span data-ttu-id="5873d-291">Temat</span><span class="sxs-lookup"><span data-stu-id="5873d-291">Topic</span></span> | <span data-ttu-id="5873d-292">Opis</span><span class="sxs-lookup"><span data-stu-id="5873d-292">Description</span></span> |
|:--- |:--- |
| [<span data-ttu-id="5873d-293">Dokumentacja dotycząca poleceń cmdlet usługi Data Factory</span><span class="sxs-lookup"><span data-stu-id="5873d-293">Data Factory Cmdlet Reference</span></span>](/powershell/module/azurerm.datafactories) |<span data-ttu-id="5873d-294">Zobacz pełną dokumentację dotyczącą poleceń cmdlet w usłudze Fabryka danych.</span><span class="sxs-lookup"><span data-stu-id="5873d-294">See comprehensive documentation on Data Factory cmdlets</span></span> |
| [<span data-ttu-id="5873d-295">Potoki</span><span class="sxs-lookup"><span data-stu-id="5873d-295">Pipelines</span></span>](data-factory-create-pipelines.md) |<span data-ttu-id="5873d-296">Ten artykuł pomaga w zrozumieniu potoki i działań w fabryce danych Azure i w jaki sposób toouse ich tooconstruct end-to-end danymi przepływy pracy dla Twojego scenariusza lub firmy.</span><span class="sxs-lookup"><span data-stu-id="5873d-296">This article helps you understand pipelines and activities in Azure Data Factory and how toouse them tooconstruct end-to-end data-driven workflows for your scenario or business.</span></span> |
| [<span data-ttu-id="5873d-297">Zestawy danych</span><span class="sxs-lookup"><span data-stu-id="5873d-297">Datasets</span></span>](data-factory-create-datasets.md) |<span data-ttu-id="5873d-298">Ten artykuł ułatwia zapoznanie się z zestawami danych w usłudze Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="5873d-298">This article helps you understand datasets in Azure Data Factory.</span></span> |
| [<span data-ttu-id="5873d-299">Planowanie i wykonywanie</span><span class="sxs-lookup"><span data-stu-id="5873d-299">Scheduling and Execution</span></span>](data-factory-scheduling-and-execution.md) |<span data-ttu-id="5873d-300">W tym artykule opisano aspekty planowania i wykonywania hello modelu aplikacji fabryki danych Azure.</span><span class="sxs-lookup"><span data-stu-id="5873d-300">This article explains hello scheduling and execution aspects of Azure Data Factory application model.</span></span> |
| [<span data-ttu-id="5873d-301">Monitorowanie potoków i zarządzanie nimi za pomocą aplikacji do monitorowania</span><span class="sxs-lookup"><span data-stu-id="5873d-301">Monitor and manage pipelines using Monitoring App</span></span>](data-factory-monitor-manage-app.md) |<span data-ttu-id="5873d-302">W tym artykule opisano sposób toomonitor, zarządzania i debugowania potoki przy użyciu hello monitorowanie & aplikacji do zarządzania.</span><span class="sxs-lookup"><span data-stu-id="5873d-302">This article describes how toomonitor, manage, and debug pipelines using hello Monitoring & Management App.</span></span> |
