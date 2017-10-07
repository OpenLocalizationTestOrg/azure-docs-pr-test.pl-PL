---
title: "Samouczek: Użyj interfejsu API REST toocreate potoku fabryki danych Azure | Dokumentacja firmy Microsoft"
description: "W tym samouczku należy użyć interfejsu API REST toocreate potoku fabryki danych Azure z toocopy działanie kopiowania danych z magazynu obiektów blob platformy Azure bazy danych Azure SQL."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 1704cdf8-30ad-49bc-a71c-4057e26e7350
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: aa6c9b035101c4ff9acff90117ca6e3e7067f418
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-use-rest-api-toocreate-an-azure-data-factory-pipeline-toocopy-data"></a><span data-ttu-id="7d5d9-103">Samouczek: Użyj interfejsu API REST toocreate danych toocopy potoku fabryki danych Azure</span><span class="sxs-lookup"><span data-stu-id="7d5d9-103">Tutorial: Use REST API toocreate an Azure Data Factory pipeline toocopy data</span></span> 
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7d5d9-104">Przegląd i wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="7d5d9-104">Overview and prerequisites</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [<span data-ttu-id="7d5d9-105">Kreator kopiowania</span><span class="sxs-lookup"><span data-stu-id="7d5d9-105">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
> * [<span data-ttu-id="7d5d9-106">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="7d5d9-106">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [<span data-ttu-id="7d5d9-107">Program Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7d5d9-107">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [<span data-ttu-id="7d5d9-108">Program PowerShell</span><span class="sxs-lookup"><span data-stu-id="7d5d9-108">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
> * [<span data-ttu-id="7d5d9-109">Szablon usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="7d5d9-109">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [<span data-ttu-id="7d5d9-110">Interfejs API REST</span><span class="sxs-lookup"><span data-stu-id="7d5d9-110">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [<span data-ttu-id="7d5d9-111">Interfejs API .NET</span><span class="sxs-lookup"><span data-stu-id="7d5d9-111">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)
> 
> 

<span data-ttu-id="7d5d9-112">W tym artykule dowiesz się, jak toouse REST API toocreate fabryki danych z potok, który kopiuje dane z bazy danych Azure SQL tooan magazynu obiektów blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-112">In this article, you learn how toouse REST API toocreate a data factory with a pipeline that copies data from an Azure blob storage tooan Azure SQL database.</span></span> <span data-ttu-id="7d5d9-113">Jeśli nowy tooAzure fabryki danych, zapoznaj się z artykułem hello [tooAzure wprowadzenie fabryki danych](data-factory-introduction.md) artykuł przed wykonaniem tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-113">If you are new tooAzure Data Factory, read through hello [Introduction tooAzure Data Factory](data-factory-introduction.md) article before doing this tutorial.</span></span>   

<span data-ttu-id="7d5d9-114">W tym samouczku opisano tworzenie potoku z jednym działaniem (Działanie kopiowania).</span><span class="sxs-lookup"><span data-stu-id="7d5d9-114">In this tutorial, you create a pipeline with one activity in it: Copy Activity.</span></span> <span data-ttu-id="7d5d9-115">działanie kopiowania Hello kopiuje dane z magazynu danych obsługiwanych ujścia magazynu tooa obsługiwane dane.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-115">hello copy activity copies data from a supported data store tooa supported sink data store.</span></span> <span data-ttu-id="7d5d9-116">Aby zapoznać się z listą magazynów danych obsługiwanych jako źródła i ujścia, zobacz [obsługiwane magazyny danych](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="7d5d9-116">For a list of data stores supported as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="7d5d9-117">działanie Hello jest obsługiwany przez ogólnie dostępna usługa, która można skopiować dane między różnych magazynach danych w sposób bezpieczny, niezawodny i skalowalności.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-117">hello activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="7d5d9-118">Aby uzyskać więcej informacji na temat hello działanie kopiowania, zobacz [działań przepływu danych](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="7d5d9-118">For more information about hello Copy Activity, see [Data Movement Activities](data-factory-data-movement-activities.md).</span></span>

<span data-ttu-id="7d5d9-119">Potok może obejmować więcej niż jedno działanie.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-119">A pipeline can have more than one activity.</span></span> <span data-ttu-id="7d5d9-120">I tworzenia łańcucha dwa działania (Uruchom jedno działanie po drugim), ustawiając hello wyjściowy zestaw danych z jednego działania jako hello wejściowy zestaw danych z hello innych działań.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-120">And, you can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="7d5d9-121">Aby uzyskać więcej informacji, zobacz sekcję dotyczącą [wielu działań w potoku](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span><span class="sxs-lookup"><span data-stu-id="7d5d9-121">For more information, see [multiple activities in a pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span>

> [!NOTE]
> <span data-ttu-id="7d5d9-122">W tym artykule nie opisano wszystkich hello interfejsu API REST fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-122">This article does not cover all hello Data Factory REST API.</span></span> <span data-ttu-id="7d5d9-123">Pełna dokumentacja dotycząca poleceń cmdlet usługi Data Factory znajduje się w artykule [Data Factory Cmdlet Reference](/rest/api/datafactory/) (Dokumentacja dotycząca interfejsu API REST usługi Data Factory).</span><span class="sxs-lookup"><span data-stu-id="7d5d9-123">See [Data Factory REST API Reference](/rest/api/datafactory/) for comprehensive documentation on Data Factory cmdlets.</span></span>
>  
> <span data-ttu-id="7d5d9-124">Witaj potoku danych w tym samouczku kopiuje dane z magazynu danych źródła danych magazynu tooa docelowego.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-124">hello data pipeline in this tutorial copies data from a source data store tooa destination data store.</span></span> <span data-ttu-id="7d5d9-125">Samouczek na temat danych tootransform przy użyciu fabryki danych Azure, zobacz [samouczek: Tworzenie danych tootransform potoku, przy użyciu klastra usługi Hadoop](data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="7d5d9-125">For a tutorial on how tootransform data using Azure Data Factory, see [Tutorial: Build a pipeline tootransform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7d5d9-126">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="7d5d9-126">Prerequisites</span></span>
* <span data-ttu-id="7d5d9-127">Przejdź przez [— samouczek Przegląd](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) i pełne hello **wymagań wstępnych** czynności.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-127">Go through [Tutorial Overview](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) and complete hello **prerequisite** steps.</span></span>
* <span data-ttu-id="7d5d9-128">Zainstaluj na komputerze narzędzie [Curl](https://curl.haxx.se/dlwiz/).</span><span class="sxs-lookup"><span data-stu-id="7d5d9-128">Install [Curl](https://curl.haxx.se/dlwiz/) on your machine.</span></span> <span data-ttu-id="7d5d9-129">Narzędzie Curl hello jest używany z toocreate polecenia REST fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-129">You use hello Curl tool with REST commands toocreate a data factory.</span></span> 
* <span data-ttu-id="7d5d9-130">Postępuj zgodnie z instrukcjami zawartymi w [tym artykule](../azure-resource-manager/resource-group-create-service-principal-portal.md), aby wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="7d5d9-130">Follow instructions from [this article](../azure-resource-manager/resource-group-create-service-principal-portal.md) to:</span></span> 
  1. <span data-ttu-id="7d5d9-131">Utworzenie aplikacji sieci Web o nazwie **ADFCopyTutorialApp** w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-131">Create a Web application named **ADFCopyTutorialApp** in Azure Active Directory.</span></span>
  2. <span data-ttu-id="7d5d9-132">Pobranie **identyfikatora klienta** i **klucza tajnego**.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-132">Get **client ID** and **secret key**.</span></span> 
  3. <span data-ttu-id="7d5d9-133">Uzyskanie **identyfikatora dzierżawy**.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-133">Get **tenant ID**.</span></span> 
  4. <span data-ttu-id="7d5d9-134">Przypisz hello **ADFCopyTutorialApp** toohello aplikacji **współautora fabryki danych** roli.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-134">Assign hello **ADFCopyTutorialApp** application toohello **Data Factory Contributor** role.</span></span>  
* <span data-ttu-id="7d5d9-135">Zainstaluj program [Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="7d5d9-135">Install [Azure PowerShell](/powershell/azure/overview).</span></span>  
* <span data-ttu-id="7d5d9-136">Uruchom **PowerShell** i hello następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-136">Launch **PowerShell** and do hello following steps.</span></span> <span data-ttu-id="7d5d9-137">Nie zamykaj programu Azure PowerShell do momentu zakończenia hello tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-137">Keep Azure PowerShell open until hello end of this tutorial.</span></span> <span data-ttu-id="7d5d9-138">Zamknij i otwórz ponownie, należy najpierw polecenia hello toorun ponownie.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-138">If you close and reopen, you need toorun hello commands again.</span></span>
  
  1. <span data-ttu-id="7d5d9-139">Uruchom następujące polecenie hello i wprowadź hello nazwę użytkownika i hasło, użyj toosign w toohello portalu Azure:</span><span class="sxs-lookup"><span data-stu-id="7d5d9-139">Run hello following command and enter hello user name and password that you use toosign in toohello Azure portal:</span></span>
    
    ```PowerShell 
    Login-AzureRmAccount
    ```   
  2. <span data-ttu-id="7d5d9-140">Uruchom następujące polecenie tooview hello wszystkie subskrypcje powitania dla tego konta:</span><span class="sxs-lookup"><span data-stu-id="7d5d9-140">Run hello following command tooview all hello subscriptions for this account:</span></span>

    ```PowerShell     
    Get-AzureRmSubscription
    ``` 
  3. <span data-ttu-id="7d5d9-141">Uruchom następujące polecenie tooselect hello subskrypcję, która ma toowork z hello.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-141">Run hello following command tooselect hello subscription that you want toowork with.</span></span> <span data-ttu-id="7d5d9-142">Zastąp  **&lt;NameOfAzureSubscription** &gt; o nazwie hello subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-142">Replace **&lt;NameOfAzureSubscription**&gt; with hello name of your Azure subscription.</span></span> 
     
    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <NameOfAzureSubscription> | Set-AzureRmContext
    ```
  4. <span data-ttu-id="7d5d9-143">Tworzenie grupy zasobów platformy Azure o nazwie **ADFTutorialResourceGroup** , uruchamiając następujące polecenie w środowiska PowerShell hello hello:</span><span class="sxs-lookup"><span data-stu-id="7d5d9-143">Create an Azure resource group named **ADFTutorialResourceGroup** by running hello following command in hello PowerShell:</span></span>  

    ```PowerShell     
      New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```
     
      <span data-ttu-id="7d5d9-144">Jeśli hello grupy zasobów już istnieje, określić czy tooupdate go (Y) lub zachować go jako (N).</span><span class="sxs-lookup"><span data-stu-id="7d5d9-144">If hello resource group already exists, you specify whether tooupdate it (Y) or keep it as (N).</span></span> 
     
      <span data-ttu-id="7d5d9-145">Niektóre kroki hello w tym samouczku Załóżmy, że hello grupy zasobów o nazwie ADFTutorialResourceGroup.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-145">Some of hello steps in this tutorial assume that you use hello resource group named ADFTutorialResourceGroup.</span></span> <span data-ttu-id="7d5d9-146">Jeśli używasz innej grupie zasobów, należy toouse hello Nazwa grupy zasobów, zamiast ADFTutorialResourceGroup w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-146">If you use a different resource group, you need toouse hello name of your resource group in place of ADFTutorialResourceGroup in this tutorial.</span></span>

## <a name="create-json-definitions"></a><span data-ttu-id="7d5d9-147">Tworzenie definicji JSON</span><span class="sxs-lookup"><span data-stu-id="7d5d9-147">Create JSON definitions</span></span>
<span data-ttu-id="7d5d9-148">Utwórz następujące pliki w folderze hello, w którym znajduje się curl.exe w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-148">Create following JSON files in hello folder where curl.exe is located.</span></span> 

### <a name="datafactoryjson"></a><span data-ttu-id="7d5d9-149">datafactory.json</span><span class="sxs-lookup"><span data-stu-id="7d5d9-149">datafactory.json</span></span>
> [!IMPORTANT]
> <span data-ttu-id="7d5d9-150">Nazwa musi być unikatowe globalnie, dlatego może być toomake ADFCopyTutorialDF tooprefix/sufiksu go unikatową nazwę.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-150">Name must be globally unique, so you may want tooprefix/suffix ADFCopyTutorialDF toomake it a unique name.</span></span> 
> 
> 

```JSON
{  
    "name": "ADFCopyTutorialDF",  
    "location": "WestUS"
}  
```

### <a name="azurestoragelinkedservicejson"></a><span data-ttu-id="7d5d9-151">azurestoragelinkedservice.json</span><span class="sxs-lookup"><span data-stu-id="7d5d9-151">azurestoragelinkedservice.json</span></span>
> [!IMPORTANT]
> <span data-ttu-id="7d5d9-152">Zastąp wartości **accountname** i **accountkey** nazwą konta usługi Azure Storage oraz jego kluczem.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-152">Replace **accountname** and **accountkey** with name and key of your Azure storage account.</span></span> <span data-ttu-id="7d5d9-153">toolearn jak tooget Twojego magazynu uzyskują dostęp do klucza, zobacz [widoku, kopiowania i regenerate magazynu klucze dostępu](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).</span><span class="sxs-lookup"><span data-stu-id="7d5d9-153">toolearn how tooget your storage access key, see [View, copy and regenerate storage access keys](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).</span></span>

```JSON
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

<span data-ttu-id="7d5d9-154">Aby uzyskać więcej informacji o właściwościach JSON, zobacz temat dotyczący [połączonej usługi Azure Storage](data-factory-azure-blob-connector.md#azure-storage-linked-service).</span><span class="sxs-lookup"><span data-stu-id="7d5d9-154">For details about JSON properties, see [Azure Storage linked service](data-factory-azure-blob-connector.md#azure-storage-linked-service).</span></span>

### <a name="azuersqllinkedservicejson"></a><span data-ttu-id="7d5d9-155">azuersqllinkedservice.json</span><span class="sxs-lookup"><span data-stu-id="7d5d9-155">azuersqllinkedservice.json</span></span>
> [!IMPORTANT]
> <span data-ttu-id="7d5d9-156">Zastąp **servername**, **databasename**, **username**, i **hasło** z nazwą swojego serwera Azure SQL, nazwa bazy danych SQL, użytkownika Konto i hasło dla konta hello.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-156">Replace **servername**, **databasename**, **username**, and **password** with name of your Azure SQL server, name of SQL database, user account, and password for hello account.</span></span>  
> 
>

```JSON
{
    "name": "AzureSqlLinkedService",
    "properties": {
        "type": "AzureSqlDatabase",
        "description": "",
        "typeProperties": {
            "connectionString": "Data Source=tcp:<servername>.database.windows.net,1433;Initial Catalog=<databasename>;User ID=<username>;Password=<password>;Integrated Security=False;Encrypt=True;Connect Timeout=30"
        }
    }
}
```

<span data-ttu-id="7d5d9-157">Aby uzyskać szczegółowe informacje o właściwościach JSON, zobacz temat dotyczący [połączonej usługi Azure SQL](data-factory-azure-sql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="7d5d9-157">For details about JSON properties, see [Azure SQL linked service](data-factory-azure-sql-connector.md#linked-service-properties).</span></span>

### <a name="inputdatasetjson"></a><span data-ttu-id="7d5d9-158">inputdataset.json</span><span class="sxs-lookup"><span data-stu-id="7d5d9-158">inputdataset.json</span></span>

```JSON
{
  "name": "AzureBlobInput",
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
      "folderPath": "adftutorial/",
      "fileName": "emp.txt",
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

<span data-ttu-id="7d5d9-159">Witaj Poniższa tabela zawiera opisy właściwości JSON hello używane we fragmencie hello:</span><span class="sxs-lookup"><span data-stu-id="7d5d9-159">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

| <span data-ttu-id="7d5d9-160">Właściwość</span><span class="sxs-lookup"><span data-stu-id="7d5d9-160">Property</span></span> | <span data-ttu-id="7d5d9-161">Opis</span><span class="sxs-lookup"><span data-stu-id="7d5d9-161">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="7d5d9-162">type</span><span class="sxs-lookup"><span data-stu-id="7d5d9-162">type</span></span> | <span data-ttu-id="7d5d9-163">Właściwość type Hello ustawiono zbyt**AzureBlob** ponieważ danych znajduje się w magazynie obiektów blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-163">hello type property is set too**AzureBlob** because data resides in an Azure blob storage.</span></span> |
| <span data-ttu-id="7d5d9-164">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="7d5d9-164">linkedServiceName</span></span> | <span data-ttu-id="7d5d9-165">Odwołuje się toohello **AzureStorageLinkedService** utworzony wcześniej.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-165">Refers toohello **AzureStorageLinkedService** that you created earlier.</span></span> |
| <span data-ttu-id="7d5d9-166">folderPath</span><span class="sxs-lookup"><span data-stu-id="7d5d9-166">folderPath</span></span> | <span data-ttu-id="7d5d9-167">Określa obiekt blob hello **kontenera** i hello **folderu** zawiera obiekty BLOB wejściowego.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-167">Specifies hello blob **container** and hello **folder** that contains input blobs.</span></span> <span data-ttu-id="7d5d9-168">W tym samouczku adftutorial jest hello kontenera obiektów blob i hello folderu głównego.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-168">In this tutorial, adftutorial is hello blob container and folder is hello root folder.</span></span> | 
| <span data-ttu-id="7d5d9-169">fileName</span><span class="sxs-lookup"><span data-stu-id="7d5d9-169">fileName</span></span> | <span data-ttu-id="7d5d9-170">Ta właściwość jest opcjonalna.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-170">This property is optional.</span></span> <span data-ttu-id="7d5d9-171">W przypadku pominięcia tej właściwości, pobierane są wszystkie pliki z hello folderPath.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-171">If you omit this property, all files from hello folderPath are picked.</span></span> <span data-ttu-id="7d5d9-172">W tym samouczku **emp.txt** określona dla hello nazwę pliku, tak aby plik zostaje pobrana do przetwarzania.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-172">In this tutorial, **emp.txt** is specified for hello fileName, so only that file is picked up for processing.</span></span> |
| <span data-ttu-id="7d5d9-173">format -> type</span><span class="sxs-lookup"><span data-stu-id="7d5d9-173">format -> type</span></span> |<span data-ttu-id="7d5d9-174">Plik wejściowy Hello jest w formacie tekstowym hello, więc używamy **TextFormat**.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-174">hello input file is in hello text format, so we use **TextFormat**.</span></span> |
| <span data-ttu-id="7d5d9-175">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="7d5d9-175">columnDelimiter</span></span> | <span data-ttu-id="7d5d9-176">Witaj kolumn w pliku wejściowym hello są rozdzielane **przecinka (`,`)**.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-176">hello columns in hello input file are delimited by **comma character (`,`)**.</span></span> |
| <span data-ttu-id="7d5d9-177">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="7d5d9-177">frequency/interval</span></span> | <span data-ttu-id="7d5d9-178">częstotliwość Hello ustawiono zbyt**godzina** i interwał jest ustawiany za**1**, co oznacza, że hello wejściowych dostępnych wycinków **co godzinę**.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-178">hello frequency is set too**Hour** and interval is  set too**1**, which means that hello input slices are available **hourly**.</span></span> <span data-ttu-id="7d5d9-179">Innymi słowy, hello usługi fabryka danych sprawdza dane wejściowe co godzinę w folderze głównym hello kontenera obiektów blob (**adftutorial**) określone.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-179">In other words, hello Data Factory service looks for input data every hour in hello root folder of blob container (**adftutorial**) you specified.</span></span> <span data-ttu-id="7d5d9-180">Wyszukuje hello danych w ramach hello potoku rozpoczęcia i zakończenia godzin, nie przed lub po tych godzinach.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-180">It looks for hello data within hello pipeline start and end times, not before or after these times.</span></span>  |
| <span data-ttu-id="7d5d9-181">external</span><span class="sxs-lookup"><span data-stu-id="7d5d9-181">external</span></span> | <span data-ttu-id="7d5d9-182">Ta właściwość jest ustawiona zbyt**true** czy hello danych nie jest generowany przez tego potoku.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-182">This property is set too**true** if hello data is not generated by this pipeline.</span></span> <span data-ttu-id="7d5d9-183">Witaj danych wejściowych w tym samouczku jest hello emp.txt pliku, który nie jest generowany w tym potoku, możemy ustawić tootrue tej właściwości.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-183">hello input data in this tutorial is in hello emp.txt file, which is not generated by this pipeline, so we set this property tootrue.</span></span> |

<span data-ttu-id="7d5d9-184">Aby uzyskać więcej informacji o tych właściwościach JSON, zobacz [artykuł dotyczący łącznika obiektu blob platformy Azure](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="7d5d9-184">For more information about these JSON properties, see [Azure Blob connector article](data-factory-azure-blob-connector.md#dataset-properties).</span></span>

### <a name="outputdatasetjson"></a><span data-ttu-id="7d5d9-185">outputdataset.json</span><span class="sxs-lookup"><span data-stu-id="7d5d9-185">outputdataset.json</span></span>

```JSON
{
  "name": "AzureSqlOutput",
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
<span data-ttu-id="7d5d9-186">Witaj Poniższa tabela zawiera opisy właściwości JSON hello używane we fragmencie hello:</span><span class="sxs-lookup"><span data-stu-id="7d5d9-186">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

| <span data-ttu-id="7d5d9-187">Właściwość</span><span class="sxs-lookup"><span data-stu-id="7d5d9-187">Property</span></span> | <span data-ttu-id="7d5d9-188">Opis</span><span class="sxs-lookup"><span data-stu-id="7d5d9-188">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="7d5d9-189">type</span><span class="sxs-lookup"><span data-stu-id="7d5d9-189">type</span></span> | <span data-ttu-id="7d5d9-190">Właściwość type Hello ustawiono zbyt**AzureSqlTable** , ponieważ dane są kopiowane tooa tabeli w bazie danych Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-190">hello type property is set too**AzureSqlTable** because data is copied tooa table in an Azure SQL database.</span></span> |
| <span data-ttu-id="7d5d9-191">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="7d5d9-191">linkedServiceName</span></span> | <span data-ttu-id="7d5d9-192">Odwołuje się toohello **AzureSqlLinkedService** utworzony wcześniej.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-192">Refers toohello **AzureSqlLinkedService** that you created earlier.</span></span> |
| <span data-ttu-id="7d5d9-193">tableName</span><span class="sxs-lookup"><span data-stu-id="7d5d9-193">tableName</span></span> | <span data-ttu-id="7d5d9-194">Określony hello **tabeli** toowhich hello dane są kopiowane.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-194">Specified hello **table** toowhich hello data is copied.</span></span> | 
| <span data-ttu-id="7d5d9-195">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="7d5d9-195">frequency/interval</span></span> | <span data-ttu-id="7d5d9-196">Witaj częstotliwość ustawiono zbyt**godzina** i interwał **1**, co oznacza, że wycinki danych wyjściowych hello są produkowane **co godzinę** między hello potoku rozpoczęcia i zakończenia godzin przed nie lub Po tych godzinach.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-196">hello frequency is set too**Hour** and interval is **1**, which means that hello output slices are produced **hourly** between hello pipeline start and end times, not before or after these times.</span></span>  |

<span data-ttu-id="7d5d9-197">Istnieją trzy kolumny — **identyfikator**, **imię**, i **nazwisko** — Witaj pustych elementów tabeli w bazie danych hello.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-197">There are three columns – **ID**, **FirstName**, and **LastName** – in hello emp table in hello database.</span></span> <span data-ttu-id="7d5d9-198">Identyfikator jest kolumny tożsamości, więc musisz tylko toospecify **imię** i **nazwisko** tutaj.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-198">ID is an identity column, so you need toospecify only **FirstName** and **LastName** here.</span></span>

<span data-ttu-id="7d5d9-199">Aby uzyskać więcej informacji o tych właściwościach JSON, zobacz [artykuł dotyczący łącznika usługi Azure SQL](data-factory-azure-sql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="7d5d9-199">For more information about these JSON properties, see [Azure SQL connector article](data-factory-azure-sql-connector.md#dataset-properties).</span></span>

### <a name="pipelinejson"></a><span data-ttu-id="7d5d9-200">pipeline.json</span><span class="sxs-lookup"><span data-stu-id="7d5d9-200">pipeline.json</span></span>

```JSON
{
  "name": "ADFTutorialPipeline",
  "properties": {
    "description": "Copy data from a blob tooAzure SQL table",
    "activities": [
      {
        "name": "CopyFromBlobToSQL",
        "description": "Push Regional Effectiveness Campaign data tooAzure SQL database",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureBlobInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureSqlOutput"
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

<span data-ttu-id="7d5d9-201">Należy zwrócić uwagę hello następujące punkty:</span><span class="sxs-lookup"><span data-stu-id="7d5d9-201">Note hello following points:</span></span>

- <span data-ttu-id="7d5d9-202">W sekcji działania hello jest tylko jedno działanie którego **typu** ustawiono zbyt**kopiowania**.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-202">In hello activities section, there is only one activity whose **type** is set too**Copy**.</span></span> <span data-ttu-id="7d5d9-203">Aby uzyskać więcej informacji o działaniu kopiowania hello, zobacz [działań przepływu danych](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="7d5d9-203">For more information about hello copy activity, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="7d5d9-204">W rozwiązaniach usługi Data Factory można również użyć [działań dotyczących przekształcania danych](data-factory-data-transformation-activities.md).</span><span class="sxs-lookup"><span data-stu-id="7d5d9-204">In Data Factory solutions, you can also use [data transformation activities](data-factory-data-transformation-activities.md).</span></span>
- <span data-ttu-id="7d5d9-205">Dane wejściowe dla działania hello jest ustawiony za**AzureBlobInput** i danych wyjściowych dla działania hello jest ustawiony za**AzureSqlOutput**.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-205">Input for hello activity is set too**AzureBlobInput** and output for hello activity is set too**AzureSqlOutput**.</span></span> 
- <span data-ttu-id="7d5d9-206">W hello **typeProperties** sekcji **BlobSource** jest określony jako typ źródła hello i **SqlSink** jest określony jako typ ujścia hello.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-206">In hello **typeProperties** section, **BlobSource** is specified as hello source type and **SqlSink** is specified as hello sink type.</span></span> <span data-ttu-id="7d5d9-207">Aby uzyskać pełną listę obsługiwanych przez działanie kopiowania hello jako źródła i wychwytywanie magazyny danych, zobacz [obsługiwane magazyny danych](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="7d5d9-207">For a complete list of data stores supported by hello copy activity as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="7d5d9-208">toolearn jak przechowywać toouse określonych danych obsługiwane jako źródło/ujście, kliknij łącze hello hello tabeli.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-208">toolearn how toouse a specific supported data store as a source/sink, click hello link in hello table.</span></span>  
 
<span data-ttu-id="7d5d9-209">Zastąp wartość hello hello **start** właściwość o hello bieżącego dnia i **zakończenia** wartości z hello następnego dnia.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-209">Replace hello value of hello **start** property with hello current day and **end** value with hello next day.</span></span> <span data-ttu-id="7d5d9-210">Można określić tylko część daty hello i Pomiń hello czas część hello Data i godzina.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-210">You can specify only hello date part and skip hello time part of hello date time.</span></span> <span data-ttu-id="7d5d9-211">Na przykład "2017-02-03", która odpowiada za "2017-02-03T00:00:00Z"</span><span class="sxs-lookup"><span data-stu-id="7d5d9-211">For example, "2017-02-03", which is equivalent too"2017-02-03T00:00:00Z"</span></span>
 
<span data-ttu-id="7d5d9-212">Zarówno data/godzina rozpoczęcia, jak i data/godzina zakończenia muszą być w [formacie ISO](http://en.wikipedia.org/wiki/ISO_8601).</span><span class="sxs-lookup"><span data-stu-id="7d5d9-212">Both start and end datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="7d5d9-213">Przykładowo: 2016-10-14T16:32:41Z.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-213">For example: 2016-10-14T16:32:41Z.</span></span> <span data-ttu-id="7d5d9-214">Witaj **zakończenia** czasu jest opcjonalne, ale możemy użyć w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-214">hello **end** time is optional, but we use it in this tutorial.</span></span> 
 
<span data-ttu-id="7d5d9-215">Jeśli nie określisz wartości hello **zakończenia** właściwości, jest on obliczany jako "**start + 48 godzin**".</span><span class="sxs-lookup"><span data-stu-id="7d5d9-215">If you do not specify value for hello **end** property, it is calculated as "**start + 48 hours**".</span></span> <span data-ttu-id="7d5d9-216">potok hello toorun przez czas nieokreślony, określ **9999-09-09** jako wartość hello hello **zakończenia** właściwości.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-216">toorun hello pipeline indefinitely, specify **9999-09-09** as hello value for hello **end** property.</span></span>
 
<span data-ttu-id="7d5d9-217">W hello poprzedzających przykład istnieją 24 wycinków danych, jak każdy wycinek danych jest tworzone co godzinę.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-217">In hello preceding example, there are 24 data slices as each data slice is produced hourly.</span></span>

<span data-ttu-id="7d5d9-218">Opisy właściwości JSON w definicji potoku znajdują się w artykule dotyczącym [tworzenia potoków](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="7d5d9-218">For descriptions of JSON properties in a pipeline definition, see [create pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="7d5d9-219">Opisy właściwości JSON w definicji działania kopiowania znajdują się w artykule dotyczącym [działań związanych z przenoszeniem danych](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="7d5d9-219">For descriptions of JSON properties in a copy activity definition, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="7d5d9-220">Opisy właściwości JSON obsługiwanych przez BlobSource można znaleźć w [artykule dotyczącym łącznika usługi Azure Blob](data-factory-azure-blob-connector.md).</span><span class="sxs-lookup"><span data-stu-id="7d5d9-220">For descriptions of JSON properties supported by BlobSource, see [Azure Blob connector article](data-factory-azure-blob-connector.md).</span></span> <span data-ttu-id="7d5d9-221">Opisy właściwości JSON obsługiwanych przez SqlSink można znaleźć w artykule [dotyczącym łącznika usługi Azure SQL Database](data-factory-azure-sql-connector.md).</span><span class="sxs-lookup"><span data-stu-id="7d5d9-221">For descriptions of JSON properties supported by SqlSink, see [Azure SQL Database connector article](data-factory-azure-sql-connector.md).</span></span>

## <a name="set-global-variables"></a><span data-ttu-id="7d5d9-222">Ustawianie zmiennych globalnych</span><span class="sxs-lookup"><span data-stu-id="7d5d9-222">Set global variables</span></span>
<span data-ttu-id="7d5d9-223">W programie Azure PowerShell wykonaj następujące polecenia, po zastąpieniu hello wartości własnymi hello:</span><span class="sxs-lookup"><span data-stu-id="7d5d9-223">In Azure PowerShell, execute hello following commands after replacing hello values with your own:</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7d5d9-224">Zobacz sekcję [Wymagania wstępne](#prerequisites), aby uzyskać instrukcje dotyczące pobierania identyfikatora klienta, klucza tajnego klienta, identyfikatora dzierżawy oraz identyfikatora subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-224">See [Prerequisites](#prerequisites) section for instructions on getting client ID, client secret, tenant ID, and subscription ID.</span></span>   
> 
> 

```JSON
$client_id = "<client ID of application in AAD>"
$client_secret = "<client key of application in AAD>"
$tenant = "<Azure tenant ID>";
$subscription_id="<Azure subscription ID>";

$rg = "ADFTutorialResourceGroup"
```

<span data-ttu-id="7d5d9-225">Uruchom następujące polecenia, po zaktualizowaniu hello nazwa fabryki danych hello, którego używasz hello:</span><span class="sxs-lookup"><span data-stu-id="7d5d9-225">Run hello following command after updating hello name of hello data factory you are using:</span></span> 

```
$adf = "ADFCopyTutorialDF"
```

## <a name="authenticate-with-aad"></a><span data-ttu-id="7d5d9-226">Uwierzytelnianie przy użyciu usługi AAD</span><span class="sxs-lookup"><span data-stu-id="7d5d9-226">Authenticate with AAD</span></span>
<span data-ttu-id="7d5d9-227">Witaj uruchom następujące polecenie tooauthenticate usłudze Azure Active Directory (AAD):</span><span class="sxs-lookup"><span data-stu-id="7d5d9-227">Run hello following command tooauthenticate with Azure Active Directory (AAD):</span></span> 

```PowerShell
$cmd = { .\curl.exe -X POST https://login.microsoftonline.com/$tenant/oauth2/token  -F grant_type=client_credentials  -F resource=https://management.core.windows.net/ -F client_id=$client_id -F client_secret=$client_secret };
$responseToken = Invoke-Command -scriptblock $cmd;
$accessToken = (ConvertFrom-Json $responseToken).access_token;

(ConvertFrom-Json $responseToken) 
```

## <a name="create-data-factory"></a><span data-ttu-id="7d5d9-228">Tworzenie fabryki danych</span><span class="sxs-lookup"><span data-stu-id="7d5d9-228">Create data factory</span></span>
<span data-ttu-id="7d5d9-229">W tym kroku opisano tworzenie fabryki danych Azure o nazwie **ADFCopyTutorialDF**.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-229">In this step, you create an Azure Data Factory named **ADFCopyTutorialDF**.</span></span> <span data-ttu-id="7d5d9-230">Fabryka danych może obejmować jeden lub wiele potoków.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-230">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="7d5d9-231">Potok może obejmować jedno lub wiele działań.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-231">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="7d5d9-232">Na przykład działanie kopiowania toocopy magazynu danych, z docelowym tooa źródła danych.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-232">For example, a Copy Activity toocopy data from a source tooa destination data store.</span></span> <span data-ttu-id="7d5d9-233">HDInsight Hive działania toorun tootransform skryptu Hive wejściowe dane wyjściowe tooproduct danych.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-233">A HDInsight Hive activity toorun a Hive script tootransform input data tooproduct output data.</span></span> <span data-ttu-id="7d5d9-234">Uruchom powitania po fabryki danych hello toocreate polecenia:</span><span class="sxs-lookup"><span data-stu-id="7d5d9-234">Run hello following commands toocreate hello data factory:</span></span> 

1. <span data-ttu-id="7d5d9-235">Przypisz hello toovariable polecenia o nazwie **cmd**.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-235">Assign hello command toovariable named **cmd**.</span></span> 
   
    > [!IMPORTANT]
    > <span data-ttu-id="7d5d9-236">Potwierdzić tę nazwę hello hello fabryki danych określone w tym miejscu (ADFCopyTutorialDF) dopasowań hello nazwa określona w hello **datafactory.json**.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-236">Confirm that hello name of hello data factory you specify here (ADFCopyTutorialDF) matches hello name specified in hello **datafactory.json**.</span></span> 
   
    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data “@datafactory.json” https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/ADFCopyTutorialDF0411?api-version=2015-10-01};
    ```
2. <span data-ttu-id="7d5d9-237">Uruchom polecenie hello przy użyciu **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-237">Run hello command by using **Invoke-Command**.</span></span>
   
    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="7d5d9-238">Wyświetl wyniki hello.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-238">View hello results.</span></span> <span data-ttu-id="7d5d9-239">Po pomyślnym utworzeniu hello fabryki danych Zobacz hello JSON dla fabryki danych hello w hello **wyniki**; w przeciwnym razie zostanie wyświetlony komunikat o błędzie.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-239">If hello data factory has been successfully created, you see hello JSON for hello data factory in hello **results**; otherwise, you see an error message.</span></span>  
   
    ```
    Write-Host $results
    ```

<span data-ttu-id="7d5d9-240">Należy zwrócić uwagę hello następujące punkty:</span><span class="sxs-lookup"><span data-stu-id="7d5d9-240">Note hello following points:</span></span>

* <span data-ttu-id="7d5d9-241">Nazwa Hello hello fabryki danych Azure musi być globalnie unikatowe.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-241">hello name of hello Azure Data Factory must be globally unique.</span></span> <span data-ttu-id="7d5d9-242">Jeśli zostanie wyświetlony błąd hello w wynikach: **nazwa fabryki danych "ADFCopyTutorialDF" nie jest dostępna**, hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="7d5d9-242">If you see hello error in results: **Data factory name “ADFCopyTutorialDF” is not available**, do hello following steps:</span></span>  
  
  1. <span data-ttu-id="7d5d9-243">Zmień nazwę hello (na przykład yournameADFCopyTutorialDF) w hello **datafactory.json** pliku.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-243">Change hello name (for example, yournameADFCopyTutorialDF) in hello **datafactory.json** file.</span></span>
  2. <span data-ttu-id="7d5d9-244">W pierwszym poleceniem hello gdzie hello **$cmd** zmiennej jest przypisywana wartość, Zamień ADFCopyTutorialDF hello nowej nazwy i uruchom polecenie hello.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-244">In hello first command where hello **$cmd** variable is assigned a value, replace ADFCopyTutorialDF with hello new name and run hello command.</span></span> 
  3. <span data-ttu-id="7d5d9-245">Uruchamianie hello następne dwa polecenia tooinvoke hello interfejsu API REST toocreate hello danych fabryki i Drukuj hello wyników hello operacji.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-245">Run hello next two commands tooinvoke hello REST API toocreate hello data factory and print hello results of hello operation.</span></span> 
     
     <span data-ttu-id="7d5d9-246">Artykuł [Data Factory — Naming Rules](data-factory-naming-rules.md) (Fabryka danych — zasady nazewnictwa) zawiera zasady nazewnictwa artefaktów usługi Fabryka danych.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-246">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>
* <span data-ttu-id="7d5d9-247">toocreate wystąpienia fabryki danych, należy toobe współautora/administrator hello subskrypcji platformy Azure</span><span class="sxs-lookup"><span data-stu-id="7d5d9-247">toocreate Data Factory instances, you need toobe a contributor/administrator of hello Azure subscription</span></span>
* <span data-ttu-id="7d5d9-248">Nazwa fabryki danych hello Hello mogą być zarejestrowana jako nazwa DNS w przyszłości hello i dlatego stać się publicznie widoczna.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-248">hello name of hello data factory may be registered as a DNS name in hello future and hence become publicly visible.</span></span>
* <span data-ttu-id="7d5d9-249">Jeśli wystąpi błąd hello: "**Ta subskrypcja nie jest zarejestrowany toouse przestrzeni nazw Microsoft.DataFactory**", wykonaj jedną z następujących hello i spróbuj ponownie opublikować:</span><span class="sxs-lookup"><span data-stu-id="7d5d9-249">If you receive hello error: "**This subscription is not registered toouse namespace Microsoft.DataFactory**", do one of hello following and try publishing again:</span></span> 
  
  * <span data-ttu-id="7d5d9-250">W programie Azure PowerShell Uruchom hello następujące polecenia tooregister hello fabryki danych dostawcy:</span><span class="sxs-lookup"><span data-stu-id="7d5d9-250">In Azure PowerShell, run hello following command tooregister hello Data Factory provider:</span></span> 

    ```PowerShell    
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```
    <span data-ttu-id="7d5d9-251">Powitania po tooconfirm polecenie można uruchomić tego hello fabryki danych dostawca został zarejestrowany.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-251">You can run hello following command tooconfirm that hello Data Factory provider is registered.</span></span> 
    
    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * <span data-ttu-id="7d5d9-252">Logowanie przy użyciu hello subskrypcji platformy Azure do hello [portalu Azure](https://portal.azure.com) i przejdź do bloku usługi fabryka danych tooa tworzenie fabryki danych w hello portalu Azure (lub).</span><span class="sxs-lookup"><span data-stu-id="7d5d9-252">Login using hello Azure subscription into hello [Azure portal](https://portal.azure.com) and navigate tooa Data Factory blade (or) create a data factory in hello Azure portal.</span></span> <span data-ttu-id="7d5d9-253">Ta akcja rejestruje automatycznie hello dostawcy dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-253">This action automatically registers hello provider for you.</span></span>

<span data-ttu-id="7d5d9-254">Przed utworzeniem potoku, należy toocreate kilku jednostek fabryki danych najpierw.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-254">Before creating a pipeline, you need toocreate a few Data Factory entities first.</span></span> <span data-ttu-id="7d5d9-255">Najpierw Utwórz źródło toolink połączonych usług i miejsce docelowe danych przechowuje dane tooyour przechowywania.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-255">You first create linked services toolink source and destination data stores tooyour data store.</span></span> <span data-ttu-id="7d5d9-256">Następnie należy zdefiniować dane toorepresent wejściowych i wyjściowych zestawów danych w magazynach połączonych danych.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-256">Then, define input and output datasets toorepresent data in linked data stores.</span></span> <span data-ttu-id="7d5d9-257">Na koniec należy utworzyć potok hello do działania, która używa tych zestawów danych.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-257">Finally, create hello pipeline with an activity that uses these datasets.</span></span>

## <a name="create-linked-services"></a><span data-ttu-id="7d5d9-258">Tworzenie połączonych usług</span><span class="sxs-lookup"><span data-stu-id="7d5d9-258">Create linked services</span></span>
<span data-ttu-id="7d5d9-259">Połączone usługi są tworzone w toolink fabryki danych dane są przechowywane i obliczeniowe fabryki danych toohello usług.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-259">You create linked services in a data factory toolink your data stores and compute services toohello data factory.</span></span> <span data-ttu-id="7d5d9-260">W tym samouczku nie przedstawiono korzystania z żadnych usług obliczeniowych, takich jak Azure HDInsight czy Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-260">In this tutorial, you don't use any compute service such as Azure HDInsight or Azure Data Lake Analytics.</span></span> <span data-ttu-id="7d5d9-261">Zostają użyte dwa magazyny danych typu Azure Storage (źródło) i Azure SQL Database (lokalizacja docelowa).</span><span class="sxs-lookup"><span data-stu-id="7d5d9-261">You use two data stores of type Azure Storage (source) and Azure SQL Database (destination).</span></span> <span data-ttu-id="7d5d9-262">W związku z tym tworzy się dwie połączone usługi o nazwie AzureStorageLinkedService i AzureSqlLinkedService typu: AzureStorage i AzureSqlDatabase.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-262">Therefore, you create two linked services named AzureStorageLinkedService and AzureSqlLinkedService of types: AzureStorage and AzureSqlDatabase.</span></span>  

<span data-ttu-id="7d5d9-263">Witaj AzureStorageLinkedService łączy fabrykę danych toohello konta magazynu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-263">hello AzureStorageLinkedService links your Azure storage account toohello data factory.</span></span> <span data-ttu-id="7d5d9-264">To konto magazynu jest hello jedną w którym utworzono kontener i hello dane przekazane jako część [wymagania wstępne](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="7d5d9-264">This storage account is hello one in which you created a container and uploaded hello data as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>   

<span data-ttu-id="7d5d9-265">AzureSqlLinkedService łączy fabrykę danych toohello bazy danych Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-265">AzureSqlLinkedService links your Azure SQL database toohello data factory.</span></span> <span data-ttu-id="7d5d9-266">dane Hello, który jest skopiowany z magazynu obiektów blob hello są przechowywane w tej bazie danych.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-266">hello data that is copied from hello blob storage is stored in this database.</span></span> <span data-ttu-id="7d5d9-267">Utworzono hello pustych elementów tabeli w tej bazie danych jako część [wymagania wstępne](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="7d5d9-267">You created hello emp table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>  

### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="7d5d9-268">Tworzenie połączonej usługi Azure Storage</span><span class="sxs-lookup"><span data-stu-id="7d5d9-268">Create Azure Storage linked service</span></span>
<span data-ttu-id="7d5d9-269">W tym kroku możesz połączyć fabrykę danych tooyour konta magazynu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-269">In this step, you link your Azure storage account tooyour data factory.</span></span> <span data-ttu-id="7d5d9-270">W tej sekcji można określić nazwę hello i klucza konta magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-270">You specify hello name and key of your Azure storage account in this section.</span></span> <span data-ttu-id="7d5d9-271">Zobacz [połączonej usługi magazynu Azure](data-factory-azure-blob-connector.md#azure-storage-linked-service) szczegółowe informacje o toodefine właściwości używane w formacie JSON połączonej usługi magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-271">See [Azure Storage linked service](data-factory-azure-blob-connector.md#azure-storage-linked-service) for details about JSON properties used toodefine an Azure Storage linked service.</span></span>  

1. <span data-ttu-id="7d5d9-272">Przypisz hello toovariable polecenia o nazwie **cmd**.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-272">Assign hello command toovariable named **cmd**.</span></span> 

    ```PowerShell   
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@azurestoragelinkedservice.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/linkedservices/AzureStorageLinkedService?api-version=2015-10-01};
    ```
2. <span data-ttu-id="7d5d9-273">Uruchom polecenie hello przy użyciu **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-273">Run hello command by using **Invoke-Command**.</span></span>

    ```PowerShell   
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="7d5d9-274">Wyświetl wyniki hello.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-274">View hello results.</span></span> <span data-ttu-id="7d5d9-275">Jeśli hello połączone usługi został utworzony pomyślnie, zobacz hello JSON usługi hello połączone w hello **wyniki**; w przeciwnym razie zostanie wyświetlony komunikat o błędzie.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-275">If hello linked service has been successfully created, you see hello JSON for hello linked service in hello **results**; otherwise, you see an error message.</span></span>

    ```PowerShell   
    Write-Host $results
    ```

### <a name="create-azure-sql-linked-service"></a><span data-ttu-id="7d5d9-276">Tworzenie połączonej usługi SQL Azure</span><span class="sxs-lookup"><span data-stu-id="7d5d9-276">Create Azure SQL linked service</span></span>
<span data-ttu-id="7d5d9-277">W tym kroku możesz połączyć fabrykę danych tooyour bazy danych Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-277">In this step, you link your Azure SQL database tooyour data factory.</span></span> <span data-ttu-id="7d5d9-278">W tej sekcji można określić nazwy serwera Azure SQL hello, nazwa bazy danych, nazwę użytkownika i hasło użytkownika.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-278">You specify hello Azure SQL server name, database name, user name, and user password in this section.</span></span> <span data-ttu-id="7d5d9-279">Zobacz [Azure SQL połączona usługa](data-factory-azure-sql-connector.md#linked-service-properties) szczegółowe informacje o toodefine właściwości używane w formacie JSON Azure SQL połączonej usługi.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-279">See [Azure SQL linked service](data-factory-azure-sql-connector.md#linked-service-properties) for details about JSON properties used toodefine an Azure SQL linked service.</span></span>

1. <span data-ttu-id="7d5d9-280">Przypisz hello toovariable polecenia o nazwie **cmd**.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-280">Assign hello command toovariable named **cmd**.</span></span> 
   
    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data “@azuresqllinkedservice.json” https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/linkedservices/AzureSqlLinkedService?api-version=2015-10-01};
    ```
2. <span data-ttu-id="7d5d9-281">Uruchom polecenie hello przy użyciu **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-281">Run hello command by using **Invoke-Command**.</span></span>
   
    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="7d5d9-282">Wyświetl wyniki hello.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-282">View hello results.</span></span> <span data-ttu-id="7d5d9-283">Jeśli hello połączone usługi został utworzony pomyślnie, zobacz hello JSON usługi hello połączone w hello **wyniki**; w przeciwnym razie zostanie wyświetlony komunikat o błędzie.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-283">If hello linked service has been successfully created, you see hello JSON for hello linked service in hello **results**; otherwise, you see an error message.</span></span>
   
    ```PowerShell
    Write-Host $results
    ```

## <a name="create-datasets"></a><span data-ttu-id="7d5d9-284">Tworzenie zestawów danych</span><span class="sxs-lookup"><span data-stu-id="7d5d9-284">Create datasets</span></span>
<span data-ttu-id="7d5d9-285">W poprzednim kroku hello utworzono toolink połączone usługi konta magazynu Azure i fabryki danych tooyour bazy danych Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-285">In hello previous step, you created linked services toolink your Azure Storage account and Azure SQL database tooyour data factory.</span></span> <span data-ttu-id="7d5d9-286">W tym kroku należy zdefiniować dwa zestawy danych o nazwie AzureBlobInput i AzureSqlOutput reprezentujące danych wejściowych i wyjściowych danych przechowywanych w magazynach danych hello odwołuje się AzureStorageLinkedService i AzureSqlLinkedService odpowiednio.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-286">In this step, you define two datasets named AzureBlobInput and AzureSqlOutput that represent input and output data that is stored in hello data stores referred by AzureStorageLinkedService and AzureSqlLinkedService respectively.</span></span>

<span data-ttu-id="7d5d9-287">Hello Azure połączoną usługą magazynu określa parametry połączenia hello, która używa usługi fabryka danych w czasie wykonywania tooconnect tooyour kontem magazynu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-287">hello Azure storage linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="7d5d9-288">I zestawu danych wejściowych obiektu blob hello (AzureBlobInput) określa hello kontenera i folderu hello, który zawiera hello danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-288">And, hello input blob dataset (AzureBlobInput) specifies hello container and hello folder that contains hello input data.</span></span>  

<span data-ttu-id="7d5d9-289">Podobnie hello usługi baza danych SQL Azure połączone określa hello parametry połączenia, które korzysta z usługi fabryka danych w czasie wykonywania tooconnect tooyour — bazy danych Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-289">Similarly, hello Azure SQL Database linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure SQL database.</span></span> <span data-ttu-id="7d5d9-290">I hello danych wyjściowych SQL tabeli dataset (OututDataset) określa hello tabeli w hello bazy danych toowhich powitalne dane z magazynu obiektów blob hello są kopiowane.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-290">And, hello output SQL table dataset (OututDataset) specifies hello table in hello database toowhich hello data from hello blob storage is copied.</span></span> 

### <a name="create-input-dataset"></a><span data-ttu-id="7d5d9-291">Tworzenie wejściowego zestawu danych</span><span class="sxs-lookup"><span data-stu-id="7d5d9-291">Create input dataset</span></span>
<span data-ttu-id="7d5d9-292">W tym kroku utworzysz zestaw danych o nazwie AzureBlobInput, który wskazuje plik obiektu blob tooa (emp.txt) w folderze głównym hello kontenera obiektów blob (adftutorial) w hello reprezentowany przez hello AzureStorageLinkedService połączone usługi Magazyn Azure.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-292">In this step, you create a dataset named AzureBlobInput that points tooa blob file (emp.txt) in hello root folder of a blob container (adftutorial) in hello Azure Storage represented by hello AzureStorageLinkedService linked service.</span></span> <span data-ttu-id="7d5d9-293">Brak określić wartość dla nazwy pliku hello (lub Pomiń je), danych z wszystkich obiektów blob w folderze wejściowych hello są skopiowanych toohello docelowego.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-293">If you don't specify a value for hello fileName (or skip it), data from all blobs in hello input folder are copied toohello destination.</span></span> <span data-ttu-id="7d5d9-294">W tym samouczku należy określić wartość dla hello fileName.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-294">In this tutorial, you specify a value for hello fileName.</span></span> 

1. <span data-ttu-id="7d5d9-295">Przypisz hello toovariable polecenia o nazwie **cmd**.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-295">Assign hello command toovariable named **cmd**.</span></span> 

    ```PowerSHell   
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@inputdataset.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/AzureBlobInput?api-version=2015-10-01};
    ```
2. <span data-ttu-id="7d5d9-296">Uruchom polecenie hello przy użyciu **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-296">Run hello command by using **Invoke-Command**.</span></span>
   
    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="7d5d9-297">Wyświetl wyniki hello.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-297">View hello results.</span></span> <span data-ttu-id="7d5d9-298">Po pomyślnym utworzeniu zestawu danych hello Zobacz hello JSON dla zestawu danych hello w hello **wyniki**; w przeciwnym razie zostanie wyświetlony komunikat o błędzie.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-298">If hello dataset has been successfully created, you see hello JSON for hello dataset in hello **results**; otherwise, you see an error message.</span></span>
   
    ```PowerShell
    Write-Host $results
    ```

### <a name="create-output-dataset"></a><span data-ttu-id="7d5d9-299">Tworzenie wyjściowego zestawu danych</span><span class="sxs-lookup"><span data-stu-id="7d5d9-299">Create output dataset</span></span>
<span data-ttu-id="7d5d9-300">Hello usługi baza danych SQL Azure połączone określa hello parametry połączenia, które korzysta z usługi fabryka danych w czasie wykonywania tooconnect tooyour — bazy danych Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-300">hello Azure SQL Database linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure SQL database.</span></span> <span data-ttu-id="7d5d9-301">Utwórz w tym kroku Hello danych wyjściowych SQL tabeli dataset (OututDataset) określa, że tabela hello hello bazy danych toowhich hello danych z magazynu obiektów blob hello jest kopiowany.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-301">hello output SQL table dataset (OututDataset) you create in this step specifies hello table in hello database toowhich hello data from hello blob storage is copied.</span></span>

1. <span data-ttu-id="7d5d9-302">Przypisz hello toovariable polecenia o nazwie **cmd**.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-302">Assign hello command toovariable named **cmd**.</span></span>

    ```PowerShell   
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@outputdataset.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/AzureSqlOutput?api-version=2015-10-01};
    ```
2. <span data-ttu-id="7d5d9-303">Uruchom polecenie hello przy użyciu **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-303">Run hello command by using **Invoke-Command**.</span></span>
    
    ```PowerShell   
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="7d5d9-304">Wyświetl wyniki hello.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-304">View hello results.</span></span> <span data-ttu-id="7d5d9-305">Po pomyślnym utworzeniu zestawu danych hello Zobacz hello JSON dla zestawu danych hello w hello **wyniki**; w przeciwnym razie zostanie wyświetlony komunikat o błędzie.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-305">If hello dataset has been successfully created, you see hello JSON for hello dataset in hello **results**; otherwise, you see an error message.</span></span>
   
    ```PowerShell
    Write-Host $results
    ``` 

## <a name="create-pipeline"></a><span data-ttu-id="7d5d9-306">Tworzenie potoku</span><span class="sxs-lookup"><span data-stu-id="7d5d9-306">Create pipeline</span></span>
<span data-ttu-id="7d5d9-307">W tym kroku za pomocą **działania kopiowania** zostanie utworzony potok, w którym parametr **AzureBlobInput** jest używany jako dane wejściowe, a parametr **AzureSqlOutput** jako dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-307">In this step, you create a pipeline with a **copy activity** that uses **AzureBlobInput** as an input and **AzureSqlOutput** as an output.</span></span>

<span data-ttu-id="7d5d9-308">Wyjściowy zestaw danych jest obecnie, jakie dysków hello harmonogramu.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-308">Currently, output dataset is what drives hello schedule.</span></span> <span data-ttu-id="7d5d9-309">W tym samouczku wyjściowy zestaw danych jest skonfigurowane tooproduce wycinek godzinę.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-309">In this tutorial, output dataset is configured tooproduce a slice once an hour.</span></span> <span data-ttu-id="7d5d9-310">potok Hello ma czas rozpoczęcia i godzina zakończenia, będące w ciągu jednego dnia od siebie, który wynosi 24 godziny.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-310">hello pipeline has a start time and end time that are one day apart, which is 24 hours.</span></span> <span data-ttu-id="7d5d9-311">W związku z tym 24 wycinków wyjściowy zestaw danych są produkowane przez hello potoku.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-311">Therefore, 24 slices of output dataset are produced by hello pipeline.</span></span> 

1. <span data-ttu-id="7d5d9-312">Przypisz hello toovariable polecenia o nazwie **cmd**.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-312">Assign hello command toovariable named **cmd**.</span></span>

    ```PowerShell   
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@pipeline.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datapipelines/MyFirstPipeline?api-version=2015-10-01};
    ```
2. <span data-ttu-id="7d5d9-313">Uruchom polecenie hello przy użyciu **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-313">Run hello command by using **Invoke-Command**.</span></span>

    ```PowerShell   
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="7d5d9-314">Wyświetl wyniki hello.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-314">View hello results.</span></span> <span data-ttu-id="7d5d9-315">Po pomyślnym utworzeniu zestawu danych hello Zobacz hello JSON dla zestawu danych hello w hello **wyniki**; w przeciwnym razie zostanie wyświetlony komunikat o błędzie.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-315">If hello dataset has been successfully created, you see hello JSON for hello dataset in hello **results**; otherwise, you see an error message.</span></span>  

    ```PowerShell   
    Write-Host $results
    ```

<span data-ttu-id="7d5d9-316">**Gratulacje!**</span><span class="sxs-lookup"><span data-stu-id="7d5d9-316">**Congratulations!**</span></span> <span data-ttu-id="7d5d9-317">Pomyślnie utworzono fabryki danych Azure z potok, który kopiuje dane z bazy danych SQL tooAzure magazynu obiektów Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-317">You have successfully created an Azure data factory, with a pipeline that copies data from Azure Blob Storage tooAzure SQL database.</span></span>

## <a name="monitor-pipeline"></a><span data-ttu-id="7d5d9-318">Monitorowanie potoku</span><span class="sxs-lookup"><span data-stu-id="7d5d9-318">Monitor pipeline</span></span>
<span data-ttu-id="7d5d9-319">W tym kroku użyjesz tworzonym przez potok hello wycinków toomonitor interfejsu API REST fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-319">In this step, you use Data Factory REST API toomonitor slices being produced by hello pipeline.</span></span>

```PowerShell
$ds ="AzureSqlOutput"
```

> [!IMPORTANT] 
> <span data-ttu-id="7d5d9-320">Upewnij się, hello początkową i końcową czas określony w powitania po polecenie start hello dopasowania i kończyć razy hello potoku.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-320">Make sure that hello start and end times specified in hello following command match hello start and end times of hello pipeline.</span></span> 

```PowerShell
$cmd = {.\curl.exe -X GET -H "Authorization: Bearer $accessToken" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/$ds/slices?start=2017-05-11T00%3a00%3a00.0000000Z"&"end=2017-05-12T00%3a00%3a00.0000000Z"&"api-version=2015-10-01};
```

```PowerShell
$results2 = Invoke-Command -scriptblock $cmd;
```

```PowerShell
IF ((ConvertFrom-Json $results2).value -ne $NULL) {
    ConvertFrom-Json $results2 | Select-Object -Expand value | Format-Table
} else {
        (convertFrom-Json $results2).RemoteException
}
```

<span data-ttu-id="7d5d9-321">Uruchom hello Invoke-Command i hello kolejnego do momentu wyświetlenia wycinek **gotowe** stanu lub **** stanu.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-321">Run hello Invoke-Command and hello next one until you see a slice in **Ready** state or **Failed** state.</span></span> <span data-ttu-id="7d5d9-322">Gdy wycinek hello jest w stanie gotowe, sprawdź hello **pustych elementów** tabeli w bazie danych Azure SQL hello danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-322">When hello slice is in Ready state, check hello **emp** table in your Azure SQL database for hello output data.</span></span> 

<span data-ttu-id="7d5d9-323">Każdy wycinek dwa wiersze danych z pliku źródłowego hello są kopiowane toohello pustych elementów tabeli w bazie danych Azure SQL hello.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-323">For each slice, two rows of data from hello source file are copied toohello emp table in hello Azure SQL database.</span></span> <span data-ttu-id="7d5d9-324">W związku z tym 24 nowych rekordów w tabeli pustych elementów hello wyświetlona w sytuacji, gdy wszystkie fragmenty hello są pomyślnie przetworzone (w stanie innym niż Ready).</span><span class="sxs-lookup"><span data-stu-id="7d5d9-324">Therefore, you see 24 new records in hello emp table when all hello slices are successfully processed (in Ready state).</span></span> 

## <a name="summary"></a><span data-ttu-id="7d5d9-325">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="7d5d9-325">Summary</span></span>
<span data-ttu-id="7d5d9-326">W tym samouczku użyto toocreate interfejsu API REST usługi Azure data factory toocopy dane z bazy danych Azure SQL tooan obiektów blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-326">In this tutorial, you used REST API toocreate an Azure data factory toocopy data from an Azure blob tooan Azure SQL database.</span></span> <span data-ttu-id="7d5d9-327">Poniżej przedstawiono ogólne kroki hello, wykonane w tym samouczku:</span><span class="sxs-lookup"><span data-stu-id="7d5d9-327">Here are hello high-level steps you performed in this tutorial:</span></span>  

1. <span data-ttu-id="7d5d9-328">Tworzenie **fabryki danych** Azure.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-328">Created an Azure **data factory**.</span></span>
2. <span data-ttu-id="7d5d9-329">Tworzenie **połączonych usług**:</span><span class="sxs-lookup"><span data-stu-id="7d5d9-329">Created **linked services**:</span></span>
   1. <span data-ttu-id="7d5d9-330">Magazyn Azure połączone usługi toolink konta magazynu Azure, która przechowuje dane wejściowe.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-330">An Azure Storage linked service toolink your Azure Storage account that holds input data.</span></span>     
   2. <span data-ttu-id="7d5d9-331">Azure SQL połączone usługi toolink przechowujący dane wyjściowe hello bazy danych Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-331">An Azure SQL linked service toolink your Azure SQL database that holds hello output data.</span></span> 
3. <span data-ttu-id="7d5d9-332">Tworzenie **zestawów danych** opisujących dane wejściowe i wyjściowe dla potoków.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-332">Created **datasets**, which describe input data and output data for pipelines.</span></span>
4. <span data-ttu-id="7d5d9-333">Tworzenie **potoku** za pomocą działania kopiowania, w którym źródłem jest element BlobSource, a ujściem element SqlSink.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-333">Created a **pipeline** with a Copy Activity with BlobSource as source and SqlSink as sink.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="7d5d9-334">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="7d5d9-334">Next steps</span></span>
<span data-ttu-id="7d5d9-335">W tym samouczku użyto magazynu obiektów blob platformy Azure jako magazynu danych źródła oraz bazy danych SQL na platformie Azure jako magazynu danych docelowych w operacji kopiowania.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-335">In this tutorial, you used Azure blob storage as a source data store and an Azure SQL database as a destination data store in a copy operation.</span></span> <span data-ttu-id="7d5d9-336">Witaj Poniższa tabela zawiera listę magazynów danych obsługiwane jako źródeł i miejsc docelowych przez działanie kopiowania hello:</span><span class="sxs-lookup"><span data-stu-id="7d5d9-336">hello following table provides a list of data stores supported as sources and destinations by hello copy activity:</span></span> 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

<span data-ttu-id="7d5d9-337">toolearn o jak magazyn danych toocopy z danych, kliknij łącze hello hello magazynu danych w tabeli hello.</span><span class="sxs-lookup"><span data-stu-id="7d5d9-337">toolearn about how toocopy data to/from a data store, click hello link for hello data store in hello table.</span></span>
