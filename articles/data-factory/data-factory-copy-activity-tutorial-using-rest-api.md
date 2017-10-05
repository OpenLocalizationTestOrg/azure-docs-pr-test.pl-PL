---
title: "Samouczek: korzystanie z interfejsu API REST w celu utworzenia potoku usługi Azure Data Factory | Microsoft Docs"
description: "W tym samouczku opisano korzystanie z interfejsu API REST w celu utworzenia potoku usługi Azure Data Factory z działaniem kopiowania, aby skopiować dane z magazynu obiektów blob Azure do bazy danych Azure SQL."
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
ms.openlocfilehash: 6663774497aa18aa98e7e8c5aed6183c599b2172
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="tutorial-use-rest-api-to-create-an-azure-data-factory-pipeline-to-copy-data"></a><span data-ttu-id="4f56b-103">Samouczek: korzystanie z interfejsu API REST w celu utworzenia potoku usługi Azure Data Factory do kopiowania danych</span><span class="sxs-lookup"><span data-stu-id="4f56b-103">Tutorial: Use REST API to create an Azure Data Factory pipeline to copy data</span></span> 
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4f56b-104">Przegląd i wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="4f56b-104">Overview and prerequisites</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [<span data-ttu-id="4f56b-105">Kreator kopiowania</span><span class="sxs-lookup"><span data-stu-id="4f56b-105">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
> * [<span data-ttu-id="4f56b-106">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="4f56b-106">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [<span data-ttu-id="4f56b-107">Program Visual Studio</span><span class="sxs-lookup"><span data-stu-id="4f56b-107">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [<span data-ttu-id="4f56b-108">Program PowerShell</span><span class="sxs-lookup"><span data-stu-id="4f56b-108">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
> * [<span data-ttu-id="4f56b-109">Szablon usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="4f56b-109">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [<span data-ttu-id="4f56b-110">Interfejs API REST</span><span class="sxs-lookup"><span data-stu-id="4f56b-110">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [<span data-ttu-id="4f56b-111">Interfejs API .NET</span><span class="sxs-lookup"><span data-stu-id="4f56b-111">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)
> 
> 

<span data-ttu-id="4f56b-112">W tym artykule wyjaśniono, jak używać interfejsu API REST do tworzenia fabryki danych obejmującej potok, który kopiuje dane z usługi Azure Blob Storage do bazy danych Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="4f56b-112">In this article, you learn how to use REST API to create a data factory with a pipeline that copies data from an Azure blob storage to an Azure SQL database.</span></span> <span data-ttu-id="4f56b-113">Jeśli jesteś nowym użytkownikiem usługi Azure Data Factory, przed wykonaniem instrukcji z tego samouczka zapoznaj się z artykułem [Wprowadzenie do usługi Azure Data Factory](data-factory-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="4f56b-113">If you are new to Azure Data Factory, read through the [Introduction to Azure Data Factory](data-factory-introduction.md) article before doing this tutorial.</span></span>   

<span data-ttu-id="4f56b-114">W tym samouczku opisano tworzenie potoku z jednym działaniem (Działanie kopiowania).</span><span class="sxs-lookup"><span data-stu-id="4f56b-114">In this tutorial, you create a pipeline with one activity in it: Copy Activity.</span></span> <span data-ttu-id="4f56b-115">Działanie kopiowania kopiuje dane z obsługiwanego magazynu danych do obsługiwanego magazynu danych ujścia.</span><span class="sxs-lookup"><span data-stu-id="4f56b-115">The copy activity copies data from a supported data store to a supported sink data store.</span></span> <span data-ttu-id="4f56b-116">Aby zapoznać się z listą magazynów danych obsługiwanych jako źródła i ujścia, zobacz [obsługiwane magazyny danych](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="4f56b-116">For a list of data stores supported as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="4f56b-117">Działanie jest obsługiwane przez globalnie dostępną usługę, która może kopiować dane między różnymi magazynami danych w sposób bezpieczny, niezawodny i skalowalny.</span><span class="sxs-lookup"><span data-stu-id="4f56b-117">The activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="4f56b-118">Więcej informacji o działaniu kopiowania znajduje się w artykule dotyczącym [działań związanych z przenoszeniem danych](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="4f56b-118">For more information about the Copy Activity, see [Data Movement Activities](data-factory-data-movement-activities.md).</span></span>

<span data-ttu-id="4f56b-119">Potok może obejmować więcej niż jedno działanie.</span><span class="sxs-lookup"><span data-stu-id="4f56b-119">A pipeline can have more than one activity.</span></span> <span data-ttu-id="4f56b-120">Dwa działania można połączyć w łańcuch (uruchomić jedno działanie po drugim), ustawiając wyjściowy zestaw danych jednego działania jako zestaw wejściowy drugiego.</span><span class="sxs-lookup"><span data-stu-id="4f56b-120">And, you can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity.</span></span> <span data-ttu-id="4f56b-121">Aby uzyskać więcej informacji, zobacz sekcję dotyczącą [wielu działań w potoku](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span><span class="sxs-lookup"><span data-stu-id="4f56b-121">For more information, see [multiple activities in a pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span>

> [!NOTE]
> <span data-ttu-id="4f56b-122">Ten artykuł nie obejmuje całego interfejsu API REST usługi Data Factory.</span><span class="sxs-lookup"><span data-stu-id="4f56b-122">This article does not cover all the Data Factory REST API.</span></span> <span data-ttu-id="4f56b-123">Pełna dokumentacja dotycząca poleceń cmdlet usługi Data Factory znajduje się w artykule [Data Factory Cmdlet Reference](/rest/api/datafactory/) (Dokumentacja dotycząca interfejsu API REST usługi Data Factory).</span><span class="sxs-lookup"><span data-stu-id="4f56b-123">See [Data Factory REST API Reference](/rest/api/datafactory/) for comprehensive documentation on Data Factory cmdlets.</span></span>
>  
> <span data-ttu-id="4f56b-124">Potok danych przedstawiony w tym samouczku kopiuje dane ze źródłowego do docelowego magazynu danych.</span><span class="sxs-lookup"><span data-stu-id="4f56b-124">The data pipeline in this tutorial copies data from a source data store to a destination data store.</span></span> <span data-ttu-id="4f56b-125">Aby zapoznać się z samouczkiem dotyczącym przekształcania danych za pomocą usługi Azure Data Factory, zobacz [Tutorial: Build a pipeline to transform data using Hadoop cluster](data-factory-build-your-first-pipeline.md) (Samouczek: Tworzenie potoku przekształcającego dane przy użyciu klastra Hadoop).</span><span class="sxs-lookup"><span data-stu-id="4f56b-125">For a tutorial on how to transform data using Azure Data Factory, see [Tutorial: Build a pipeline to transform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4f56b-126">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="4f56b-126">Prerequisites</span></span>
* <span data-ttu-id="4f56b-127">Zapoznaj się z artykułem [Omówienie samouczka](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) i wykonaj kroki **wymagań wstępnych**.</span><span class="sxs-lookup"><span data-stu-id="4f56b-127">Go through [Tutorial Overview](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) and complete the **prerequisite** steps.</span></span>
* <span data-ttu-id="4f56b-128">Zainstaluj na komputerze narzędzie [Curl](https://curl.haxx.se/dlwiz/).</span><span class="sxs-lookup"><span data-stu-id="4f56b-128">Install [Curl](https://curl.haxx.se/dlwiz/) on your machine.</span></span> <span data-ttu-id="4f56b-129">W połączeniu z poleceniami REST umożliwia ono utworzenie fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="4f56b-129">You use the Curl tool with REST commands to create a data factory.</span></span> 
* <span data-ttu-id="4f56b-130">Postępuj zgodnie z instrukcjami zawartymi w [tym artykule](../azure-resource-manager/resource-group-create-service-principal-portal.md), aby wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="4f56b-130">Follow instructions from [this article](../azure-resource-manager/resource-group-create-service-principal-portal.md) to:</span></span> 
  1. <span data-ttu-id="4f56b-131">Utworzenie aplikacji sieci Web o nazwie **ADFCopyTutorialApp** w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="4f56b-131">Create a Web application named **ADFCopyTutorialApp** in Azure Active Directory.</span></span>
  2. <span data-ttu-id="4f56b-132">Pobranie **identyfikatora klienta** i **klucza tajnego**.</span><span class="sxs-lookup"><span data-stu-id="4f56b-132">Get **client ID** and **secret key**.</span></span> 
  3. <span data-ttu-id="4f56b-133">Uzyskanie **identyfikatora dzierżawy**.</span><span class="sxs-lookup"><span data-stu-id="4f56b-133">Get **tenant ID**.</span></span> 
  4. <span data-ttu-id="4f56b-134">Przypisanie aplikacji **ADFCopyTutorialApp** do roli **Współautor Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="4f56b-134">Assign the **ADFCopyTutorialApp** application to the **Data Factory Contributor** role.</span></span>  
* <span data-ttu-id="4f56b-135">Zainstaluj program [Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="4f56b-135">Install [Azure PowerShell](/powershell/azure/overview).</span></span>  
* <span data-ttu-id="4f56b-136">Uruchom program **PowerShell** i wykonaj następujące czynności.</span><span class="sxs-lookup"><span data-stu-id="4f56b-136">Launch **PowerShell** and do the following steps.</span></span> <span data-ttu-id="4f56b-137">Nie zamykaj programu Azure PowerShell, zanim nie wykonasz wszystkich instrukcji z tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="4f56b-137">Keep Azure PowerShell open until the end of this tutorial.</span></span> <span data-ttu-id="4f56b-138">Jeśli go zamkniesz i otworzysz ponownie, musisz uruchomić te polecenia jeszcze raz.</span><span class="sxs-lookup"><span data-stu-id="4f56b-138">If you close and reopen, you need to run the commands again.</span></span>
  
  1. <span data-ttu-id="4f56b-139">Uruchom poniższe polecenie i wprowadź nazwę użytkownika oraz hasło, których używasz do logowania się w witrynie Azure Portal:</span><span class="sxs-lookup"><span data-stu-id="4f56b-139">Run the following command and enter the user name and password that you use to sign in to the Azure portal:</span></span>
    
    ```PowerShell 
    Login-AzureRmAccount
    ```   
  2. <span data-ttu-id="4f56b-140">Uruchom poniższe polecenie, aby wyświetlić wszystkie subskrypcje dla tego konta:</span><span class="sxs-lookup"><span data-stu-id="4f56b-140">Run the following command to view all the subscriptions for this account:</span></span>

    ```PowerShell     
    Get-AzureRmSubscription
    ``` 
  3. <span data-ttu-id="4f56b-141">Uruchom poniższe polecenie, aby wybrać subskrypcję, z którą chcesz pracować.</span><span class="sxs-lookup"><span data-stu-id="4f56b-141">Run the following command to select the subscription that you want to work with.</span></span> <span data-ttu-id="4f56b-142">Zastąp ciąg **&lt;NameOfAzureSubscription**&gt; nazwą subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="4f56b-142">Replace **&lt;NameOfAzureSubscription**&gt; with the name of your Azure subscription.</span></span> 
     
    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <NameOfAzureSubscription> | Set-AzureRmContext
    ```
  4. <span data-ttu-id="4f56b-143">Utwórz grupę zasobów platformy Azure o nazwie **ADFTutorialResourceGroup** przez uruchomienie następującego polecenia w programie PowerShell:</span><span class="sxs-lookup"><span data-stu-id="4f56b-143">Create an Azure resource group named **ADFTutorialResourceGroup** by running the following command in the PowerShell:</span></span>  

    ```PowerShell     
      New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```
     
      <span data-ttu-id="4f56b-144">Jeśli istnieje już grupa zasobów, można określić, czy należy ją zaktualizować (Y), czy zachować (N).</span><span class="sxs-lookup"><span data-stu-id="4f56b-144">If the resource group already exists, you specify whether to update it (Y) or keep it as (N).</span></span> 
     
      <span data-ttu-id="4f56b-145">W niektórych krokach w tym samouczku zakłada się, że używana jest grupa zasobów o nazwie ADFTutorialResourceGroup.</span><span class="sxs-lookup"><span data-stu-id="4f56b-145">Some of the steps in this tutorial assume that you use the resource group named ADFTutorialResourceGroup.</span></span> <span data-ttu-id="4f56b-146">Jeśli używasz innej grupy zasobów, podczas wykonywania instrukcji w tym samouczku trzeba będzie wstawić jej nazwę zamiast nazwy ADFTutorialResourceGroup.</span><span class="sxs-lookup"><span data-stu-id="4f56b-146">If you use a different resource group, you need to use the name of your resource group in place of ADFTutorialResourceGroup in this tutorial.</span></span>

## <a name="create-json-definitions"></a><span data-ttu-id="4f56b-147">Tworzenie definicji JSON</span><span class="sxs-lookup"><span data-stu-id="4f56b-147">Create JSON definitions</span></span>
<span data-ttu-id="4f56b-148">W folderze, w którym znajduje się narzędzie curl.exe, utwórz następujące pliki w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="4f56b-148">Create following JSON files in the folder where curl.exe is located.</span></span> 

### <a name="datafactoryjson"></a><span data-ttu-id="4f56b-149">datafactory.json</span><span class="sxs-lookup"><span data-stu-id="4f56b-149">datafactory.json</span></span>
> [!IMPORTANT]
> <span data-ttu-id="4f56b-150">Nazwa musi być globalnie unikatowa — można o to zadbać, dodając do niej prefiks/sufiks ADFCopyTutorialDF.</span><span class="sxs-lookup"><span data-stu-id="4f56b-150">Name must be globally unique, so you may want to prefix/suffix ADFCopyTutorialDF to make it a unique name.</span></span> 
> 
> 

```JSON
{  
    "name": "ADFCopyTutorialDF",  
    "location": "WestUS"
}  
```

### <a name="azurestoragelinkedservicejson"></a><span data-ttu-id="4f56b-151">azurestoragelinkedservice.json</span><span class="sxs-lookup"><span data-stu-id="4f56b-151">azurestoragelinkedservice.json</span></span>
> [!IMPORTANT]
> <span data-ttu-id="4f56b-152">Zastąp wartości **accountname** i **accountkey** nazwą konta usługi Azure Storage oraz jego kluczem.</span><span class="sxs-lookup"><span data-stu-id="4f56b-152">Replace **accountname** and **accountkey** with name and key of your Azure storage account.</span></span> <span data-ttu-id="4f56b-153">Informacje na temat pobierania klucza dostępu do magazynu znajdują się w artykule [Wyświetlanie, kopiowanie i ponowne generowanie kluczy dostępu do magazynu](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).</span><span class="sxs-lookup"><span data-stu-id="4f56b-153">To learn how to get your storage access key, see [View, copy and regenerate storage access keys](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).</span></span>

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

<span data-ttu-id="4f56b-154">Aby uzyskać więcej informacji o właściwościach JSON, zobacz temat dotyczący [połączonej usługi Azure Storage](data-factory-azure-blob-connector.md#azure-storage-linked-service).</span><span class="sxs-lookup"><span data-stu-id="4f56b-154">For details about JSON properties, see [Azure Storage linked service](data-factory-azure-blob-connector.md#azure-storage-linked-service).</span></span>

### <a name="azuersqllinkedservicejson"></a><span data-ttu-id="4f56b-155">azuersqllinkedservice.json</span><span class="sxs-lookup"><span data-stu-id="4f56b-155">azuersqllinkedservice.json</span></span>
> [!IMPORTANT]
> <span data-ttu-id="4f56b-156">Zastąp parametry **servername**, **databasename**, **username** oraz **password** nazwą serwera SQL Azure, bazy danych, konta użytkownika i hasłem do konta.</span><span class="sxs-lookup"><span data-stu-id="4f56b-156">Replace **servername**, **databasename**, **username**, and **password** with name of your Azure SQL server, name of SQL database, user account, and password for the account.</span></span>  
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

<span data-ttu-id="4f56b-157">Aby uzyskać szczegółowe informacje o właściwościach JSON, zobacz temat dotyczący [połączonej usługi Azure SQL](data-factory-azure-sql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="4f56b-157">For details about JSON properties, see [Azure SQL linked service](data-factory-azure-sql-connector.md#linked-service-properties).</span></span>

### <a name="inputdatasetjson"></a><span data-ttu-id="4f56b-158">inputdataset.json</span><span class="sxs-lookup"><span data-stu-id="4f56b-158">inputdataset.json</span></span>

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

<span data-ttu-id="4f56b-159">Poniższa tabela zawiera opis właściwości kodu JSON użytych w tym fragmencie kodu:</span><span class="sxs-lookup"><span data-stu-id="4f56b-159">The following table provides descriptions for the JSON properties used in the snippet:</span></span>

| <span data-ttu-id="4f56b-160">Właściwość</span><span class="sxs-lookup"><span data-stu-id="4f56b-160">Property</span></span> | <span data-ttu-id="4f56b-161">Opis</span><span class="sxs-lookup"><span data-stu-id="4f56b-161">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="4f56b-162">type</span><span class="sxs-lookup"><span data-stu-id="4f56b-162">type</span></span> | <span data-ttu-id="4f56b-163">Właściwość typu jest ustawiona na wartość **AzureBlob**, ponieważ dane znajdują się w magazynie obiektów blob na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="4f56b-163">The type property is set to **AzureBlob** because data resides in an Azure blob storage.</span></span> |
| <span data-ttu-id="4f56b-164">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="4f56b-164">linkedServiceName</span></span> | <span data-ttu-id="4f56b-165">Odnosi się do utworzonego wcześniej elementu **AzureStorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="4f56b-165">Refers to the **AzureStorageLinkedService** that you created earlier.</span></span> |
| <span data-ttu-id="4f56b-166">folderPath</span><span class="sxs-lookup"><span data-stu-id="4f56b-166">folderPath</span></span> | <span data-ttu-id="4f56b-167">Określa **kontener** obiektów blob oraz **folder**, który zawiera wejściowe obiekty blob.</span><span class="sxs-lookup"><span data-stu-id="4f56b-167">Specifies the blob **container** and the **folder** that contains input blobs.</span></span> <span data-ttu-id="4f56b-168">W tym samouczku kontenerem obiektów blob jest adftutorial, a folderem — katalog główny.</span><span class="sxs-lookup"><span data-stu-id="4f56b-168">In this tutorial, adftutorial is the blob container and folder is the root folder.</span></span> | 
| <span data-ttu-id="4f56b-169">fileName</span><span class="sxs-lookup"><span data-stu-id="4f56b-169">fileName</span></span> | <span data-ttu-id="4f56b-170">Ta właściwość jest opcjonalna.</span><span class="sxs-lookup"><span data-stu-id="4f56b-170">This property is optional.</span></span> <span data-ttu-id="4f56b-171">Jeśli pominiesz tę właściwość, zostaną wybrane wszystkie pliki z folderu folderPath.</span><span class="sxs-lookup"><span data-stu-id="4f56b-171">If you omit this property, all files from the folderPath are picked.</span></span> <span data-ttu-id="4f56b-172">W tym samouczku dla fileName określono plik **emp.txt**, więc tylko on zostanie wybrany do przetwarzania.</span><span class="sxs-lookup"><span data-stu-id="4f56b-172">In this tutorial, **emp.txt** is specified for the fileName, so only that file is picked up for processing.</span></span> |
| <span data-ttu-id="4f56b-173">format -> type</span><span class="sxs-lookup"><span data-stu-id="4f56b-173">format -> type</span></span> |<span data-ttu-id="4f56b-174">Plik wejściowy jest w formacie tekstowym, więc należy użyć właściwości **TextFormat**.</span><span class="sxs-lookup"><span data-stu-id="4f56b-174">The input file is in the text format, so we use **TextFormat**.</span></span> |
| <span data-ttu-id="4f56b-175">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="4f56b-175">columnDelimiter</span></span> | <span data-ttu-id="4f56b-176">Kolumny w pliku wejściowym są rozdzielane **przecinkami (`,`)**.</span><span class="sxs-lookup"><span data-stu-id="4f56b-176">The columns in the input file are delimited by **comma character (`,`)**.</span></span> |
| <span data-ttu-id="4f56b-177">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="4f56b-177">frequency/interval</span></span> | <span data-ttu-id="4f56b-178">Właściwość frequency (częstotliwość) jest ustawiona na wartość **Hour** (Godzina), a wartość interwału wynosi **1**, co oznacza, że wycinki wejściowe są dostępne **co godzinę**.</span><span class="sxs-lookup"><span data-stu-id="4f56b-178">The frequency is set to **Hour** and interval is  set to **1**, which means that the input slices are available **hourly**.</span></span> <span data-ttu-id="4f56b-179">Innymi słowy, usługa Data Factory szuka danych wejściowych co godzinę w folderze głównym określonego kontenera obiektów blob (**adftutorial**).</span><span class="sxs-lookup"><span data-stu-id="4f56b-179">In other words, the Data Factory service looks for input data every hour in the root folder of blob container (**adftutorial**) you specified.</span></span> <span data-ttu-id="4f56b-180">Wyszukuje dane między godzinami rozpoczęcia i zakończenia potoku, a nie przed nimi ani po nich.</span><span class="sxs-lookup"><span data-stu-id="4f56b-180">It looks for the data within the pipeline start and end times, not before or after these times.</span></span>  |
| <span data-ttu-id="4f56b-181">external</span><span class="sxs-lookup"><span data-stu-id="4f56b-181">external</span></span> | <span data-ttu-id="4f56b-182">Ta właściwość ma wartość **true** (prawda), jeśli dane nie są generowane przez ten potok.</span><span class="sxs-lookup"><span data-stu-id="4f56b-182">This property is set to **true** if the data is not generated by this pipeline.</span></span> <span data-ttu-id="4f56b-183">Dane wejściowe w tym samouczku znajdują się w pliku emp.txt, który nie jest generowany w tym potoku, więc możemy ustawić tę właściwość na true.</span><span class="sxs-lookup"><span data-stu-id="4f56b-183">The input data in this tutorial is in the emp.txt file, which is not generated by this pipeline, so we set this property to true.</span></span> |

<span data-ttu-id="4f56b-184">Aby uzyskać więcej informacji o tych właściwościach JSON, zobacz [artykuł dotyczący łącznika obiektu blob platformy Azure](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="4f56b-184">For more information about these JSON properties, see [Azure Blob connector article](data-factory-azure-blob-connector.md#dataset-properties).</span></span>

### <a name="outputdatasetjson"></a><span data-ttu-id="4f56b-185">outputdataset.json</span><span class="sxs-lookup"><span data-stu-id="4f56b-185">outputdataset.json</span></span>

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
<span data-ttu-id="4f56b-186">Poniższa tabela zawiera opis właściwości kodu JSON użytych w tym fragmencie kodu:</span><span class="sxs-lookup"><span data-stu-id="4f56b-186">The following table provides descriptions for the JSON properties used in the snippet:</span></span>

| <span data-ttu-id="4f56b-187">Właściwość</span><span class="sxs-lookup"><span data-stu-id="4f56b-187">Property</span></span> | <span data-ttu-id="4f56b-188">Opis</span><span class="sxs-lookup"><span data-stu-id="4f56b-188">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="4f56b-189">type</span><span class="sxs-lookup"><span data-stu-id="4f56b-189">type</span></span> | <span data-ttu-id="4f56b-190">Właściwość typu jest ustawiona na **AzureSqlTable**, ponieważ dane są kopiowane do tabeli w bazie danych SQL na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="4f56b-190">The type property is set to **AzureSqlTable** because data is copied to a table in an Azure SQL database.</span></span> |
| <span data-ttu-id="4f56b-191">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="4f56b-191">linkedServiceName</span></span> | <span data-ttu-id="4f56b-192">Odnosi się do utworzonego wcześniej elementu **AzureSqlLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="4f56b-192">Refers to the **AzureSqlLinkedService** that you created earlier.</span></span> |
| <span data-ttu-id="4f56b-193">tableName</span><span class="sxs-lookup"><span data-stu-id="4f56b-193">tableName</span></span> | <span data-ttu-id="4f56b-194">Określa **tabelę** , do której są kopiowane dane.</span><span class="sxs-lookup"><span data-stu-id="4f56b-194">Specified the **table** to which the data is copied.</span></span> | 
| <span data-ttu-id="4f56b-195">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="4f56b-195">frequency/interval</span></span> | <span data-ttu-id="4f56b-196">Właściwość frequency (częstotliwość) jest ustawiona na wartość **Hour** (Godzina), a wartość interwału wynosi **1**, co oznacza, że wycinki wyjściowe są tworzone **co godzinę** między godziną rozpoczęcia i zakończenia potoku, a nie przed tą godziną lub po niej.</span><span class="sxs-lookup"><span data-stu-id="4f56b-196">The frequency is set to **Hour** and interval is **1**, which means that the output slices are produced **hourly** between the pipeline start and end times, not before or after these times.</span></span>  |

<span data-ttu-id="4f56b-197">Tabela emp bazy danych zawiera trzy kolumny — **ID**, **FirstName** i **LastName**.</span><span class="sxs-lookup"><span data-stu-id="4f56b-197">There are three columns – **ID**, **FirstName**, and **LastName** – in the emp table in the database.</span></span> <span data-ttu-id="4f56b-198">ID to kolumna tożsamości, więc należy określić tylko wartości **FirstName** i **LastName**.</span><span class="sxs-lookup"><span data-stu-id="4f56b-198">ID is an identity column, so you need to specify only **FirstName** and **LastName** here.</span></span>

<span data-ttu-id="4f56b-199">Aby uzyskać więcej informacji o tych właściwościach JSON, zobacz [artykuł dotyczący łącznika usługi Azure SQL](data-factory-azure-sql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="4f56b-199">For more information about these JSON properties, see [Azure SQL connector article](data-factory-azure-sql-connector.md#dataset-properties).</span></span>

### <a name="pipelinejson"></a><span data-ttu-id="4f56b-200">pipeline.json</span><span class="sxs-lookup"><span data-stu-id="4f56b-200">pipeline.json</span></span>

```JSON
{
  "name": "ADFTutorialPipeline",
  "properties": {
    "description": "Copy data from a blob to Azure SQL table",
    "activities": [
      {
        "name": "CopyFromBlobToSQL",
        "description": "Push Regional Effectiveness Campaign data to Azure SQL database",
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

<span data-ttu-id="4f56b-201">Pamiętaj o następujących kwestiach:</span><span class="sxs-lookup"><span data-stu-id="4f56b-201">Note the following points:</span></span>

- <span data-ttu-id="4f56b-202">W sekcji działań jest tylko jedno działanie, którego parametr **type** (typ) został ustawiony na wartość **Copy**.</span><span class="sxs-lookup"><span data-stu-id="4f56b-202">In the activities section, there is only one activity whose **type** is set to **Copy**.</span></span> <span data-ttu-id="4f56b-203">Więcej informacji o działaniu kopiowania znajduje się w artykule dotyczącym [działań związanych z przenoszeniem danych](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="4f56b-203">For more information about the copy activity, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="4f56b-204">W rozwiązaniach usługi Data Factory można również użyć [działań dotyczących przekształcania danych](data-factory-data-transformation-activities.md).</span><span class="sxs-lookup"><span data-stu-id="4f56b-204">In Data Factory solutions, you can also use [data transformation activities](data-factory-data-transformation-activities.md).</span></span>
- <span data-ttu-id="4f56b-205">Dane wejściowe dla działania mają ustawienie **AzureBlobInput**, a dane wyjściowe — **AzureSqlOutput**.</span><span class="sxs-lookup"><span data-stu-id="4f56b-205">Input for the activity is set to **AzureBlobInput** and output for the activity is set to **AzureSqlOutput**.</span></span> 
- <span data-ttu-id="4f56b-206">W sekcji **typeProperties** parametr **BlobSource** został określony jako typ źródłowy, a parametr **SqlSink** został określony jako typ ujścia.</span><span class="sxs-lookup"><span data-stu-id="4f56b-206">In the **typeProperties** section, **BlobSource** is specified as the source type and **SqlSink** is specified as the sink type.</span></span> <span data-ttu-id="4f56b-207">Aby uzyskać pełną listę magazynów danych obsługiwanych przez działanie kopiowania jako źródła i ujścia, zobacz informacje dotyczące [obsługiwanych magazynów danych](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="4f56b-207">For a complete list of data stores supported by the copy activity as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="4f56b-208">Aby dowiedzieć się, jak używać określonego obsługiwanego magazynu danych jako źródła/ujścia, kliknij link w tabeli.</span><span class="sxs-lookup"><span data-stu-id="4f56b-208">To learn how to use a specific supported data store as a source/sink, click the link in the table.</span></span>  
 
<span data-ttu-id="4f56b-209">Zastąp wartość właściwości **start** datą bieżącą, a wartość **end** datą jutrzejszą.</span><span class="sxs-lookup"><span data-stu-id="4f56b-209">Replace the value of the **start** property with the current day and **end** value with the next day.</span></span> <span data-ttu-id="4f56b-210">Możesz określić tylko część daty i pominąć część godziny parametru data/godzina.</span><span class="sxs-lookup"><span data-stu-id="4f56b-210">You can specify only the date part and skip the time part of the date time.</span></span> <span data-ttu-id="4f56b-211">Na przykład „2017-02-03” jest odpowiednikiem „2017-02-03T00:00:00Z”.</span><span class="sxs-lookup"><span data-stu-id="4f56b-211">For example, "2017-02-03", which is equivalent to "2017-02-03T00:00:00Z"</span></span>
 
<span data-ttu-id="4f56b-212">Zarówno data/godzina rozpoczęcia, jak i data/godzina zakończenia muszą być w [formacie ISO](http://en.wikipedia.org/wiki/ISO_8601).</span><span class="sxs-lookup"><span data-stu-id="4f56b-212">Both start and end datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="4f56b-213">Przykładowo: 2016-10-14T16:32:41Z.</span><span class="sxs-lookup"><span data-stu-id="4f56b-213">For example: 2016-10-14T16:32:41Z.</span></span> <span data-ttu-id="4f56b-214">Czas **end** jest opcjonalny, ale w tym samouczku zostanie użyty.</span><span class="sxs-lookup"><span data-stu-id="4f56b-214">The **end** time is optional, but we use it in this tutorial.</span></span> 
 
<span data-ttu-id="4f56b-215">Jeśli nie określisz wartości dla właściwości **end**, zostanie ona obliczona jako „**czas rozpoczęcia + 48 godzin**”.</span><span class="sxs-lookup"><span data-stu-id="4f56b-215">If you do not specify value for the **end** property, it is calculated as "**start + 48 hours**".</span></span> <span data-ttu-id="4f56b-216">Aby uruchomić potok bezterminowo, określ **9999-09-09** jako wartość właściwości **end**.</span><span class="sxs-lookup"><span data-stu-id="4f56b-216">To run the pipeline indefinitely, specify **9999-09-09** as the value for the **end** property.</span></span>
 
<span data-ttu-id="4f56b-217">W powyższym przykładzie występują 24 wycinki danych, gdyż poszczególne wycinki są generowane co godzinę.</span><span class="sxs-lookup"><span data-stu-id="4f56b-217">In the preceding example, there are 24 data slices as each data slice is produced hourly.</span></span>

<span data-ttu-id="4f56b-218">Opisy właściwości JSON w definicji potoku znajdują się w artykule dotyczącym [tworzenia potoków](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="4f56b-218">For descriptions of JSON properties in a pipeline definition, see [create pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="4f56b-219">Opisy właściwości JSON w definicji działania kopiowania znajdują się w artykule dotyczącym [działań związanych z przenoszeniem danych](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="4f56b-219">For descriptions of JSON properties in a copy activity definition, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="4f56b-220">Opisy właściwości JSON obsługiwanych przez BlobSource można znaleźć w [artykule dotyczącym łącznika usługi Azure Blob](data-factory-azure-blob-connector.md).</span><span class="sxs-lookup"><span data-stu-id="4f56b-220">For descriptions of JSON properties supported by BlobSource, see [Azure Blob connector article](data-factory-azure-blob-connector.md).</span></span> <span data-ttu-id="4f56b-221">Opisy właściwości JSON obsługiwanych przez SqlSink można znaleźć w artykule [dotyczącym łącznika usługi Azure SQL Database](data-factory-azure-sql-connector.md).</span><span class="sxs-lookup"><span data-stu-id="4f56b-221">For descriptions of JSON properties supported by SqlSink, see [Azure SQL Database connector article](data-factory-azure-sql-connector.md).</span></span>

## <a name="set-global-variables"></a><span data-ttu-id="4f56b-222">Ustawianie zmiennych globalnych</span><span class="sxs-lookup"><span data-stu-id="4f56b-222">Set global variables</span></span>
<span data-ttu-id="4f56b-223">Po zastąpieniu wartości własnymi wykonaj następujące polecenia w programie Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="4f56b-223">In Azure PowerShell, execute the following commands after replacing the values with your own:</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4f56b-224">Zobacz sekcję [Wymagania wstępne](#prerequisites), aby uzyskać instrukcje dotyczące pobierania identyfikatora klienta, klucza tajnego klienta, identyfikatora dzierżawy oraz identyfikatora subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="4f56b-224">See [Prerequisites](#prerequisites) section for instructions on getting client ID, client secret, tenant ID, and subscription ID.</span></span>   
> 
> 

```JSON
$client_id = "<client ID of application in AAD>"
$client_secret = "<client key of application in AAD>"
$tenant = "<Azure tenant ID>";
$subscription_id="<Azure subscription ID>";

$rg = "ADFTutorialResourceGroup"
```

<span data-ttu-id="4f56b-225">Po zaktualizowaniu nazwy fabryki danych, której używasz, uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="4f56b-225">Run the following command after updating the name of the data factory you are using:</span></span> 

```
$adf = "ADFCopyTutorialDF"
```

## <a name="authenticate-with-aad"></a><span data-ttu-id="4f56b-226">Uwierzytelnianie przy użyciu usługi AAD</span><span class="sxs-lookup"><span data-stu-id="4f56b-226">Authenticate with AAD</span></span>
<span data-ttu-id="4f56b-227">Uruchom następujące polecenie w celu uwierzytelniania za pomocą usługi Azure Active Directory (AAD):</span><span class="sxs-lookup"><span data-stu-id="4f56b-227">Run the following command to authenticate with Azure Active Directory (AAD):</span></span> 

```PowerShell
$cmd = { .\curl.exe -X POST https://login.microsoftonline.com/$tenant/oauth2/token  -F grant_type=client_credentials  -F resource=https://management.core.windows.net/ -F client_id=$client_id -F client_secret=$client_secret };
$responseToken = Invoke-Command -scriptblock $cmd;
$accessToken = (ConvertFrom-Json $responseToken).access_token;

(ConvertFrom-Json $responseToken) 
```

## <a name="create-data-factory"></a><span data-ttu-id="4f56b-228">Tworzenie fabryki danych</span><span class="sxs-lookup"><span data-stu-id="4f56b-228">Create data factory</span></span>
<span data-ttu-id="4f56b-229">W tym kroku opisano tworzenie fabryki danych Azure o nazwie **ADFCopyTutorialDF**.</span><span class="sxs-lookup"><span data-stu-id="4f56b-229">In this step, you create an Azure Data Factory named **ADFCopyTutorialDF**.</span></span> <span data-ttu-id="4f56b-230">Fabryka danych może obejmować jeden lub wiele potoków.</span><span class="sxs-lookup"><span data-stu-id="4f56b-230">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="4f56b-231">Potok może obejmować jedno lub wiele działań.</span><span class="sxs-lookup"><span data-stu-id="4f56b-231">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="4f56b-232">Na przykład działanie kopiowania w celu kopiowania danych ze źródła do docelowego magazynu danych.</span><span class="sxs-lookup"><span data-stu-id="4f56b-232">For example, a Copy Activity to copy data from a source to a destination data store.</span></span> <span data-ttu-id="4f56b-233">Działanie technologii Hive w usłudze HDInsight służące do uruchamiania skryptu Hive używanego do przekształcenia danych wejściowych w dane wyjściowe produktu.</span><span class="sxs-lookup"><span data-stu-id="4f56b-233">A HDInsight Hive activity to run a Hive script to transform input data to product output data.</span></span> <span data-ttu-id="4f56b-234">Uruchom następujące polecenia, aby utworzyć fabrykę danych:</span><span class="sxs-lookup"><span data-stu-id="4f56b-234">Run the following commands to create the data factory:</span></span> 

1. <span data-ttu-id="4f56b-235">Przypisz polecenie do zmiennej o nazwie **cmd**.</span><span class="sxs-lookup"><span data-stu-id="4f56b-235">Assign the command to variable named **cmd**.</span></span> 
   
    > [!IMPORTANT]
    > <span data-ttu-id="4f56b-236">Upewnij się, że określona tutaj nazwa fabryki danych (ADFCopyTutorialDF) odpowiada nazwie podanej w pliku **datafactory.json**.</span><span class="sxs-lookup"><span data-stu-id="4f56b-236">Confirm that the name of the data factory you specify here (ADFCopyTutorialDF) matches the name specified in the **datafactory.json**.</span></span> 
   
    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data “@datafactory.json” https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/ADFCopyTutorialDF0411?api-version=2015-10-01};
    ```
2. <span data-ttu-id="4f56b-237">Uruchom to polecenie przy użyciu polecenia **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="4f56b-237">Run the command by using **Invoke-Command**.</span></span>
   
    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="4f56b-238">Przejrzyj wyniki.</span><span class="sxs-lookup"><span data-stu-id="4f56b-238">View the results.</span></span> <span data-ttu-id="4f56b-239">Jeśli fabryka danych została utworzona pomyślnie, w **wynikach** będzie widoczny kod JSON tej fabryki. W przeciwnym razie zostanie wyświetlony komunikat o błędzie.</span><span class="sxs-lookup"><span data-stu-id="4f56b-239">If the data factory has been successfully created, you see the JSON for the data factory in the **results**; otherwise, you see an error message.</span></span>  
   
    ```
    Write-Host $results
    ```

<span data-ttu-id="4f56b-240">Pamiętaj o następujących kwestiach:</span><span class="sxs-lookup"><span data-stu-id="4f56b-240">Note the following points:</span></span>

* <span data-ttu-id="4f56b-241">Nazwa fabryki danych Azure musi być globalnie unikatowa.</span><span class="sxs-lookup"><span data-stu-id="4f56b-241">The name of the Azure Data Factory must be globally unique.</span></span> <span data-ttu-id="4f56b-242">Jeśli w wynikach jest wyświetlany błąd: **Nazwa fabryki danych „ADFCopyTutorialDF” jest niedostępna**, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="4f56b-242">If you see the error in results: **Data factory name “ADFCopyTutorialDF” is not available**, do the following steps:</span></span>  
  
  1. <span data-ttu-id="4f56b-243">Zmień nazwę fabryki (np. twojanazwaADFCopyTutorialDF) w pliku **datafactory.json**.</span><span class="sxs-lookup"><span data-stu-id="4f56b-243">Change the name (for example, yournameADFCopyTutorialDF) in the **datafactory.json** file.</span></span>
  2. <span data-ttu-id="4f56b-244">W pierwszym poleceniu, w którym zmiennej **$cmd** jest przypisywana wartość, zastąp nazwę ADFCopyTutorialDF nową nazwą i uruchom to polecenie.</span><span class="sxs-lookup"><span data-stu-id="4f56b-244">In the first command where the **$cmd** variable is assigned a value, replace ADFCopyTutorialDF with the new name and run the command.</span></span> 
  3. <span data-ttu-id="4f56b-245">Uruchom kolejne dwa polecenia, aby wywołać interfejs API REST w celu utworzenia fabryki danych i wyświetlić wyniki tej operacji.</span><span class="sxs-lookup"><span data-stu-id="4f56b-245">Run the next two commands to invoke the REST API to create the data factory and print the results of the operation.</span></span> 
     
     <span data-ttu-id="4f56b-246">Artykuł [Data Factory — Naming Rules](data-factory-naming-rules.md) (Fabryka danych — zasady nazewnictwa) zawiera zasady nazewnictwa artefaktów usługi Fabryka danych.</span><span class="sxs-lookup"><span data-stu-id="4f56b-246">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>
* <span data-ttu-id="4f56b-247">Aby tworzyć wystąpienia usługi Fabryka danych, musisz być współautorem/administratorem subskrypcji Azure</span><span class="sxs-lookup"><span data-stu-id="4f56b-247">To create Data Factory instances, you need to be a contributor/administrator of the Azure subscription</span></span>
* <span data-ttu-id="4f56b-248">W przyszłości nazwa fabryki danych może zostać zarejestrowana jako nazwa DNS, a wówczas stanie się widoczna publicznie.</span><span class="sxs-lookup"><span data-stu-id="4f56b-248">The name of the data factory may be registered as a DNS name in the future and hence become publicly visible.</span></span>
* <span data-ttu-id="4f56b-249">Jeśli zostanie wyświetlony komunikat o błędzie: „**Subskrypcja nie jest zarejestrowana w celu używania przestrzeni nazw Microsoft.DataFactory**”, wykonaj jedną z następujących czynności i spróbuj opublikować ponownie:</span><span class="sxs-lookup"><span data-stu-id="4f56b-249">If you receive the error: "**This subscription is not registered to use namespace Microsoft.DataFactory**", do one of the following and try publishing again:</span></span> 
  
  * <span data-ttu-id="4f56b-250">W programie Azure PowerShell uruchom następujące polecenie, aby zarejestrować dostawcę usługi Data Factory:</span><span class="sxs-lookup"><span data-stu-id="4f56b-250">In Azure PowerShell, run the following command to register the Data Factory provider:</span></span> 

    ```PowerShell    
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```
    <span data-ttu-id="4f56b-251">Można uruchomić następujące polecenie, aby potwierdzić, że dostawca usługi Data Factory jest zarejestrowany.</span><span class="sxs-lookup"><span data-stu-id="4f56b-251">You can run the following command to confirm that the Data Factory provider is registered.</span></span> 
    
    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * <span data-ttu-id="4f56b-252">Zaloguj się przy użyciu subskrypcji Azure do [portalu Azure](https://portal.azure.com) i przejdź do bloku Fabryka danych lub utwórz fabrykę danych w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="4f56b-252">Login using the Azure subscription into the [Azure portal](https://portal.azure.com) and navigate to a Data Factory blade (or) create a data factory in the Azure portal.</span></span> <span data-ttu-id="4f56b-253">Ta akcja powoduje automatyczne zarejestrowanie dostawcy.</span><span class="sxs-lookup"><span data-stu-id="4f56b-253">This action automatically registers the provider for you.</span></span>

<span data-ttu-id="4f56b-254">Przed utworzeniem potoku musisz utworzyć kilka jednostek usługi Fabryka danych.</span><span class="sxs-lookup"><span data-stu-id="4f56b-254">Before creating a pipeline, you need to create a few Data Factory entities first.</span></span> <span data-ttu-id="4f56b-255">Najpierw utwórz połączone usługi, aby połączyć źródłowy i docelowy magazyn danych ze swoim magazynem danych.</span><span class="sxs-lookup"><span data-stu-id="4f56b-255">You first create linked services to link source and destination data stores to your data store.</span></span> <span data-ttu-id="4f56b-256">Następnie zdefiniuj wejściowy i wyjściowy zestaw danych w celu reprezentowania danych w połączonych magazynach danych.</span><span class="sxs-lookup"><span data-stu-id="4f56b-256">Then, define input and output datasets to represent data in linked data stores.</span></span> <span data-ttu-id="4f56b-257">Na koniec utwórz potok z działaniem używającym tych zestawów danych.</span><span class="sxs-lookup"><span data-stu-id="4f56b-257">Finally, create the pipeline with an activity that uses these datasets.</span></span>

## <a name="create-linked-services"></a><span data-ttu-id="4f56b-258">Tworzenie połączonych usług</span><span class="sxs-lookup"><span data-stu-id="4f56b-258">Create linked services</span></span>
<span data-ttu-id="4f56b-259">Połączone usługi tworzy się w fabryce danych w celu połączenia magazynów danych i usług obliczeniowych z fabryką danych.</span><span class="sxs-lookup"><span data-stu-id="4f56b-259">You create linked services in a data factory to link your data stores and compute services to the data factory.</span></span> <span data-ttu-id="4f56b-260">W tym samouczku nie przedstawiono korzystania z żadnych usług obliczeniowych, takich jak Azure HDInsight czy Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="4f56b-260">In this tutorial, you don't use any compute service such as Azure HDInsight or Azure Data Lake Analytics.</span></span> <span data-ttu-id="4f56b-261">Zostają użyte dwa magazyny danych typu Azure Storage (źródło) i Azure SQL Database (lokalizacja docelowa).</span><span class="sxs-lookup"><span data-stu-id="4f56b-261">You use two data stores of type Azure Storage (source) and Azure SQL Database (destination).</span></span> <span data-ttu-id="4f56b-262">W związku z tym tworzy się dwie połączone usługi o nazwie AzureStorageLinkedService i AzureSqlLinkedService typu: AzureStorage i AzureSqlDatabase.</span><span class="sxs-lookup"><span data-stu-id="4f56b-262">Therefore, you create two linked services named AzureStorageLinkedService and AzureSqlLinkedService of types: AzureStorage and AzureSqlDatabase.</span></span>  

<span data-ttu-id="4f56b-263">Polecenie AzureStorageLinkedService łączy konto usługi Azure Storage z fabryką danych.</span><span class="sxs-lookup"><span data-stu-id="4f56b-263">The AzureStorageLinkedService links your Azure storage account to the data factory.</span></span> <span data-ttu-id="4f56b-264">Na tym koncie magazynu utworzono kontener i przekazano na nie dane w ramach [wymagań wstępnych](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="4f56b-264">This storage account is the one in which you created a container and uploaded the data as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>   

<span data-ttu-id="4f56b-265">Polecenie AzureSqlLinkedService łączy bazę danych SQL na platformie Azure z fabryką danych.</span><span class="sxs-lookup"><span data-stu-id="4f56b-265">AzureSqlLinkedService links your Azure SQL database to the data factory.</span></span> <span data-ttu-id="4f56b-266">W tej bazie danych są przechowywane dane skopiowane z magazynu obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="4f56b-266">The data that is copied from the blob storage is stored in this database.</span></span> <span data-ttu-id="4f56b-267">Tabelę emp w tej bazie danych utworzono w ramach [wymagań wstępnych](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="4f56b-267">You created the emp table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>  

### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="4f56b-268">Tworzenie połączonej usługi Azure Storage</span><span class="sxs-lookup"><span data-stu-id="4f56b-268">Create Azure Storage linked service</span></span>
<span data-ttu-id="4f56b-269">W tym kroku opisano łączenie konta usługi Azure Storage z fabryką danych.</span><span class="sxs-lookup"><span data-stu-id="4f56b-269">In this step, you link your Azure storage account to your data factory.</span></span> <span data-ttu-id="4f56b-270">W tej sekcji określa się nazwę i klucz konta magazynu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="4f56b-270">You specify the name and key of your Azure storage account in this section.</span></span> <span data-ttu-id="4f56b-271">Szczegóły dotyczące właściwości JSON używanych do definiowania połączonej usługi Azure Storage zawiera temat [Połączona usługa Azure Storage](data-factory-azure-blob-connector.md#azure-storage-linked-service).</span><span class="sxs-lookup"><span data-stu-id="4f56b-271">See [Azure Storage linked service](data-factory-azure-blob-connector.md#azure-storage-linked-service) for details about JSON properties used to define an Azure Storage linked service.</span></span>  

1. <span data-ttu-id="4f56b-272">Przypisz polecenie do zmiennej o nazwie **cmd**.</span><span class="sxs-lookup"><span data-stu-id="4f56b-272">Assign the command to variable named **cmd**.</span></span> 

    ```PowerShell   
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@azurestoragelinkedservice.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/linkedservices/AzureStorageLinkedService?api-version=2015-10-01};
    ```
2. <span data-ttu-id="4f56b-273">Uruchom to polecenie przy użyciu polecenia **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="4f56b-273">Run the command by using **Invoke-Command**.</span></span>

    ```PowerShell   
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="4f56b-274">Przejrzyj wyniki.</span><span class="sxs-lookup"><span data-stu-id="4f56b-274">View the results.</span></span> <span data-ttu-id="4f56b-275">Jeśli połączona usługa została utworzona pomyślnie, w **wynikach** będzie widoczny kod JSON tej usługi. W przeciwnym razie zostanie wyświetlony komunikat o błędzie.</span><span class="sxs-lookup"><span data-stu-id="4f56b-275">If the linked service has been successfully created, you see the JSON for the linked service in the **results**; otherwise, you see an error message.</span></span>

    ```PowerShell   
    Write-Host $results
    ```

### <a name="create-azure-sql-linked-service"></a><span data-ttu-id="4f56b-276">Tworzenie połączonej usługi SQL Azure</span><span class="sxs-lookup"><span data-stu-id="4f56b-276">Create Azure SQL linked service</span></span>
<span data-ttu-id="4f56b-277">W tym kroku opisano łączenie bazy danych Azure SQL Database z fabryką danych.</span><span class="sxs-lookup"><span data-stu-id="4f56b-277">In this step, you link your Azure SQL database to your data factory.</span></span> <span data-ttu-id="4f56b-278">W tej sekcji określa się nazwę serwera usługi Azure SQL, nazwę bazy danych, nazwę użytkownika i hasło użytkownika.</span><span class="sxs-lookup"><span data-stu-id="4f56b-278">You specify the Azure SQL server name, database name, user name, and user password in this section.</span></span> <span data-ttu-id="4f56b-279">Szczegóły dotyczące właściwości JSON używanych do definiowania połączonej usługi Azure SQL zawiera temat [Połączona usługa Azure SQL](data-factory-azure-sql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="4f56b-279">See [Azure SQL linked service](data-factory-azure-sql-connector.md#linked-service-properties) for details about JSON properties used to define an Azure SQL linked service.</span></span>

1. <span data-ttu-id="4f56b-280">Przypisz polecenie do zmiennej o nazwie **cmd**.</span><span class="sxs-lookup"><span data-stu-id="4f56b-280">Assign the command to variable named **cmd**.</span></span> 
   
    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data “@azuresqllinkedservice.json” https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/linkedservices/AzureSqlLinkedService?api-version=2015-10-01};
    ```
2. <span data-ttu-id="4f56b-281">Uruchom to polecenie przy użyciu polecenia **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="4f56b-281">Run the command by using **Invoke-Command**.</span></span>
   
    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="4f56b-282">Przejrzyj wyniki.</span><span class="sxs-lookup"><span data-stu-id="4f56b-282">View the results.</span></span> <span data-ttu-id="4f56b-283">Jeśli połączona usługa została utworzona pomyślnie, w **wynikach** będzie widoczny kod JSON tej usługi. W przeciwnym razie zostanie wyświetlony komunikat o błędzie.</span><span class="sxs-lookup"><span data-stu-id="4f56b-283">If the linked service has been successfully created, you see the JSON for the linked service in the **results**; otherwise, you see an error message.</span></span>
   
    ```PowerShell
    Write-Host $results
    ```

## <a name="create-datasets"></a><span data-ttu-id="4f56b-284">Tworzenie zestawów danych</span><span class="sxs-lookup"><span data-stu-id="4f56b-284">Create datasets</span></span>
<span data-ttu-id="4f56b-285">W poprzednim kroku zostały utworzone połączone usługi używane do połączenia konta usługi Azure Storage i bazy danych Azure SQL z fabryką danych.</span><span class="sxs-lookup"><span data-stu-id="4f56b-285">In the previous step, you created linked services to link your Azure Storage account and Azure SQL database to your data factory.</span></span> <span data-ttu-id="4f56b-286">W tym kroku zostaną zdefiniowane dwa zestawy danych o nazwach AzureBlobInput i AzureSqlOutput zawierające dane wejściowe i wyjściowe przechowywane w magazynach danych, do których odwołują się usługi AzureStorageLinkedService i AzureSqlLinkedService.</span><span class="sxs-lookup"><span data-stu-id="4f56b-286">In this step, you define two datasets named AzureBlobInput and AzureSqlOutput that represent input and output data that is stored in the data stores referred by AzureStorageLinkedService and AzureSqlLinkedService respectively.</span></span>

<span data-ttu-id="4f56b-287">Połączona usługa magazynu Azure określa parametry połączenia, z których korzysta usługa Data Factory w czasie wykonywania, aby połączyć się z kontem magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="4f56b-287">The Azure storage linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure storage account.</span></span> <span data-ttu-id="4f56b-288">Natomiast wejściowy zestaw danych obiektów blob (AzureBlobInput) określa kontener oraz folder, który zawiera dane wejściowe.</span><span class="sxs-lookup"><span data-stu-id="4f56b-288">And, the input blob dataset (AzureBlobInput) specifies the container and the folder that contains the input data.</span></span>  

<span data-ttu-id="4f56b-289">W analogiczny sposób połączona usługa Azure SQL Database określa parametry połączenia, z których korzysta usługa Data Factory w czasie wykonywania, aby połączyć się z bazą danych SQL usługi Azure.</span><span class="sxs-lookup"><span data-stu-id="4f56b-289">Similarly, the Azure SQL Database linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure SQL database.</span></span> <span data-ttu-id="4f56b-290">Wyjściowy zestaw danych tabeli SQL (OutputDataset) określa tabelę w bazie danych, do której są kopiowane dane z magazynu obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="4f56b-290">And, the output SQL table dataset (OututDataset) specifies the table in the database to which the data from the blob storage is copied.</span></span> 

### <a name="create-input-dataset"></a><span data-ttu-id="4f56b-291">Tworzenie wejściowego zestawu danych</span><span class="sxs-lookup"><span data-stu-id="4f56b-291">Create input dataset</span></span>
<span data-ttu-id="4f56b-292">W tym kroku zostanie utworzony zestaw danych o nazwie AzureBlobInput wskazujący na plik obiektów blob (emp.txt) w katalogu głównym kontenera obiektów blob (adftutorial) w usłudze Azure Storage reprezentowany przez połączoną usługę AzureStorageLinkedService.</span><span class="sxs-lookup"><span data-stu-id="4f56b-292">In this step, you create a dataset named AzureBlobInput that points to a blob file (emp.txt) in the root folder of a blob container (adftutorial) in the Azure Storage represented by the AzureStorageLinkedService linked service.</span></span> <span data-ttu-id="4f56b-293">Jeśli nie określisz wartości obiektu fileName lub ją pominiesz, dane ze wszystkich obiektów blob w folderze wejściowym zostaną skopiowane do lokalizacji docelowej.</span><span class="sxs-lookup"><span data-stu-id="4f56b-293">If you don't specify a value for the fileName (or skip it), data from all blobs in the input folder are copied to the destination.</span></span> <span data-ttu-id="4f56b-294">W tym samouczku wartość obiektu fileName jest określona.</span><span class="sxs-lookup"><span data-stu-id="4f56b-294">In this tutorial, you specify a value for the fileName.</span></span> 

1. <span data-ttu-id="4f56b-295">Przypisz polecenie do zmiennej o nazwie **cmd**.</span><span class="sxs-lookup"><span data-stu-id="4f56b-295">Assign the command to variable named **cmd**.</span></span> 

    ```PowerSHell   
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@inputdataset.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/AzureBlobInput?api-version=2015-10-01};
    ```
2. <span data-ttu-id="4f56b-296">Uruchom to polecenie przy użyciu polecenia **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="4f56b-296">Run the command by using **Invoke-Command**.</span></span>
   
    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="4f56b-297">Przejrzyj wyniki.</span><span class="sxs-lookup"><span data-stu-id="4f56b-297">View the results.</span></span> <span data-ttu-id="4f56b-298">Jeśli zestaw danych został utworzony pomyślnie, w **wynikach** będzie widoczny kod JSON tego zestawu. W przeciwnym razie zostanie wyświetlony komunikat o błędzie.</span><span class="sxs-lookup"><span data-stu-id="4f56b-298">If the dataset has been successfully created, you see the JSON for the dataset in the **results**; otherwise, you see an error message.</span></span>
   
    ```PowerShell
    Write-Host $results
    ```

### <a name="create-output-dataset"></a><span data-ttu-id="4f56b-299">Tworzenie wyjściowego zestawu danych</span><span class="sxs-lookup"><span data-stu-id="4f56b-299">Create output dataset</span></span>
<span data-ttu-id="4f56b-300">Połączona usługa Azure SQL Database określa parametry połączenia, z których korzysta usługa Data Factory w czasie wykonywania, aby połączyć się z bazą danych SQL usługi Azure.</span><span class="sxs-lookup"><span data-stu-id="4f56b-300">The Azure SQL Database linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure SQL database.</span></span> <span data-ttu-id="4f56b-301">Wyjściowy zestaw danych tabeli SQL (OutputDataset) tworzony w tym kroku określa tabelę w bazie danych, do której są kopiowane dane z magazynu obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="4f56b-301">The output SQL table dataset (OututDataset) you create in this step specifies the table in the database to which the data from the blob storage is copied.</span></span>

1. <span data-ttu-id="4f56b-302">Przypisz polecenie do zmiennej o nazwie **cmd**.</span><span class="sxs-lookup"><span data-stu-id="4f56b-302">Assign the command to variable named **cmd**.</span></span>

    ```PowerShell   
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@outputdataset.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/AzureSqlOutput?api-version=2015-10-01};
    ```
2. <span data-ttu-id="4f56b-303">Uruchom to polecenie przy użyciu polecenia **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="4f56b-303">Run the command by using **Invoke-Command**.</span></span>
    
    ```PowerShell   
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="4f56b-304">Przejrzyj wyniki.</span><span class="sxs-lookup"><span data-stu-id="4f56b-304">View the results.</span></span> <span data-ttu-id="4f56b-305">Jeśli zestaw danych został utworzony pomyślnie, w **wynikach** będzie widoczny kod JSON tego zestawu. W przeciwnym razie zostanie wyświetlony komunikat o błędzie.</span><span class="sxs-lookup"><span data-stu-id="4f56b-305">If the dataset has been successfully created, you see the JSON for the dataset in the **results**; otherwise, you see an error message.</span></span>
   
    ```PowerShell
    Write-Host $results
    ``` 

## <a name="create-pipeline"></a><span data-ttu-id="4f56b-306">Tworzenie potoku</span><span class="sxs-lookup"><span data-stu-id="4f56b-306">Create pipeline</span></span>
<span data-ttu-id="4f56b-307">W tym kroku za pomocą **działania kopiowania** zostanie utworzony potok, w którym parametr **AzureBlobInput** jest używany jako dane wejściowe, a parametr **AzureSqlOutput** jako dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="4f56b-307">In this step, you create a pipeline with a **copy activity** that uses **AzureBlobInput** as an input and **AzureSqlOutput** as an output.</span></span>

<span data-ttu-id="4f56b-308">Obecnie harmonogram jest prowadzony przy użyciu wyjściowego zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="4f56b-308">Currently, output dataset is what drives the schedule.</span></span> <span data-ttu-id="4f56b-309">W tym samouczku wyjściowy zestaw danych jest konfigurowany do tworzenia wycinka co godzinę.</span><span class="sxs-lookup"><span data-stu-id="4f56b-309">In this tutorial, output dataset is configured to produce a slice once an hour.</span></span> <span data-ttu-id="4f56b-310">Potok ma godzinę rozpoczęcia i zakończenia, między którymi następuje jeden dzień różnicy (dokładnie 24 godziny).</span><span class="sxs-lookup"><span data-stu-id="4f56b-310">The pipeline has a start time and end time that are one day apart, which is 24 hours.</span></span> <span data-ttu-id="4f56b-311">Potok tworzy więc 24 wycinki wyjściowego zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="4f56b-311">Therefore, 24 slices of output dataset are produced by the pipeline.</span></span> 

1. <span data-ttu-id="4f56b-312">Przypisz polecenie do zmiennej o nazwie **cmd**.</span><span class="sxs-lookup"><span data-stu-id="4f56b-312">Assign the command to variable named **cmd**.</span></span>

    ```PowerShell   
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@pipeline.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datapipelines/MyFirstPipeline?api-version=2015-10-01};
    ```
2. <span data-ttu-id="4f56b-313">Uruchom to polecenie przy użyciu polecenia **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="4f56b-313">Run the command by using **Invoke-Command**.</span></span>

    ```PowerShell   
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="4f56b-314">Przejrzyj wyniki.</span><span class="sxs-lookup"><span data-stu-id="4f56b-314">View the results.</span></span> <span data-ttu-id="4f56b-315">Jeśli zestaw danych został utworzony pomyślnie, w **wynikach** będzie widoczny kod JSON tego zestawu. W przeciwnym razie zostanie wyświetlony komunikat o błędzie.</span><span class="sxs-lookup"><span data-stu-id="4f56b-315">If the dataset has been successfully created, you see the JSON for the dataset in the **results**; otherwise, you see an error message.</span></span>  

    ```PowerShell   
    Write-Host $results
    ```

<span data-ttu-id="4f56b-316">**Gratulacje!**</span><span class="sxs-lookup"><span data-stu-id="4f56b-316">**Congratulations!**</span></span> <span data-ttu-id="4f56b-317">Fabryka danych Azure z potokiem kopiującym dane z usługi Azure Blob Storage do bazy danych Azure SQL Database została pomyślnie utworzona.</span><span class="sxs-lookup"><span data-stu-id="4f56b-317">You have successfully created an Azure data factory, with a pipeline that copies data from Azure Blob Storage to Azure SQL database.</span></span>

## <a name="monitor-pipeline"></a><span data-ttu-id="4f56b-318">Monitorowanie potoku</span><span class="sxs-lookup"><span data-stu-id="4f56b-318">Monitor pipeline</span></span>
<span data-ttu-id="4f56b-319">W tym kroku interfejs API REST usługi Data Factory służy do monitorowania wycinków generowanych przez potok.</span><span class="sxs-lookup"><span data-stu-id="4f56b-319">In this step, you use Data Factory REST API to monitor slices being produced by the pipeline.</span></span>

```PowerShell
$ds ="AzureSqlOutput"
```

> [!IMPORTANT] 
> <span data-ttu-id="4f56b-320">Upewnij się, że godziny rozpoczęcia i zakończenia określone w następującym poleceniu są zgodne z godzinami rozpoczęcia i zakończenia potoku.</span><span class="sxs-lookup"><span data-stu-id="4f56b-320">Make sure that the start and end times specified in the following command match the start and end times of the pipeline.</span></span> 

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

<span data-ttu-id="4f56b-321">Uruchom polecenie Invoke-Command i kolejne polecenie, aż zobaczysz, że wycinek jest w stanie **Gotowe** lub **Niepowodzenie**.</span><span class="sxs-lookup"><span data-stu-id="4f56b-321">Run the Invoke-Command and the next one until you see a slice in **Ready** state or **Failed** state.</span></span> <span data-ttu-id="4f56b-322">Gdy wycinek jest w stanie Gotowe, sprawdź, czy w tabeli **emp** w bazie danych Azure SQL Database znajdują się dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="4f56b-322">When the slice is in Ready state, check the **emp** table in your Azure SQL database for the output data.</span></span> 

<span data-ttu-id="4f56b-323">Dla każdego wycinka do tabeli emp w bazie danych Azure SQL Database zostają skopiowane dwa wiersze danych z pliku źródłowego.</span><span class="sxs-lookup"><span data-stu-id="4f56b-323">For each slice, two rows of data from the source file are copied to the emp table in the Azure SQL database.</span></span> <span data-ttu-id="4f56b-324">Po pomyślnym przetworzeniu wycinków (stan Gotowe) w tabeli emp będą widoczne 24 nowe rekordy.</span><span class="sxs-lookup"><span data-stu-id="4f56b-324">Therefore, you see 24 new records in the emp table when all the slices are successfully processed (in Ready state).</span></span> 

## <a name="summary"></a><span data-ttu-id="4f56b-325">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="4f56b-325">Summary</span></span>
<span data-ttu-id="4f56b-326">W tym samouczku opisano tworzenie fabryki danych Azure za pomocą interfejsu API REST w celu kopiowania danych z obiektu blob Azure do bazy danych Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="4f56b-326">In this tutorial, you used REST API to create an Azure data factory to copy data from an Azure blob to an Azure SQL database.</span></span> <span data-ttu-id="4f56b-327">Główne kroki opisane w tym samouczku:</span><span class="sxs-lookup"><span data-stu-id="4f56b-327">Here are the high-level steps you performed in this tutorial:</span></span>  

1. <span data-ttu-id="4f56b-328">Tworzenie **fabryki danych** Azure.</span><span class="sxs-lookup"><span data-stu-id="4f56b-328">Created an Azure **data factory**.</span></span>
2. <span data-ttu-id="4f56b-329">Tworzenie **połączonych usług**:</span><span class="sxs-lookup"><span data-stu-id="4f56b-329">Created **linked services**:</span></span>
   1. <span data-ttu-id="4f56b-330">Połączona usługa Azure Storage, która ma nawiązać połączenie z kontem usługi Azure Storage, na którym przechowywane są dane wejściowe.</span><span class="sxs-lookup"><span data-stu-id="4f56b-330">An Azure Storage linked service to link your Azure Storage account that holds input data.</span></span>     
   2. <span data-ttu-id="4f56b-331">Połączona usługa SQL Azure, która ma nawiązać połączenie z bazą danych Azure SQL Database, w której przechowywane są dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="4f56b-331">An Azure SQL linked service to link your Azure SQL database that holds the output data.</span></span> 
3. <span data-ttu-id="4f56b-332">Tworzenie **zestawów danych** opisujących dane wejściowe i wyjściowe dla potoków.</span><span class="sxs-lookup"><span data-stu-id="4f56b-332">Created **datasets**, which describe input data and output data for pipelines.</span></span>
4. <span data-ttu-id="4f56b-333">Tworzenie **potoku** za pomocą działania kopiowania, w którym źródłem jest element BlobSource, a ujściem element SqlSink.</span><span class="sxs-lookup"><span data-stu-id="4f56b-333">Created a **pipeline** with a Copy Activity with BlobSource as source and SqlSink as sink.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="4f56b-334">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="4f56b-334">Next steps</span></span>
<span data-ttu-id="4f56b-335">W tym samouczku użyto magazynu obiektów blob platformy Azure jako magazynu danych źródła oraz bazy danych SQL na platformie Azure jako magazynu danych docelowych w operacji kopiowania.</span><span class="sxs-lookup"><span data-stu-id="4f56b-335">In this tutorial, you used Azure blob storage as a source data store and an Azure SQL database as a destination data store in a copy operation.</span></span> <span data-ttu-id="4f56b-336">Poniższa tabela zawiera listę magazynów danych obsługiwanych przez działanie kopiowania jako źródła i lokalizacje docelowe:</span><span class="sxs-lookup"><span data-stu-id="4f56b-336">The following table provides a list of data stores supported as sources and destinations by the copy activity:</span></span> 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

<span data-ttu-id="4f56b-337">Aby uzyskać informacje dotyczące kopiowania danych do/z magazynu danych, kliknij link do magazynu danych w tabeli.</span><span class="sxs-lookup"><span data-stu-id="4f56b-337">To learn about how to copy data to/from a data store, click the link for the data store in the table.</span></span>