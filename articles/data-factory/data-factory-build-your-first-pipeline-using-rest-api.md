---
title: Tworzenie pierwszej fabryki danych (REST) | Microsoft Docs
description: "W tym samouczku przedstawiono instrukcje tworzenia przykładowego potoku usługi Azure Data Factory przy użyciu interfejsu API REST usługi Data Factory."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 7e0a2465-2d85-4143-a4bb-42e03c273097
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: b0c237667f1f55298df20ab0f525202aa1b42e0b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="tutorial-build-your-first-azure-data-factory-using-data-factory-rest-api"></a><span data-ttu-id="22625-103">Samouczek: Tworzenie pierwszej fabryki danych Azure przy użyciu interfejsu API REST usługi Fabryka danych</span><span class="sxs-lookup"><span data-stu-id="22625-103">Tutorial: Build your first Azure data factory using Data Factory REST API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="22625-104">Przegląd i wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="22625-104">Overview and prerequisites</span></span>](data-factory-build-your-first-pipeline.md)
> * [<span data-ttu-id="22625-105">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="22625-105">Azure portal</span></span>](data-factory-build-your-first-pipeline-using-editor.md)
> * [<span data-ttu-id="22625-106">Program Visual Studio</span><span class="sxs-lookup"><span data-stu-id="22625-106">Visual Studio</span></span>](data-factory-build-your-first-pipeline-using-vs.md)
> * [<span data-ttu-id="22625-107">Program PowerShell</span><span class="sxs-lookup"><span data-stu-id="22625-107">PowerShell</span></span>](data-factory-build-your-first-pipeline-using-powershell.md)
> * [<span data-ttu-id="22625-108">Szablon usługi Resource Manager</span><span class="sxs-lookup"><span data-stu-id="22625-108">Resource Manager Template</span></span>](data-factory-build-your-first-pipeline-using-arm.md)
> * [<span data-ttu-id="22625-109">Interfejs API REST</span><span class="sxs-lookup"><span data-stu-id="22625-109">REST API</span></span>](data-factory-build-your-first-pipeline-using-rest-api.md)
>
>


<span data-ttu-id="22625-110">Ten artykuł zawiera instrukcje korzystania z interfejsu API REST usługi Fabryka danych w celu utworzenia pierwszej fabryki danych Azure.</span><span class="sxs-lookup"><span data-stu-id="22625-110">In this article, you use Data Factory REST API to create your first Azure data factory.</span></span> <span data-ttu-id="22625-111">Aby wykonać instrukcje z tego samouczka przy użyciu innych narzędzi/zestawów SDK, wybierz jedną z opcji z listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="22625-111">To do the tutorial using other tools/SDKs, select one of the options from the drop-down list.</span></span>

<span data-ttu-id="22625-112">Potok w tym samouczku zawiera jedno działanie: **działanie Hive usługi HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="22625-112">The pipeline in this tutorial has one activity: **HDInsight Hive activity**.</span></span> <span data-ttu-id="22625-113">To działanie uruchamia skrypt Hive w klastrze Azure HDInsight, który przekształca dane wejściowe, aby wygenerować dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="22625-113">This activity runs a hive script on an Azure HDInsight cluster that transforms input data to produce output data.</span></span> <span data-ttu-id="22625-114">Uruchamianie potoku zaplanowano raz w miesiącu między określonym czasem rozpoczęcia i zakończenia.</span><span class="sxs-lookup"><span data-stu-id="22625-114">The pipeline is scheduled to run once a month between the specified start and end times.</span></span>

> [!NOTE]
> <span data-ttu-id="22625-115">Ten artykuł nie obejmuje całego interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="22625-115">This article does not cover all the REST API.</span></span> <span data-ttu-id="22625-116">Pełna dokumentacja dotycząca interfejsu API REST znajduje się w [Dokumentacji interfejsu API REST usługi Data Factory](/rest/api/datafactory/).</span><span class="sxs-lookup"><span data-stu-id="22625-116">For comprehensive documentation on REST API, see [Data Factory REST API Reference](/rest/api/datafactory/).</span></span>
> 
> <span data-ttu-id="22625-117">Potok może obejmować więcej niż jedno działanie.</span><span class="sxs-lookup"><span data-stu-id="22625-117">A pipeline can have more than one activity.</span></span> <span data-ttu-id="22625-118">Dwa działania można połączyć w łańcuch (uruchomić jedno działanie po drugim), ustawiając wyjściowy zestaw danych jednego działania jako zestaw wejściowy drugiego.</span><span class="sxs-lookup"><span data-stu-id="22625-118">And, you can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity.</span></span> <span data-ttu-id="22625-119">Więcej informacji znajduje się w artykule dotyczącym [planowania i wykonywania w usłudze Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span><span class="sxs-lookup"><span data-stu-id="22625-119">For more information, see [scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="22625-120">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="22625-120">Prerequisites</span></span>
* <span data-ttu-id="22625-121">Przeczytaj artykuł [Omówienie samouczka](data-factory-build-your-first-pipeline.md) oraz wykonaj kroki **wymagań wstępnych**.</span><span class="sxs-lookup"><span data-stu-id="22625-121">Read through [Tutorial Overview](data-factory-build-your-first-pipeline.md) article and complete the **prerequisite** steps.</span></span>
* <span data-ttu-id="22625-122">Zainstaluj na komputerze narzędzie [Curl](https://curl.haxx.se/dlwiz/).</span><span class="sxs-lookup"><span data-stu-id="22625-122">Install [Curl](https://curl.haxx.se/dlwiz/) on your machine.</span></span> <span data-ttu-id="22625-123">W połączeniu z poleceniami REST umożliwia ono utworzenie fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="22625-123">You use the CURL tool with REST commands to create a data factory.</span></span>
* <span data-ttu-id="22625-124">Postępuj zgodnie z instrukcjami zawartymi w [tym artykule](../azure-resource-manager/resource-group-create-service-principal-portal.md), aby wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="22625-124">Follow instructions from [this article](../azure-resource-manager/resource-group-create-service-principal-portal.md) to:</span></span>
  1. <span data-ttu-id="22625-125">Utworzenie aplikacji sieci Web o nazwie **ADFGetStartedApp** w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="22625-125">Create a Web application named **ADFGetStartedApp** in Azure Active Directory.</span></span>
  2. <span data-ttu-id="22625-126">Pobranie **identyfikatora klienta** i **klucza tajnego**.</span><span class="sxs-lookup"><span data-stu-id="22625-126">Get **client ID** and **secret key**.</span></span>
  3. <span data-ttu-id="22625-127">Uzyskanie **identyfikatora dzierżawy**.</span><span class="sxs-lookup"><span data-stu-id="22625-127">Get **tenant ID**.</span></span>
  4. <span data-ttu-id="22625-128">Przypisanie aplikacji **ADFGetStartedApp** do roli **Współautor Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="22625-128">Assign the **ADFGetStartedApp** application to the **Data Factory Contributor** role.</span></span>
* <span data-ttu-id="22625-129">Zainstaluj program [Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="22625-129">Install [Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="22625-130">Uruchom program **PowerShell** i uruchom następujące polecenie.</span><span class="sxs-lookup"><span data-stu-id="22625-130">Launch **PowerShell** and run the following command.</span></span> <span data-ttu-id="22625-131">Nie zamykaj programu Azure PowerShell, zanim nie wykonasz wszystkich instrukcji z tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="22625-131">Keep Azure PowerShell open until the end of this tutorial.</span></span> <span data-ttu-id="22625-132">Jeśli go zamkniesz i otworzysz ponownie, musisz uruchomić te polecenia jeszcze raz.</span><span class="sxs-lookup"><span data-stu-id="22625-132">If you close and reopen, you need to run the commands again.</span></span>
  1. <span data-ttu-id="22625-133">Uruchom polecenie **Login-AzureRmAccount** i wprowadź nazwę użytkownika oraz hasło, których używasz do logowania się w witrynie Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="22625-133">Run **Login-AzureRmAccount** and enter the user name and password that you use to sign in to the Azure portal.</span></span>
  2. <span data-ttu-id="22625-134">Uruchom polecenie **Get-AzureRmSubscription**, aby wyświetlić wszystkie subskrypcje dla tego konta.</span><span class="sxs-lookup"><span data-stu-id="22625-134">Run **Get-AzureRmSubscription** to view all the subscriptions for this account.</span></span>
  3. <span data-ttu-id="22625-135">Uruchom polecenie **Get-AzureRmSubscription -SubscriptionName NameOfAzureSubscription | Set-AzureRmContext**, aby wybrać subskrypcję, której chcesz używać.</span><span class="sxs-lookup"><span data-stu-id="22625-135">Run **Get-AzureRmSubscription -SubscriptionName NameOfAzureSubscription | Set-AzureRmContext** to select the subscription that you want to work with.</span></span> <span data-ttu-id="22625-136">Zastąp ciąg **NameOfAzureSubscription** nazwą subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="22625-136">Replace **NameOfAzureSubscription** with the name of your Azure subscription.</span></span>
* <span data-ttu-id="22625-137">Utwórz grupę zasobów platformy Azure o nazwie **ADFTutorialResourceGroup** przez uruchomienie następującego polecenia w programie PowerShell:</span><span class="sxs-lookup"><span data-stu-id="22625-137">Create an Azure resource group named **ADFTutorialResourceGroup** by running the following command in the PowerShell:</span></span>

    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```

   <span data-ttu-id="22625-138">W niektórych krokach w tym samouczku zakłada się, że używana jest grupa zasobów o nazwie ADFTutorialResourceGroup.</span><span class="sxs-lookup"><span data-stu-id="22625-138">Some of the steps in this tutorial assume that you use the resource group named ADFTutorialResourceGroup.</span></span> <span data-ttu-id="22625-139">Jeśli używasz innej grupy zasobów, podczas wykonywania instrukcji w tym samouczku trzeba będzie wstawić jej nazwę zamiast nazwy ADFTutorialResourceGroup.</span><span class="sxs-lookup"><span data-stu-id="22625-139">If you use a different resource group, you need to use the name of your resource group in place of ADFTutorialResourceGroup in this tutorial.</span></span>

## <a name="create-json-definitions"></a><span data-ttu-id="22625-140">Tworzenie definicji JSON</span><span class="sxs-lookup"><span data-stu-id="22625-140">Create JSON definitions</span></span>
<span data-ttu-id="22625-141">W folderze, w którym znajduje się narzędzie curl.exe, utwórz następujące pliki w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="22625-141">Create following JSON files in the folder where curl.exe is located.</span></span>

### <a name="datafactoryjson"></a><span data-ttu-id="22625-142">datafactory.json</span><span class="sxs-lookup"><span data-stu-id="22625-142">datafactory.json</span></span>
> [!IMPORTANT]
> <span data-ttu-id="22625-143">Nazwa musi być globalnie unikatowa — można o to zadbać, dodając do niej prefiks/sufiks ADFCopyTutorialDF.</span><span class="sxs-lookup"><span data-stu-id="22625-143">Name must be globally unique, so you may want to prefix/suffix ADFCopyTutorialDF to make it a unique name.</span></span>
>
>

```JSON
{
    "name": "FirstDataFactoryREST",
    "location": "WestUS"
}
```

### <a name="azurestoragelinkedservicejson"></a><span data-ttu-id="22625-144">azurestoragelinkedservice.json</span><span class="sxs-lookup"><span data-stu-id="22625-144">azurestoragelinkedservice.json</span></span>
> [!IMPORTANT]
> <span data-ttu-id="22625-145">Zastąp wartości **accountname** i **accountkey** nazwą konta usługi Azure Storage oraz jego kluczem.</span><span class="sxs-lookup"><span data-stu-id="22625-145">Replace **accountname** and **accountkey** with name and key of your Azure storage account.</span></span> <span data-ttu-id="22625-146">Aby dowiedzieć się, jak uzyskać klucz dostępu do magazynu, zapoznaj się z informacjami na temat sposobów wyświetlania, kopiowania i ponownego generowania kluczy dostępu do magazynu w sekcji [Zarządzanie kontem magazynu](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="22625-146">To learn how to get your storage access key, see the information about how to view, copy, and regenerate storage access keys in [Manage your storage account](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>
>
>

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

### <a name="hdinsightondemandlinkedservicejson"></a><span data-ttu-id="22625-147">hdinsightondemandlinkedservice.json</span><span class="sxs-lookup"><span data-stu-id="22625-147">hdinsightondemandlinkedservice.json</span></span>

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

<span data-ttu-id="22625-148">Poniższa tabela zawiera opis właściwości kodu JSON użytych w tym fragmencie kodu:</span><span class="sxs-lookup"><span data-stu-id="22625-148">The following table provides descriptions for the JSON properties used in the snippet:</span></span>

| <span data-ttu-id="22625-149">Właściwość</span><span class="sxs-lookup"><span data-stu-id="22625-149">Property</span></span> | <span data-ttu-id="22625-150">Opis</span><span class="sxs-lookup"><span data-stu-id="22625-150">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="22625-151">ClusterSize</span><span class="sxs-lookup"><span data-stu-id="22625-151">ClusterSize</span></span> |<span data-ttu-id="22625-152">Rozmiar klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="22625-152">Size of the HDInsight cluster.</span></span> |
| <span data-ttu-id="22625-153">TimeToLive</span><span class="sxs-lookup"><span data-stu-id="22625-153">TimeToLive</span></span> |<span data-ttu-id="22625-154">Określa czas bezczynności, po którym klaster usługi HDInsight zostanie usunięty.</span><span class="sxs-lookup"><span data-stu-id="22625-154">Specifies that the idle time for the HDInsight cluster, before it is deleted.</span></span> |
| <span data-ttu-id="22625-155">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="22625-155">linkedServiceName</span></span> |<span data-ttu-id="22625-156">Określa konto magazynu używane do przechowywania dzienników generowanych w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="22625-156">Specifies the storage account that is used to store the logs that are generated by HDInsight</span></span> |

<span data-ttu-id="22625-157">Pamiętaj o następujących kwestiach:</span><span class="sxs-lookup"><span data-stu-id="22625-157">Note the following points:</span></span>

* <span data-ttu-id="22625-158">Usługa Data Factory tworzy klaster usługi HDInsight **oparty na systemie Linux** za pomocą powyższego kodu JSON.</span><span class="sxs-lookup"><span data-stu-id="22625-158">The Data Factory creates a **Linux-based** HDInsight cluster for you with the above JSON.</span></span> <span data-ttu-id="22625-159">Szczegółowe informacje znajdują się w artykule [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) (Połączona usługa HDInsight na żądanie).</span><span class="sxs-lookup"><span data-stu-id="22625-159">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>
* <span data-ttu-id="22625-160">Możesz użyć **własnego klastra usługi HDInsight** zamiast klastra usługi HDInsight na żądanie.</span><span class="sxs-lookup"><span data-stu-id="22625-160">You could use **your own HDInsight cluster** instead of using an on-demand HDInsight cluster.</span></span> <span data-ttu-id="22625-161">Szczegółowe informacje znajdują się w artykule [HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) (Połączona usługa HDInsight).</span><span class="sxs-lookup"><span data-stu-id="22625-161">See [HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) for details.</span></span>
* <span data-ttu-id="22625-162">Klaster usługi HDInsight tworzy **kontener domyślny** w magazynie obiektów blob określonym w kodzie JSON (**linkedServiceName**).</span><span class="sxs-lookup"><span data-stu-id="22625-162">The HDInsight cluster creates a **default container** in the blob storage you specified in the JSON (**linkedServiceName**).</span></span> <span data-ttu-id="22625-163">Usługa HDInsight nie powoduje usunięcia tego kontenera w przypadku usunięcia klastra.</span><span class="sxs-lookup"><span data-stu-id="22625-163">HDInsight does not delete this container when the cluster is deleted.</span></span> <span data-ttu-id="22625-164">To zachowanie jest celowe.</span><span class="sxs-lookup"><span data-stu-id="22625-164">This behavior is by design.</span></span> <span data-ttu-id="22625-165">W przypadku połączonej usługi HDInsight na żądanie klaster usługi HDInsight jest tworzony przy każdym przetwarzaniu wycinka — o ile w tym momencie nie istnieje aktywny klaster (**timeToLive**) — i zostaje usunięty po zakończeniu przetwarzania.</span><span class="sxs-lookup"><span data-stu-id="22625-165">With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice is processed unless there is an existing live cluster (**timeToLive**) and is deleted when the processing is done.</span></span>

    <span data-ttu-id="22625-166">Po przetworzeniu większej liczby wycinków w usłudze Azure Blob Storage będzie widocznych wiele kontenerów.</span><span class="sxs-lookup"><span data-stu-id="22625-166">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="22625-167">Jeśli nie są potrzebne do rozwiązywania problemów z zadaniami, można je usunąć, aby zmniejszyć koszt przechowywania.</span><span class="sxs-lookup"><span data-stu-id="22625-167">If you do not need them for troubleshooting of the jobs, you may want to delete them to reduce the storage cost.</span></span> <span data-ttu-id="22625-168">Nazwy tych kontenerów są zgodne ze wzorcem: „adf**twojanazwafabrykidanych**-**nazwapołączonejusługi**-znacznikdatygodziny”.</span><span class="sxs-lookup"><span data-stu-id="22625-168">The names of these containers follow a pattern: "adf**yourdatafactoryname**-**linkedservicename**-datetimestamp".</span></span> <span data-ttu-id="22625-169">Aby usunąć kontenery z usługi Azure Blob Storage, użyj takich narzędzi, jak [Microsoft Storage Explorer](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="22625-169">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) to delete containers in your Azure blob storage.</span></span>

<span data-ttu-id="22625-170">Szczegółowe informacje znajdują się w artykule [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) (Połączona usługa HDInsight na żądanie).</span><span class="sxs-lookup"><span data-stu-id="22625-170">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>

### <a name="inputdatasetjson"></a><span data-ttu-id="22625-171">inputdataset.json</span><span class="sxs-lookup"><span data-stu-id="22625-171">inputdataset.json</span></span>

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

<span data-ttu-id="22625-172">Ten kod JSON definiuje zestaw danych o nazwie **AzureBlobInput**, który reprezentuje dane wejściowe dla działania w potoku.</span><span class="sxs-lookup"><span data-stu-id="22625-172">The JSON defines a dataset named **AzureBlobInput**, which represents input data for an activity in the pipeline.</span></span> <span data-ttu-id="22625-173">Ponadto określa, że dane wejściowe znajdują się w kontenerze obiektów blob o nazwie **adfgetstarted** oraz w folderze o nazwie **inputdata**.</span><span class="sxs-lookup"><span data-stu-id="22625-173">In addition, it specifies that the input data is located in the blob container called **adfgetstarted** and the folder called **inputdata**.</span></span>

<span data-ttu-id="22625-174">Poniższa tabela zawiera opis właściwości kodu JSON użytych w tym fragmencie kodu:</span><span class="sxs-lookup"><span data-stu-id="22625-174">The following table provides descriptions for the JSON properties used in the snippet:</span></span>

| <span data-ttu-id="22625-175">Właściwość</span><span class="sxs-lookup"><span data-stu-id="22625-175">Property</span></span> | <span data-ttu-id="22625-176">Opis</span><span class="sxs-lookup"><span data-stu-id="22625-176">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="22625-177">type</span><span class="sxs-lookup"><span data-stu-id="22625-177">type</span></span> |<span data-ttu-id="22625-178">Właściwość type jest ustawiona na wartość AzureBlob, ponieważ dane znajdują się w magazynie obiektów blob Azure.</span><span class="sxs-lookup"><span data-stu-id="22625-178">The type property is set to AzureBlob because data resides in Azure blob storage.</span></span> |
| <span data-ttu-id="22625-179">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="22625-179">linkedServiceName</span></span> |<span data-ttu-id="22625-180">Odnosi się do elementu StorageLinkedService utworzonego wcześniej.</span><span class="sxs-lookup"><span data-stu-id="22625-180">refers to the StorageLinkedService you created earlier.</span></span> |
| <span data-ttu-id="22625-181">fileName</span><span class="sxs-lookup"><span data-stu-id="22625-181">fileName</span></span> |<span data-ttu-id="22625-182">Ta właściwość jest opcjonalna.</span><span class="sxs-lookup"><span data-stu-id="22625-182">This property is optional.</span></span> <span data-ttu-id="22625-183">Jeśli tę właściwość pominiesz, zostaną wybrane wszystkie pliki z folderu folderPath.</span><span class="sxs-lookup"><span data-stu-id="22625-183">If you omit this property, all the files from the folderPath are picked.</span></span> <span data-ttu-id="22625-184">W tym przypadku zostanie przetworzony tylko plik input.log.</span><span class="sxs-lookup"><span data-stu-id="22625-184">In this case, only the input.log is processed.</span></span> |
| <span data-ttu-id="22625-185">type</span><span class="sxs-lookup"><span data-stu-id="22625-185">type</span></span> |<span data-ttu-id="22625-186">Pliki dziennika są w formacie tekstowym, więc używana jest wartość TextFormat.</span><span class="sxs-lookup"><span data-stu-id="22625-186">The log files are in text format, so we use TextFormat.</span></span> |
| <span data-ttu-id="22625-187">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="22625-187">columnDelimiter</span></span> |<span data-ttu-id="22625-188">Kolumny w plikach dziennika są rozdzielane przecinkami (,)</span><span class="sxs-lookup"><span data-stu-id="22625-188">columns in the log files are delimited by a comma character (,)</span></span> |
| <span data-ttu-id="22625-189">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="22625-189">frequency/interval</span></span> |<span data-ttu-id="22625-190">Właściwość frequency (częstotliwość) jest ustawiona na wartość Month (Miesiąc), a wartość interwału wynosi 1, co oznacza, że wycinki wejściowe są dostępne co miesiąc.</span><span class="sxs-lookup"><span data-stu-id="22625-190">frequency set to Month and interval is 1, which means that the input slices are available monthly.</span></span> |
| <span data-ttu-id="22625-191">external</span><span class="sxs-lookup"><span data-stu-id="22625-191">external</span></span> |<span data-ttu-id="22625-192">Ta właściwość ma wartość true (prawda), jeśli dane wejściowe nie są generowane przez usługę Fabryka danych.</span><span class="sxs-lookup"><span data-stu-id="22625-192">this property is set to true if the input data is not generated by the Data Factory service.</span></span> |

### <a name="outputdatasetjson"></a><span data-ttu-id="22625-193">outputdataset.json</span><span class="sxs-lookup"><span data-stu-id="22625-193">outputdataset.json</span></span>

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

<span data-ttu-id="22625-194">Ten kod JSON definiuje zestaw danych o nazwie **AzureBlobOutput**, który reprezentuje dane wyjściowe dla działania w potoku.</span><span class="sxs-lookup"><span data-stu-id="22625-194">The JSON defines a dataset named **AzureBlobOutput**, which represents output data for an activity in the pipeline.</span></span> <span data-ttu-id="22625-195">Ponadto określa, że wyniki są przechowywane w kontenerze obiektów blob o nazwie **adfgetstarted** oraz folderze o nazwie **partitioneddata**.</span><span class="sxs-lookup"><span data-stu-id="22625-195">In addition, it specifies that the results are stored in the blob container called **adfgetstarted** and the folder called **partitioneddata**.</span></span> <span data-ttu-id="22625-196">W sekcji **availability** (dostępność) określono, że wyjściowy zestaw danych jest generowany co miesiąc.</span><span class="sxs-lookup"><span data-stu-id="22625-196">The **availability** section specifies that the output dataset is produced on a monthly basis.</span></span>

### <a name="pipelinejson"></a><span data-ttu-id="22625-197">pipeline.json</span><span class="sxs-lookup"><span data-stu-id="22625-197">pipeline.json</span></span>
> [!IMPORTANT]
> <span data-ttu-id="22625-198">Zastąp wartość **storageaccountname** nazwą konta usługi Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="22625-198">Replace **storageaccountname** with name of your Azure storage account.</span></span>
>
>

```JSON
{
    "name": "MyFirstPipeline",
    "properties": {
        "description": "My first Azure Data Factory pipeline",
        "activities": [{
            "type": "HDInsightHive",
            "typeProperties": {
                "scriptPath": "adfgetstarted/script/partitionweblogs.hql",
                "scriptLinkedService": "AzureStorageLinkedService",
                "defines": {
                    "inputtable": "wasb://adfgetstarted@<stroageaccountname>.blob.core.windows.net/inputdata",
                    "partitionedtable": "wasb://adfgetstarted@<stroageaccountname>t.blob.core.windows.net/partitioneddata"
                }
            },
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
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
        }],
        "start": "2017-07-10T00:00:00Z",
        "end": "2017-07-11T00:00:00Z",
        "isPaused": false
    }
}
```

<span data-ttu-id="22625-199">Ten fragment kodu JSON służy do utworzenia potoku obejmującego jedno działanie, które korzysta z programu Hive do przetwarzania danych w klastrze usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="22625-199">In the JSON snippet, you are creating a pipeline that consists of a single activity that uses Hive to process data on a HDInsight cluster.</span></span>

<span data-ttu-id="22625-200">Plik skryptu programu Hive **partitionweblogs.hql** jest przechowywany na koncie usługi Azure Storage (określonym za pomocą elementu scriptLinkedService o nazwie **StorageLinkedService**) oraz w folderze **script** w kontenerze **adfgetstarted**.</span><span class="sxs-lookup"><span data-stu-id="22625-200">The Hive script file, **partitionweblogs.hql**, is stored in the Azure storage account (specified by the scriptLinkedService, called **StorageLinkedService**), and in **script** folder in the container **adfgetstarted**.</span></span>

<span data-ttu-id="22625-201">Sekcja **defines** określa ustawienia środowiska uruchomieniowego, które są przekazywane do skryptu programu Hive w formie wartości konfiguracyjnych programu Hive (np. ${hiveconf:inputtable}, ${hiveconf:partitionedtable}).</span><span class="sxs-lookup"><span data-stu-id="22625-201">The **defines** section specifies runtime settings that are passed to the hive script as Hive configuration values (e.g ${hiveconf:inputtable}, ${hiveconf:partitionedtable}).</span></span>

<span data-ttu-id="22625-202">Właściwości **start** i **end** potoku określają aktywny okres potoku.</span><span class="sxs-lookup"><span data-stu-id="22625-202">The **start** and **end** properties of the pipeline specifies the active period of the pipeline.</span></span>

<span data-ttu-id="22625-203">W kodzie JSON dotyczącym działania określasz, że skrypt programu Hive jest uruchamiany w usłudze obliczeniowej określonej przez właściwość **linkedServiceName** — **HDInsightOnDemandLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="22625-203">In the activity JSON, you specify that the Hive script runs on the compute specified by the **linkedServiceName** – **HDInsightOnDemandLinkedService**.</span></span>

> [!NOTE]
> <span data-ttu-id="22625-204">Aby uzyskać szczegółowe informacje na temat właściwości kodu JSON używanych w poprzednim przykładzie, zobacz sekcję „Pipeline JSON” (Kod JSON potoku) w temacie [Pipelines and activities in Azure Data Factory](data-factory-create-pipelines.md) (Potoki i działania w usłudze Azure Data Factory).</span><span class="sxs-lookup"><span data-stu-id="22625-204">See "Pipeline JSON" in [Pipelines and activities in Azure Data Factory](data-factory-create-pipelines.md) for details about JSON properties used in the preceding example.</span></span>
>
>

## <a name="set-global-variables"></a><span data-ttu-id="22625-205">Ustawianie zmiennych globalnych</span><span class="sxs-lookup"><span data-stu-id="22625-205">Set global variables</span></span>
<span data-ttu-id="22625-206">Po zastąpieniu wartości własnymi wykonaj następujące polecenia w programie Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="22625-206">In Azure PowerShell, execute the following commands after replacing the values with your own:</span></span>

> [!IMPORTANT]
> <span data-ttu-id="22625-207">Zobacz sekcję [Wymagania wstępne](#prerequisites), aby uzyskać instrukcje dotyczące pobierania identyfikatora klienta, klucza tajnego klienta, identyfikatora dzierżawy oraz identyfikatora subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="22625-207">See [Prerequisites](#prerequisites) section for instructions on getting client ID, client secret, tenant ID, and subscription ID.</span></span>
>
>

```PowerShell
$client_id = "<client ID of application in AAD>"
$client_secret = "<client key of application in AAD>"
$tenant = "<Azure tenant ID>";
$subscription_id="<Azure subscription ID>";

$rg = "ADFTutorialResourceGroup"
$adf = "FirstDataFactoryREST"
```


## <a name="authenticate-with-aad"></a><span data-ttu-id="22625-208">Uwierzytelnianie przy użyciu usługi AAD</span><span class="sxs-lookup"><span data-stu-id="22625-208">Authenticate with AAD</span></span>

```PowerShell
$cmd = { .\curl.exe -X POST https://login.microsoftonline.com/$tenant/oauth2/token  -F grant_type=client_credentials  -F resource=https://management.core.windows.net/ -F client_id=$client_id -F client_secret=$client_secret };
$responseToken = Invoke-Command -scriptblock $cmd;
$accessToken = (ConvertFrom-Json $responseToken).access_token;

(ConvertFrom-Json $responseToken)
```


## <a name="create-data-factory"></a><span data-ttu-id="22625-209">Tworzenie fabryki danych</span><span class="sxs-lookup"><span data-stu-id="22625-209">Create data factory</span></span>
<span data-ttu-id="22625-210">W tym kroku opisano tworzenie fabryki danych Azure o nazwie **FirstDataFactoryREST**.</span><span class="sxs-lookup"><span data-stu-id="22625-210">In this step, you create an Azure Data Factory named **FirstDataFactoryREST**.</span></span> <span data-ttu-id="22625-211">Fabryka danych może obejmować jeden lub wiele potoków.</span><span class="sxs-lookup"><span data-stu-id="22625-211">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="22625-212">Potok może obejmować jedno lub wiele działań.</span><span class="sxs-lookup"><span data-stu-id="22625-212">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="22625-213">Na przykład działanie kopiowania może służyć do skopiowania danych ze źródła do docelowego magazynu danych, a działanie programu Hive w usłudze HDInsight do uruchomienia skryptu programu Hive, który przekształci dane.</span><span class="sxs-lookup"><span data-stu-id="22625-213">For example, a Copy Activity to copy data from a source to a destination data store and a HDInsight Hive activity to run a Hive script to transform data.</span></span> <span data-ttu-id="22625-214">Uruchom następujące polecenia, aby utworzyć fabrykę danych:</span><span class="sxs-lookup"><span data-stu-id="22625-214">Run the following commands to create the data factory:</span></span>

1. <span data-ttu-id="22625-215">Przypisz polecenie do zmiennej o nazwie **cmd**.</span><span class="sxs-lookup"><span data-stu-id="22625-215">Assign the command to variable named **cmd**.</span></span>

    <span data-ttu-id="22625-216">Upewnij się, że określona tutaj nazwa fabryki danych (ADFCopyTutorialDF) odpowiada nazwie podanej w pliku **datafactory.json**.</span><span class="sxs-lookup"><span data-stu-id="22625-216">Confirm that the name of the data factory you specify here (ADFCopyTutorialDF) matches the name specified in the **datafactory.json**.</span></span>

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data “@datafactory.json” https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/FirstDataFactoryREST?api-version=2015-10-01};
    ```
2. <span data-ttu-id="22625-217">Uruchom to polecenie przy użyciu polecenia **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="22625-217">Run the command by using **Invoke-Command**.</span></span>

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="22625-218">Przejrzyj wyniki.</span><span class="sxs-lookup"><span data-stu-id="22625-218">View the results.</span></span> <span data-ttu-id="22625-219">Jeśli fabryka danych została utworzona pomyślnie, w **wynikach** będzie widoczny kod JSON tej fabryki. W przeciwnym razie zostanie wyświetlony komunikat o błędzie.</span><span class="sxs-lookup"><span data-stu-id="22625-219">If the data factory has been successfully created, you see the JSON for the data factory in the **results**; otherwise, you see an error message.</span></span>

    ```PowerShell
    Write-Host $results
    ```

<span data-ttu-id="22625-220">Pamiętaj o następujących kwestiach:</span><span class="sxs-lookup"><span data-stu-id="22625-220">Note the following points:</span></span>

* <span data-ttu-id="22625-221">Nazwa fabryki danych Azure musi być globalnie unikatowa.</span><span class="sxs-lookup"><span data-stu-id="22625-221">The name of the Azure Data Factory must be globally unique.</span></span> <span data-ttu-id="22625-222">Jeśli w wynikach jest wyświetlany błąd: **Nazwa fabryki danych „FirstDataFactoryREST” jest niedostępna**, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="22625-222">If you see the error in results: **Data factory name “FirstDataFactoryREST” is not available**, do the following steps:</span></span>
  1. <span data-ttu-id="22625-223">Zmień nazwę fabryki (np. twojanazwaFirstDataFactoryREST) w pliku **datafactory.json**.</span><span class="sxs-lookup"><span data-stu-id="22625-223">Change the name (for example, yournameFirstDataFactoryREST) in the **datafactory.json** file.</span></span> <span data-ttu-id="22625-224">Artykuł [Data Factory — Naming Rules](data-factory-naming-rules.md) (Fabryka danych — zasady nazewnictwa) zawiera zasady nazewnictwa artefaktów usługi Fabryka danych.</span><span class="sxs-lookup"><span data-stu-id="22625-224">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>
  2. <span data-ttu-id="22625-225">W pierwszym poleceniu, w którym zmiennej **$cmd** jest przypisywana wartość, zastąp nazwę FirstDataFactoryREST nową nazwą i uruchom to polecenie.</span><span class="sxs-lookup"><span data-stu-id="22625-225">In the first command where the **$cmd** variable is assigned a value, replace FirstDataFactoryREST with the new name and run the command.</span></span>
  3. <span data-ttu-id="22625-226">Uruchom kolejne dwa polecenia, aby wywołać interfejs API REST w celu utworzenia fabryki danych i wyświetlić wyniki tej operacji.</span><span class="sxs-lookup"><span data-stu-id="22625-226">Run the next two commands to invoke the REST API to create the data factory and print the results of the operation.</span></span>
* <span data-ttu-id="22625-227">Aby tworzyć wystąpienia usługi Fabryka danych, musisz być współautorem/administratorem subskrypcji Azure</span><span class="sxs-lookup"><span data-stu-id="22625-227">To create Data Factory instances, you need to be a contributor/administrator of the Azure subscription</span></span>
* <span data-ttu-id="22625-228">W przyszłości nazwa fabryki danych może zostać zarejestrowana jako nazwa DNS, a wówczas stanie się widoczna publicznie.</span><span class="sxs-lookup"><span data-stu-id="22625-228">The name of the data factory may be registered as a DNS name in the future and hence become publicly visible.</span></span>
* <span data-ttu-id="22625-229">Jeśli zostanie wyświetlony komunikat o błędzie: „**Subskrypcja nie jest zarejestrowana w celu używania przestrzeni nazw Microsoft.DataFactory**”, wykonaj jedną z następujących czynności i spróbuj opublikować ponownie:</span><span class="sxs-lookup"><span data-stu-id="22625-229">If you receive the error: "**This subscription is not registered to use namespace Microsoft.DataFactory**", do one of the following and try publishing again:</span></span>

  * <span data-ttu-id="22625-230">W programie Azure PowerShell uruchom następujące polecenie, aby zarejestrować dostawcę usługi Data Factory:</span><span class="sxs-lookup"><span data-stu-id="22625-230">In Azure PowerShell, run the following command to register the Data Factory provider:</span></span>

    ```PowerShell
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```

      <span data-ttu-id="22625-231">Możesz uruchomić następujące polecenie, aby potwierdzić, że dostawca usługi Fabryka danych jest zarejestrowany:</span><span class="sxs-lookup"><span data-stu-id="22625-231">You can run the following command to confirm that the Data Factory provider is registered:</span></span>
    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * <span data-ttu-id="22625-232">Zaloguj się przy użyciu subskrypcji Azure do [portalu Azure](https://portal.azure.com) i przejdź do bloku Fabryka danych lub utwórz fabrykę danych w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="22625-232">Login using the Azure subscription into the [Azure portal](https://portal.azure.com) and navigate to a Data Factory blade (or) create a data factory in the Azure portal.</span></span> <span data-ttu-id="22625-233">Ta akcja powoduje automatyczne zarejestrowanie dostawcy.</span><span class="sxs-lookup"><span data-stu-id="22625-233">This action automatically registers the provider for you.</span></span>

<span data-ttu-id="22625-234">Przed utworzeniem potoku musisz utworzyć kilka jednostek usługi Fabryka danych.</span><span class="sxs-lookup"><span data-stu-id="22625-234">Before creating a pipeline, you need to create a few Data Factory entities first.</span></span> <span data-ttu-id="22625-235">Najpierw utwórz połączone usługi, aby połączyć usługi magazynu danych/usługi obliczeniowe ze swoim magazynem danych, oraz zdefiniuj wejściowe i wyjściowe zestawy danych do reprezentowania danych w połączonych magazynach danych.</span><span class="sxs-lookup"><span data-stu-id="22625-235">You first create linked services to link data stores/computes to your data store, define input and output datasets to represent data in linked data stores.</span></span>

## <a name="create-linked-services"></a><span data-ttu-id="22625-236">Tworzenie połączonych usług</span><span class="sxs-lookup"><span data-stu-id="22625-236">Create linked services</span></span>
<span data-ttu-id="22625-237">W tym kroku opisano połączenie konta usługi Azure Storage oraz klastra Azure HDInsight na żądanie z fabryką danych.</span><span class="sxs-lookup"><span data-stu-id="22625-237">In this step, you link your Azure Storage account and an on-demand Azure HDInsight cluster to your data factory.</span></span> <span data-ttu-id="22625-238">Konto usługi Azure Storage będzie przechowywać dane wejściowe i wyjściowe dla potoku w tym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="22625-238">The Azure Storage account holds the input and output data for the pipeline in this sample.</span></span> <span data-ttu-id="22625-239">Połączona usługa HDInsight służy do uruchamiania skryptu programu Hive określonego w działaniu potoku w tym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="22625-239">The HDInsight linked service is used to run a Hive script specified in the activity of the pipeline in this sample.</span></span>

### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="22625-240">Tworzenie połączonej usługi Azure Storage</span><span class="sxs-lookup"><span data-stu-id="22625-240">Create Azure Storage linked service</span></span>
<span data-ttu-id="22625-241">W tym kroku opisano łączenie konta usługi Azure Storage z fabryką danych.</span><span class="sxs-lookup"><span data-stu-id="22625-241">In this step, you link your Azure Storage account to your data factory.</span></span> <span data-ttu-id="22625-242">W tym samouczku do przechowywania danych wejściowych/wyjściowych oraz pliku skryptu HQL używa się tego samego konta usługi Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="22625-242">With this tutorial, you use the same Azure Storage account to store input/output data and the HQL script file.</span></span>

1. <span data-ttu-id="22625-243">Przypisz polecenie do zmiennej o nazwie **cmd**.</span><span class="sxs-lookup"><span data-stu-id="22625-243">Assign the command to variable named **cmd**.</span></span>

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data “@azurestoragelinkedservice.json” https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/linkedservices/AzureStorageLinkedService?api-version=2015-10-01};
    ```
2. <span data-ttu-id="22625-244">Uruchom to polecenie przy użyciu polecenia **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="22625-244">Run the command by using **Invoke-Command**.</span></span>

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="22625-245">Przejrzyj wyniki.</span><span class="sxs-lookup"><span data-stu-id="22625-245">View the results.</span></span> <span data-ttu-id="22625-246">Jeśli połączona usługa została utworzona pomyślnie, w **wynikach** będzie widoczny kod JSON tej usługi. W przeciwnym razie zostanie wyświetlony komunikat o błędzie.</span><span class="sxs-lookup"><span data-stu-id="22625-246">If the linked service has been successfully created, you see the JSON for the linked service in the **results**; otherwise, you see an error message.</span></span>

    ```PowerShell
    Write-Host $results
    ```

### <a name="create-azure-hdinsight-linked-service"></a><span data-ttu-id="22625-247">Tworzenie połączonej usługi Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="22625-247">Create Azure HDInsight linked service</span></span>
<span data-ttu-id="22625-248">W tym kroku przedstawiono łączenie klastra usługi HDInsight na żądanie z fabryką danych.</span><span class="sxs-lookup"><span data-stu-id="22625-248">In this step, you link an on-demand HDInsight cluster to your data factory.</span></span> <span data-ttu-id="22625-249">Klaster usługi HDInsight jest automatycznie tworzony w czasie wykonywania oraz usuwany po zakończeniu przetwarzania i określonym czasie bezczynności.</span><span class="sxs-lookup"><span data-stu-id="22625-249">The HDInsight cluster is automatically created at runtime and deleted after it is done processing and idle for the specified amount of time.</span></span> <span data-ttu-id="22625-250">Możesz użyć własnego klastra usługi HDInsight zamiast klastra usługi HDInsight na żądanie.</span><span class="sxs-lookup"><span data-stu-id="22625-250">You could use your own HDInsight cluster instead of using an on-demand HDInsight cluster.</span></span> <span data-ttu-id="22625-251">Szczegółowe informacje znajdują się w artykule [Compute Linked Services](data-factory-compute-linked-services.md) (Połączone usługi obliczeniowe).</span><span class="sxs-lookup"><span data-stu-id="22625-251">See [Compute Linked Services](data-factory-compute-linked-services.md) for details.</span></span>

1. <span data-ttu-id="22625-252">Przypisz polecenie do zmiennej o nazwie **cmd**.</span><span class="sxs-lookup"><span data-stu-id="22625-252">Assign the command to variable named **cmd**.</span></span>

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@hdinsightondemandlinkedservice.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/linkedservices/hdinsightondemandlinkedservice?api-version=2015-10-01};
    ```
2. <span data-ttu-id="22625-253">Uruchom to polecenie przy użyciu polecenia **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="22625-253">Run the command by using **Invoke-Command**.</span></span>

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="22625-254">Przejrzyj wyniki.</span><span class="sxs-lookup"><span data-stu-id="22625-254">View the results.</span></span> <span data-ttu-id="22625-255">Jeśli połączona usługa została utworzona pomyślnie, w **wynikach** będzie widoczny kod JSON tej usługi. W przeciwnym razie zostanie wyświetlony komunikat o błędzie.</span><span class="sxs-lookup"><span data-stu-id="22625-255">If the linked service has been successfully created, you see the JSON for the linked service in the **results**; otherwise, you see an error message.</span></span>

    ```PowerShell
    Write-Host $results
    ```

## <a name="create-datasets"></a><span data-ttu-id="22625-256">Tworzenie zestawów danych</span><span class="sxs-lookup"><span data-stu-id="22625-256">Create datasets</span></span>
<span data-ttu-id="22625-257">W tym kroku opisano tworzenie zestawów danych do reprezentowania danych wejściowych i wyjściowych na potrzeby przetwarzania przy użyciu programu Hive.</span><span class="sxs-lookup"><span data-stu-id="22625-257">In this step, you create datasets to represent the input and output data for Hive processing.</span></span> <span data-ttu-id="22625-258">Te zestawy danych dotyczą elementu **StorageLinkedService** utworzonego wcześniej w ramach tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="22625-258">These datasets refer to the **StorageLinkedService** you have created earlier in this tutorial.</span></span> <span data-ttu-id="22625-259">Połączona usługa wskazuje konto usługi Azure Storage, a zestawy danych określają kontener, folder i nazwę pliku w magazynie, w którym przechowywane są dane wejściowe i wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="22625-259">The linked service points to an Azure Storage account and datasets specify container, folder, file name in the storage that holds input and output data.</span></span>

### <a name="create-input-dataset"></a><span data-ttu-id="22625-260">Tworzenie wejściowego zestawu danych</span><span class="sxs-lookup"><span data-stu-id="22625-260">Create input dataset</span></span>
<span data-ttu-id="22625-261">W tym kroku opisano tworzenie wejściowego zestawu danych do reprezentowania danych wejściowych przechowywanych w usłudze Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="22625-261">In this step, you create the input dataset to represent input data stored in the Azure Blob storage.</span></span>

1. <span data-ttu-id="22625-262">Przypisz polecenie do zmiennej o nazwie **cmd**.</span><span class="sxs-lookup"><span data-stu-id="22625-262">Assign the command to variable named **cmd**.</span></span>

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@inputdataset.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/AzureBlobInput?api-version=2015-10-01};
    ```
2. <span data-ttu-id="22625-263">Uruchom to polecenie przy użyciu polecenia **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="22625-263">Run the command by using **Invoke-Command**.</span></span>

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="22625-264">Przejrzyj wyniki.</span><span class="sxs-lookup"><span data-stu-id="22625-264">View the results.</span></span> <span data-ttu-id="22625-265">Jeśli zestaw danych został utworzony pomyślnie, w **wynikach** będzie widoczny kod JSON tego zestawu. W przeciwnym razie zostanie wyświetlony komunikat o błędzie.</span><span class="sxs-lookup"><span data-stu-id="22625-265">If the dataset has been successfully created, you see the JSON for the dataset in the **results**; otherwise, you see an error message.</span></span>

    ```PowerShell
    Write-Host $results
    ```

### <a name="create-output-dataset"></a><span data-ttu-id="22625-266">Tworzenie wyjściowego zestawu danych</span><span class="sxs-lookup"><span data-stu-id="22625-266">Create output dataset</span></span>
<span data-ttu-id="22625-267">W tym kroku opisano tworzenie wyjściowego zestawu danych do reprezentowania danych wyjściowych przechowywanych w usłudze Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="22625-267">In this step, you create the output dataset to represent output data stored in the Azure Blob storage.</span></span>

1. <span data-ttu-id="22625-268">Przypisz polecenie do zmiennej o nazwie **cmd**.</span><span class="sxs-lookup"><span data-stu-id="22625-268">Assign the command to variable named **cmd**.</span></span>

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@outputdataset.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/AzureBlobOutput?api-version=2015-10-01};
    ```
2. <span data-ttu-id="22625-269">Uruchom to polecenie przy użyciu polecenia **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="22625-269">Run the command by using **Invoke-Command**.</span></span>

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="22625-270">Przejrzyj wyniki.</span><span class="sxs-lookup"><span data-stu-id="22625-270">View the results.</span></span> <span data-ttu-id="22625-271">Jeśli zestaw danych został utworzony pomyślnie, w **wynikach** będzie widoczny kod JSON tego zestawu. W przeciwnym razie zostanie wyświetlony komunikat o błędzie.</span><span class="sxs-lookup"><span data-stu-id="22625-271">If the dataset has been successfully created, you see the JSON for the dataset in the **results**; otherwise, you see an error message.</span></span>

    ```PowerShell
    Write-Host $results
    ```

## <a name="create-pipeline"></a><span data-ttu-id="22625-272">Tworzenie potoku</span><span class="sxs-lookup"><span data-stu-id="22625-272">Create pipeline</span></span>
<span data-ttu-id="22625-273">W tym kroku opisano tworzenie pierwszego potoku za pomocą działania **HDInsightHive**.</span><span class="sxs-lookup"><span data-stu-id="22625-273">In this step, you create your first pipeline with a **HDInsightHive** activity.</span></span> <span data-ttu-id="22625-274">Wycinek danych wejściowych jest dostępny co miesiąc (frequency: Month, interval: 1), wycinek danych wyjściowych jest generowany co miesiąc, a właściwość scheduler dla działania jest również ustawiona na wartość miesięczną.</span><span class="sxs-lookup"><span data-stu-id="22625-274">Input slice is available monthly (frequency: Month, interval: 1), output slice is produced monthly, and the scheduler property for the activity is also set to monthly.</span></span> <span data-ttu-id="22625-275">Ustawienia dla wyjściowego zestawu danych i harmonogramu działania muszą być zgodne.</span><span class="sxs-lookup"><span data-stu-id="22625-275">The settings for the output dataset and the activity scheduler must match.</span></span> <span data-ttu-id="22625-276">W tym przypadku wyjściowy zestaw danych jest elementem wpływającym na ustawienia harmonogramu, więc musisz utworzyć wyjściowy zestaw danych nawet wtedy, gdy działanie nie generuje żadnych danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="22625-276">Currently, output dataset is what drives the schedule, so you must create an output dataset even if the activity does not produce any output.</span></span> <span data-ttu-id="22625-277">Jeśli w działaniu nie są używane żadne dane wejściowe, możesz pominąć tworzenie zestawu danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="22625-277">If the activity doesn't take any input, you can skip creating the input dataset.</span></span>

<span data-ttu-id="22625-278">Upewnij się, że plik **input.log** jest wyświetlany w folderze **adfgetstarted/inputdata** w magazynie obiektów blob Azure, i uruchom następujące polecenie, aby wdrożyć potok.</span><span class="sxs-lookup"><span data-stu-id="22625-278">Confirm that you see the **input.log** file in the **adfgetstarted/inputdata** folder in the Azure blob storage, and run the following command to deploy the pipeline.</span></span> <span data-ttu-id="22625-279">Ponieważ właściwości **start** i **end** są ustawione na wartość w przeszłości i właściwość **isPaused** została ustawiona na wartość „false”, potok (działanie w potoku) jest uruchamiany natychmiast po wdrożeniu.</span><span class="sxs-lookup"><span data-stu-id="22625-279">Since the **start** and **end** times are set in the past and **isPaused** is set to false, the pipeline (activity in the pipeline) runs immediately after you deploy.</span></span>

1. <span data-ttu-id="22625-280">Przypisz polecenie do zmiennej o nazwie **cmd**.</span><span class="sxs-lookup"><span data-stu-id="22625-280">Assign the command to variable named **cmd**.</span></span>

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@pipeline.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datapipelines/MyFirstPipeline?api-version=2015-10-01};
    ```
2. <span data-ttu-id="22625-281">Uruchom to polecenie przy użyciu polecenia **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="22625-281">Run the command by using **Invoke-Command**.</span></span>

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="22625-282">Przejrzyj wyniki.</span><span class="sxs-lookup"><span data-stu-id="22625-282">View the results.</span></span> <span data-ttu-id="22625-283">Jeśli zestaw danych został utworzony pomyślnie, w **wynikach** będzie widoczny kod JSON tego zestawu. W przeciwnym razie zostanie wyświetlony komunikat o błędzie.</span><span class="sxs-lookup"><span data-stu-id="22625-283">If the dataset has been successfully created, you see the JSON for the dataset in the **results**; otherwise, you see an error message.</span></span>

    ```PowerShell
    Write-Host $results
    ```
4. <span data-ttu-id="22625-284">Gratulacje! Udało Ci się utworzyć pierwszy potok przy użyciu programu Azure PowerShell!</span><span class="sxs-lookup"><span data-stu-id="22625-284">Congratulations, you have successfully created your first pipeline using Azure PowerShell!</span></span>

## <a name="monitor-pipeline"></a><span data-ttu-id="22625-285">Monitorowanie potoku</span><span class="sxs-lookup"><span data-stu-id="22625-285">Monitor pipeline</span></span>
<span data-ttu-id="22625-286">W tym kroku interfejs API REST usługi Data Factory służy do monitorowania wycinków generowanych przez potok.</span><span class="sxs-lookup"><span data-stu-id="22625-286">In this step, you use Data Factory REST API to monitor slices being produced by the pipeline.</span></span>

```PowerShell
$ds ="AzureBlobOutput"

$cmd = {.\curl.exe -X GET -H "Authorization: Bearer $accessToken" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/$ds/slices?start=1970-01-01T00%3a00%3a00.0000000Z"&"end=2016-08-12T00%3a00%3a00.0000000Z"&"api-version=2015-10-01};

$results2 = Invoke-Command -scriptblock $cmd;

IF ((ConvertFrom-Json $results2).value -ne $NULL) {
    ConvertFrom-Json $results2 | Select-Object -Expand value | Format-Table
} else {
        (convertFrom-Json $results2).RemoteException
}
```

> [!IMPORTANT]
> <span data-ttu-id="22625-287">Tworzenie klastra usługi HDInsight na żądanie zwykle trwa trochę czasu (około 20 minut).</span><span class="sxs-lookup"><span data-stu-id="22625-287">Creation of an on-demand HDInsight cluster usually takes sometime (approximately 20 minutes).</span></span> <span data-ttu-id="22625-288">Dlatego należy oczekiwać, że przetworzenie wycinka przez potok zajmie **około 30 minut**.</span><span class="sxs-lookup"><span data-stu-id="22625-288">Therefore, expect the pipeline to take **approximately 30 minutes** to process the slice.</span></span>
>
>

<span data-ttu-id="22625-289">Uruchom polecenie Invoke-Command i kolejne polecenie, aż zobaczysz, że wycinek jest w stanie **Gotowe** lub **Niepowodzenie**.</span><span class="sxs-lookup"><span data-stu-id="22625-289">Run the Invoke-Command and the next one until you see the slice in **Ready** state or **Failed** state.</span></span> <span data-ttu-id="22625-290">Gdy wycinek będzie w stanie Gotowe, sprawdź folder **partitioneddata** w kontenerze **adfgetstarted** w magazynie obiektów blob pod kątem danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="22625-290">When the slice is in Ready state, check the **partitioneddata** folder in the **adfgetstarted** container in your blob storage for the output data.</span></span>  <span data-ttu-id="22625-291">Tworzenie klastra usługi HDInsight na żądanie zwykle zajmuje trochę czasu.</span><span class="sxs-lookup"><span data-stu-id="22625-291">The creation of an on-demand HDInsight cluster usually takes some time.</span></span>

![Dane wyjściowe](./media/data-factory-build-your-first-pipeline-using-rest-api/three-ouptut-files.png)

> [!IMPORTANT]
> <span data-ttu-id="22625-293">Po pomyślnym przetworzeniu wycinka plik wejściowy zostanie usunięty.</span><span class="sxs-lookup"><span data-stu-id="22625-293">The input file gets deleted when the slice is processed successfully.</span></span> <span data-ttu-id="22625-294">Tak więc, jeśli chcesz ponownie uruchomić wycinek lub ponownie wykonać instrukcje z tego samouczka, przekaż plik wejściowy (input.log) do folderu inputdata kontenera adfgetstarted.</span><span class="sxs-lookup"><span data-stu-id="22625-294">Therefore, if you want to rerun the slice or do the tutorial again, upload the input file (input.log) to the inputdata folder of the adfgetstarted container.</span></span>
>
>

<span data-ttu-id="22625-295">Monitorowanie wycinków i rozwiązywanie problemów jest również możliwe za pośrednictwem witryny Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="22625-295">You can also use Azure portal to monitor slices and troubleshoot any issues.</span></span> <span data-ttu-id="22625-296">Aby poznać szczegóły, zapoznaj się z informacjami dotyczącymi [monitorowania potoków w witrynie Azure Portal](data-factory-build-your-first-pipeline-using-editor.md#monitor-pipeline).</span><span class="sxs-lookup"><span data-stu-id="22625-296">See [Monitor pipelines using Azure portal](data-factory-build-your-first-pipeline-using-editor.md#monitor-pipeline) details.</span></span>

## <a name="summary"></a><span data-ttu-id="22625-297">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="22625-297">Summary</span></span>
<span data-ttu-id="22625-298">W tym samouczku opisano tworzenie fabryki danych Azure do przetwarzania danych przez uruchomienie skryptu programu Hive w klastrze platformy Hadoop w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="22625-298">In this tutorial, you created an Azure data factory to process data by running Hive script on a HDInsight hadoop cluster.</span></span> <span data-ttu-id="22625-299">Użyto Edytora fabryki danych w witrynie Azure Portal, aby:</span><span class="sxs-lookup"><span data-stu-id="22625-299">You used the Data Factory Editor in the Azure portal to do the following steps:</span></span>

1. <span data-ttu-id="22625-300">Tworzenie **fabryki danych** Azure.</span><span class="sxs-lookup"><span data-stu-id="22625-300">Created an Azure **data factory**.</span></span>
2. <span data-ttu-id="22625-301">Utworzyć dwie **połączone usługi**:</span><span class="sxs-lookup"><span data-stu-id="22625-301">Created two **linked services**:</span></span>
   1. <span data-ttu-id="22625-302">Połączoną usługę **Azure Storage** w celu połączenia magazynu obiektów blob Azure, w którym przechowywane są pliki wejściowe/wyjściowe, z fabryką danych.</span><span class="sxs-lookup"><span data-stu-id="22625-302">**Azure Storage** linked service to link your Azure blob storage that holds input/output files to the data factory.</span></span>
   2. <span data-ttu-id="22625-303">Połączoną usługę **Azure HDInsight** na żądanie w celu połączenia klastra platformy Hadoop w usłudze HDInsight na żądanie z fabryką danych.</span><span class="sxs-lookup"><span data-stu-id="22625-303">**Azure HDInsight** on-demand linked service to link an on-demand HDInsight Hadoop cluster to the data factory.</span></span> <span data-ttu-id="22625-304">Usługa Fabryka danych Azure tworzy klaster just in time platformy Hadoop w usłudze HDInsight, aby przetwarzać dane wejściowe i generować dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="22625-304">Azure Data Factory creates a HDInsight Hadoop cluster just-in-time to process input data and produce output data.</span></span>
3. <span data-ttu-id="22625-305">Utworzyć dwa **zestawy danych** zawierające dane wejściowe i wyjściowe dla działania programu Hive w usłudze HDInsight w potoku.</span><span class="sxs-lookup"><span data-stu-id="22625-305">Created two **datasets**, which describe input and output data for HDInsight Hive activity in the pipeline.</span></span>
4. <span data-ttu-id="22625-306">Utworzyć **potok** za pomocą działania **programu Hive w usłudze HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="22625-306">Created a **pipeline** with a **HDInsight Hive** activity.</span></span>

## <a name="next-steps"></a><span data-ttu-id="22625-307">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="22625-307">Next steps</span></span>
<span data-ttu-id="22625-308">W tym artykule opisano tworzenie potoku za pomocą działania przekształcania (działanie usługi HDInsight), które uruchamia skrypt programu Hive w klastrze usługi HDInsight platformy Azure na żądanie.</span><span class="sxs-lookup"><span data-stu-id="22625-308">In this article, you have created a pipeline with a transformation activity (HDInsight Activity) that runs a Hive script on an on-demand Azure HDInsight cluster.</span></span> <span data-ttu-id="22625-309">Instrukcje dotyczące korzystania z działania kopiowania w celu kopiowania danych z magazynu obiektów blob Azure do usług SQL Azure znajdują się w artykule [Tutorial: Copy data from an Azure Blob to Azure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) (Samouczek: kopiowanie danych z magazynu obiektów blob Azure do usług SQL Azure).</span><span class="sxs-lookup"><span data-stu-id="22625-309">To see how to use a Copy Activity to copy data from an Azure Blob to Azure SQL, see [Tutorial: Copy data from an Azure Blob to Azure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="22625-310">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="22625-310">See Also</span></span>
| <span data-ttu-id="22625-311">Temat</span><span class="sxs-lookup"><span data-stu-id="22625-311">Topic</span></span> | <span data-ttu-id="22625-312">Opis</span><span class="sxs-lookup"><span data-stu-id="22625-312">Description</span></span> |
|:--- |:--- |
| [<span data-ttu-id="22625-313">Dokumentacja interfejsu API REST usługi Data Factory</span><span class="sxs-lookup"><span data-stu-id="22625-313">Data Factory REST API Reference</span></span>](/rest/api/datafactory/) |<span data-ttu-id="22625-314">Zobacz pełną dokumentację dotyczącą poleceń cmdlet w usłudze Fabryka danych.</span><span class="sxs-lookup"><span data-stu-id="22625-314">See comprehensive documentation on Data Factory cmdlets</span></span> |
| [<span data-ttu-id="22625-315">Potoki</span><span class="sxs-lookup"><span data-stu-id="22625-315">Pipelines</span></span>](data-factory-create-pipelines.md) |<span data-ttu-id="22625-316">Ten artykuł ułatwia zapoznanie się z potokami i działaniami w usłudze Azure Data Factory oraz ze sposobem konstruowania za ich pomocą przepływów pracy typu end-to-end opartych na danych na potrzeby scenariusza lub firmy.</span><span class="sxs-lookup"><span data-stu-id="22625-316">This article helps you understand pipelines and activities in Azure Data Factory and how to use them to construct end-to-end data-driven workflows for your scenario or business.</span></span> |
| [<span data-ttu-id="22625-317">Zestawy danych</span><span class="sxs-lookup"><span data-stu-id="22625-317">Datasets</span></span>](data-factory-create-datasets.md) |<span data-ttu-id="22625-318">Ten artykuł ułatwia zapoznanie się z zestawami danych w usłudze Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="22625-318">This article helps you understand datasets in Azure Data Factory.</span></span> |
| [<span data-ttu-id="22625-319">Planowanie i wykonywanie</span><span class="sxs-lookup"><span data-stu-id="22625-319">Scheduling and Execution</span></span>](data-factory-scheduling-and-execution.md) |<span data-ttu-id="22625-320">W tym artykule wyjaśniono aspekty planowania i wykonywania modelu aplikacji usługi Fabryka danych Azure.</span><span class="sxs-lookup"><span data-stu-id="22625-320">This article explains the scheduling and execution aspects of Azure Data Factory application model.</span></span> |
| [<span data-ttu-id="22625-321">Monitorowanie potoków i zarządzanie nimi za pomocą aplikacji do monitorowania</span><span class="sxs-lookup"><span data-stu-id="22625-321">Monitor and manage pipelines using Monitoring App</span></span>](data-factory-monitor-manage-app.md) |<span data-ttu-id="22625-322">Ten artykuł zawiera instrukcje dotyczące monitorowania i debugowania potoków oraz zarządzania nimi przy użyciu aplikacji do monitorowania i zarządzania.</span><span class="sxs-lookup"><span data-stu-id="22625-322">This article describes how to monitor, manage, and debug pipelines using the Monitoring & Management App.</span></span> |
