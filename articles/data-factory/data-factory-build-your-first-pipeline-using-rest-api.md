---
title: aaaBuild pierwszy fabryki danych (REST) | Dokumentacja firmy Microsoft
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
ms.openlocfilehash: 5d8e39bd598cca35f91d501bad74e8a8436f8f89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-build-your-first-azure-data-factory-using-data-factory-rest-api"></a><span data-ttu-id="c80c9-103">Samouczek: Tworzenie pierwszej fabryki danych Azure przy użyciu interfejsu API REST usługi Fabryka danych</span><span class="sxs-lookup"><span data-stu-id="c80c9-103">Tutorial: Build your first Azure data factory using Data Factory REST API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c80c9-104">Przegląd i wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="c80c9-104">Overview and prerequisites</span></span>](data-factory-build-your-first-pipeline.md)
> * [<span data-ttu-id="c80c9-105">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="c80c9-105">Azure portal</span></span>](data-factory-build-your-first-pipeline-using-editor.md)
> * [<span data-ttu-id="c80c9-106">Program Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c80c9-106">Visual Studio</span></span>](data-factory-build-your-first-pipeline-using-vs.md)
> * [<span data-ttu-id="c80c9-107">Program PowerShell</span><span class="sxs-lookup"><span data-stu-id="c80c9-107">PowerShell</span></span>](data-factory-build-your-first-pipeline-using-powershell.md)
> * [<span data-ttu-id="c80c9-108">Szablon usługi Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c80c9-108">Resource Manager Template</span></span>](data-factory-build-your-first-pipeline-using-arm.md)
> * [<span data-ttu-id="c80c9-109">Interfejs API REST</span><span class="sxs-lookup"><span data-stu-id="c80c9-109">REST API</span></span>](data-factory-build-your-first-pipeline-using-rest-api.md)
>
>


<span data-ttu-id="c80c9-110">W tym artykule Użyj interfejsu API REST fabryki danych toocreate Twojego pierwszego fabryki danych Azure.</span><span class="sxs-lookup"><span data-stu-id="c80c9-110">In this article, you use Data Factory REST API toocreate your first Azure data factory.</span></span> <span data-ttu-id="c80c9-111">Samouczek hello toodo przy użyciu innych narzędzi/SDK, wybierz jedną z opcji hello z listy rozwijanej hello.</span><span class="sxs-lookup"><span data-stu-id="c80c9-111">toodo hello tutorial using other tools/SDKs, select one of hello options from hello drop-down list.</span></span>

<span data-ttu-id="c80c9-112">Witaj potoku, w tym samouczku ma jedno działanie: **działania HDInsight Hive**.</span><span class="sxs-lookup"><span data-stu-id="c80c9-112">hello pipeline in this tutorial has one activity: **HDInsight Hive activity**.</span></span> <span data-ttu-id="c80c9-113">To działanie uruchamia skrypt hive w klastrze Azure HDInsight czy transformacji wejściowych danych wyjściowych tooproduce danych.</span><span class="sxs-lookup"><span data-stu-id="c80c9-113">This activity runs a hive script on an Azure HDInsight cluster that transforms input data tooproduce output data.</span></span> <span data-ttu-id="c80c9-114">potok Hello jest zaplanowane toorun po miesiącu między hello określono godziny rozpoczęcia i zakończenia.</span><span class="sxs-lookup"><span data-stu-id="c80c9-114">hello pipeline is scheduled toorun once a month between hello specified start and end times.</span></span>

> [!NOTE]
> <span data-ttu-id="c80c9-115">W tym artykule nie opisano wszystkich hello interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="c80c9-115">This article does not cover all hello REST API.</span></span> <span data-ttu-id="c80c9-116">Pełna dokumentacja dotycząca interfejsu API REST znajduje się w [Dokumentacji interfejsu API REST usługi Data Factory](/rest/api/datafactory/).</span><span class="sxs-lookup"><span data-stu-id="c80c9-116">For comprehensive documentation on REST API, see [Data Factory REST API Reference](/rest/api/datafactory/).</span></span>
> 
> <span data-ttu-id="c80c9-117">Potok może obejmować więcej niż jedno działanie.</span><span class="sxs-lookup"><span data-stu-id="c80c9-117">A pipeline can have more than one activity.</span></span> <span data-ttu-id="c80c9-118">I tworzenia łańcucha dwa działania (Uruchom jedno działanie po drugim), ustawiając hello wyjściowy zestaw danych z jednego działania jako hello wejściowy zestaw danych z hello innych działań.</span><span class="sxs-lookup"><span data-stu-id="c80c9-118">And, you can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="c80c9-119">Więcej informacji znajduje się w artykule dotyczącym [planowania i wykonywania w usłudze Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span><span class="sxs-lookup"><span data-stu-id="c80c9-119">For more information, see [scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="c80c9-120">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="c80c9-120">Prerequisites</span></span>
* <span data-ttu-id="c80c9-121">Zapoznaj się z artykułem [— samouczek Przegląd](data-factory-build-your-first-pipeline.md) artykułu i pełne hello **wymagań wstępnych** czynności.</span><span class="sxs-lookup"><span data-stu-id="c80c9-121">Read through [Tutorial Overview](data-factory-build-your-first-pipeline.md) article and complete hello **prerequisite** steps.</span></span>
* <span data-ttu-id="c80c9-122">Zainstaluj na komputerze narzędzie [Curl](https://curl.haxx.se/dlwiz/).</span><span class="sxs-lookup"><span data-stu-id="c80c9-122">Install [Curl](https://curl.haxx.se/dlwiz/) on your machine.</span></span> <span data-ttu-id="c80c9-123">Narzędzie CURL hello jest używany z toocreate polecenia REST fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="c80c9-123">You use hello CURL tool with REST commands toocreate a data factory.</span></span>
* <span data-ttu-id="c80c9-124">Postępuj zgodnie z instrukcjami zawartymi w [tym artykule](../azure-resource-manager/resource-group-create-service-principal-portal.md), aby wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="c80c9-124">Follow instructions from [this article](../azure-resource-manager/resource-group-create-service-principal-portal.md) to:</span></span>
  1. <span data-ttu-id="c80c9-125">Utworzenie aplikacji sieci Web o nazwie **ADFGetStartedApp** w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c80c9-125">Create a Web application named **ADFGetStartedApp** in Azure Active Directory.</span></span>
  2. <span data-ttu-id="c80c9-126">Pobranie **identyfikatora klienta** i **klucza tajnego**.</span><span class="sxs-lookup"><span data-stu-id="c80c9-126">Get **client ID** and **secret key**.</span></span>
  3. <span data-ttu-id="c80c9-127">Uzyskanie **identyfikatora dzierżawy**.</span><span class="sxs-lookup"><span data-stu-id="c80c9-127">Get **tenant ID**.</span></span>
  4. <span data-ttu-id="c80c9-128">Przypisz hello **ADFGetStartedApp** toohello aplikacji **współautora fabryki danych** roli.</span><span class="sxs-lookup"><span data-stu-id="c80c9-128">Assign hello **ADFGetStartedApp** application toohello **Data Factory Contributor** role.</span></span>
* <span data-ttu-id="c80c9-129">Zainstaluj program [Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c80c9-129">Install [Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="c80c9-130">Uruchom **PowerShell** i hello uruchom następujące polecenie.</span><span class="sxs-lookup"><span data-stu-id="c80c9-130">Launch **PowerShell** and run hello following command.</span></span> <span data-ttu-id="c80c9-131">Nie zamykaj programu Azure PowerShell do momentu zakończenia hello tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="c80c9-131">Keep Azure PowerShell open until hello end of this tutorial.</span></span> <span data-ttu-id="c80c9-132">Zamknij i otwórz ponownie, należy najpierw polecenia hello toorun ponownie.</span><span class="sxs-lookup"><span data-stu-id="c80c9-132">If you close and reopen, you need toorun hello commands again.</span></span>
  1. <span data-ttu-id="c80c9-133">Uruchom **Login-AzureRmAccount** , a następnie wprowadź hello nazwy użytkownika i hasła, użyj toosign w toohello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="c80c9-133">Run **Login-AzureRmAccount** and enter hello user name and password that you use toosign in toohello Azure portal.</span></span>
  2. <span data-ttu-id="c80c9-134">Uruchom **Get-AzureRmSubscription** tooview hello wszystkie subskrypcje dla tego konta.</span><span class="sxs-lookup"><span data-stu-id="c80c9-134">Run **Get-AzureRmSubscription** tooview all hello subscriptions for this account.</span></span>
  3. <span data-ttu-id="c80c9-135">Uruchom **NameOfAzureSubscription Nazwa subskrypcji - Get-AzureRmSubscription | Set-AzureRmContext** tooselect hello subskrypcji, która ma toowork z.</span><span class="sxs-lookup"><span data-stu-id="c80c9-135">Run **Get-AzureRmSubscription -SubscriptionName NameOfAzureSubscription | Set-AzureRmContext** tooselect hello subscription that you want toowork with.</span></span> <span data-ttu-id="c80c9-136">Zastąp **NameOfAzureSubscription** o nazwie hello subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c80c9-136">Replace **NameOfAzureSubscription** with hello name of your Azure subscription.</span></span>
* <span data-ttu-id="c80c9-137">Tworzenie grupy zasobów platformy Azure o nazwie **ADFTutorialResourceGroup** , uruchamiając następujące polecenie w środowiska PowerShell hello hello:</span><span class="sxs-lookup"><span data-stu-id="c80c9-137">Create an Azure resource group named **ADFTutorialResourceGroup** by running hello following command in hello PowerShell:</span></span>

    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```

   <span data-ttu-id="c80c9-138">Niektóre kroki hello w tym samouczku Załóżmy, że hello grupy zasobów o nazwie ADFTutorialResourceGroup.</span><span class="sxs-lookup"><span data-stu-id="c80c9-138">Some of hello steps in this tutorial assume that you use hello resource group named ADFTutorialResourceGroup.</span></span> <span data-ttu-id="c80c9-139">Jeśli używasz innej grupie zasobów, należy toouse hello Nazwa grupy zasobów, zamiast ADFTutorialResourceGroup w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="c80c9-139">If you use a different resource group, you need toouse hello name of your resource group in place of ADFTutorialResourceGroup in this tutorial.</span></span>

## <a name="create-json-definitions"></a><span data-ttu-id="c80c9-140">Tworzenie definicji JSON</span><span class="sxs-lookup"><span data-stu-id="c80c9-140">Create JSON definitions</span></span>
<span data-ttu-id="c80c9-141">Utwórz następujące pliki w folderze hello, w którym znajduje się curl.exe w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="c80c9-141">Create following JSON files in hello folder where curl.exe is located.</span></span>

### <a name="datafactoryjson"></a><span data-ttu-id="c80c9-142">datafactory.json</span><span class="sxs-lookup"><span data-stu-id="c80c9-142">datafactory.json</span></span>
> [!IMPORTANT]
> <span data-ttu-id="c80c9-143">Nazwa musi być unikatowe globalnie, dlatego może być toomake ADFCopyTutorialDF tooprefix/sufiksu go unikatową nazwę.</span><span class="sxs-lookup"><span data-stu-id="c80c9-143">Name must be globally unique, so you may want tooprefix/suffix ADFCopyTutorialDF toomake it a unique name.</span></span>
>
>

```JSON
{
    "name": "FirstDataFactoryREST",
    "location": "WestUS"
}
```

### <a name="azurestoragelinkedservicejson"></a><span data-ttu-id="c80c9-144">azurestoragelinkedservice.json</span><span class="sxs-lookup"><span data-stu-id="c80c9-144">azurestoragelinkedservice.json</span></span>
> [!IMPORTANT]
> <span data-ttu-id="c80c9-145">Zastąp wartości **accountname** i **accountkey** nazwą konta usługi Azure Storage oraz jego kluczem.</span><span class="sxs-lookup"><span data-stu-id="c80c9-145">Replace **accountname** and **accountkey** with name and key of your Azure storage account.</span></span> <span data-ttu-id="c80c9-146">toolearn sposób dostępu do magazynu tooget klucza, zobacz hello informacji na temat sposobu tooview, kopiowania i regenerate magazynu dostępu do kluczy w [Zarządzanie kontem magazynu](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="c80c9-146">toolearn how tooget your storage access key, see hello information about how tooview, copy, and regenerate storage access keys in [Manage your storage account](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>
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

### <a name="hdinsightondemandlinkedservicejson"></a><span data-ttu-id="c80c9-147">hdinsightondemandlinkedservice.json</span><span class="sxs-lookup"><span data-stu-id="c80c9-147">hdinsightondemandlinkedservice.json</span></span>

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

<span data-ttu-id="c80c9-148">Witaj Poniższa tabela zawiera opisy właściwości JSON hello używane we fragmencie hello:</span><span class="sxs-lookup"><span data-stu-id="c80c9-148">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

| <span data-ttu-id="c80c9-149">Właściwość</span><span class="sxs-lookup"><span data-stu-id="c80c9-149">Property</span></span> | <span data-ttu-id="c80c9-150">Opis</span><span class="sxs-lookup"><span data-stu-id="c80c9-150">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="c80c9-151">ClusterSize</span><span class="sxs-lookup"><span data-stu-id="c80c9-151">ClusterSize</span></span> |<span data-ttu-id="c80c9-152">Rozmiar klastra usługi HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="c80c9-152">Size of hello HDInsight cluster.</span></span> |
| <span data-ttu-id="c80c9-153">TimeToLive</span><span class="sxs-lookup"><span data-stu-id="c80c9-153">TimeToLive</span></span> |<span data-ttu-id="c80c9-154">Określa czas bezczynności tej hello hello klastra usługi HDInsight, przed usunięciem.</span><span class="sxs-lookup"><span data-stu-id="c80c9-154">Specifies that hello idle time for hello HDInsight cluster, before it is deleted.</span></span> |
| <span data-ttu-id="c80c9-155">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="c80c9-155">linkedServiceName</span></span> |<span data-ttu-id="c80c9-156">Określa konto magazynu hello jest używany toostore hello dzienniki, generowanych przez usługi HDInsight</span><span class="sxs-lookup"><span data-stu-id="c80c9-156">Specifies hello storage account that is used toostore hello logs that are generated by HDInsight</span></span> |

<span data-ttu-id="c80c9-157">Należy zwrócić uwagę hello następujące punkty:</span><span class="sxs-lookup"><span data-stu-id="c80c9-157">Note hello following points:</span></span>

* <span data-ttu-id="c80c9-158">Witaj fabryki danych tworzy **opartych na systemie Linux** klastra usługi HDInsight za pomocą hello powyżej JSON.</span><span class="sxs-lookup"><span data-stu-id="c80c9-158">hello Data Factory creates a **Linux-based** HDInsight cluster for you with hello above JSON.</span></span> <span data-ttu-id="c80c9-159">Szczegółowe informacje znajdują się w artykule [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) (Połączona usługa HDInsight na żądanie).</span><span class="sxs-lookup"><span data-stu-id="c80c9-159">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>
* <span data-ttu-id="c80c9-160">Możesz użyć **własnego klastra usługi HDInsight** zamiast klastra usługi HDInsight na żądanie.</span><span class="sxs-lookup"><span data-stu-id="c80c9-160">You could use **your own HDInsight cluster** instead of using an on-demand HDInsight cluster.</span></span> <span data-ttu-id="c80c9-161">Szczegółowe informacje znajdują się w artykule [HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) (Połączona usługa HDInsight).</span><span class="sxs-lookup"><span data-stu-id="c80c9-161">See [HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) for details.</span></span>
* <span data-ttu-id="c80c9-162">Tworzy klaster usługi HDInsight Hello **domyślny kontener** w magazynie obiektów blob hello określone w hello JSON (**linkedServiceName**).</span><span class="sxs-lookup"><span data-stu-id="c80c9-162">hello HDInsight cluster creates a **default container** in hello blob storage you specified in hello JSON (**linkedServiceName**).</span></span> <span data-ttu-id="c80c9-163">Po usunięciu klastra hello HDInsight nie usunie tego kontenera.</span><span class="sxs-lookup"><span data-stu-id="c80c9-163">HDInsight does not delete this container when hello cluster is deleted.</span></span> <span data-ttu-id="c80c9-164">To zachowanie jest celowe.</span><span class="sxs-lookup"><span data-stu-id="c80c9-164">This behavior is by design.</span></span> <span data-ttu-id="c80c9-165">Z usługą HDInsight połączony na żądanie, tworzenia klastra usługi HDInsight za każdym razem, gdy wycinek jest przetwarzany, chyba że istnieje istniejącego klastra na żywo (**timeToLive**) i zostaną usunięte po zakończeniu przetwarzania hello.</span><span class="sxs-lookup"><span data-stu-id="c80c9-165">With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice is processed unless there is an existing live cluster (**timeToLive**) and is deleted when hello processing is done.</span></span>

    <span data-ttu-id="c80c9-166">Po przetworzeniu większej liczby wycinków w usłudze Azure Blob Storage będzie widocznych wiele kontenerów.</span><span class="sxs-lookup"><span data-stu-id="c80c9-166">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="c80c9-167">Jeśli nie ma potrzeby do rozwiązywania problemów hello zadań, możesz toodelete ich magazynu hello tooreduce kosztów.</span><span class="sxs-lookup"><span data-stu-id="c80c9-167">If you do not need them for troubleshooting of hello jobs, you may want toodelete them tooreduce hello storage cost.</span></span> <span data-ttu-id="c80c9-168">nazwy Hello kontenery wykonaj wzorca: "adf**yourdatafactoryname**-**linkedservicename**- datetimestamp".</span><span class="sxs-lookup"><span data-stu-id="c80c9-168">hello names of these containers follow a pattern: "adf**yourdatafactoryname**-**linkedservicename**-datetimestamp".</span></span> <span data-ttu-id="c80c9-169">Użyj narzędzia takiego jak [Eksploratora magazynu](http://storageexplorer.com/) magazynu obiektów blob toodelete kontenerów w platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c80c9-169">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) toodelete containers in your Azure blob storage.</span></span>

<span data-ttu-id="c80c9-170">Szczegółowe informacje znajdują się w artykule [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) (Połączona usługa HDInsight na żądanie).</span><span class="sxs-lookup"><span data-stu-id="c80c9-170">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>

### <a name="inputdatasetjson"></a><span data-ttu-id="c80c9-171">inputdataset.json</span><span class="sxs-lookup"><span data-stu-id="c80c9-171">inputdataset.json</span></span>

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

<span data-ttu-id="c80c9-172">Witaj JSON definiuje zestaw danych o nazwie **AzureBlobInput**, który reprezentuje dane wejściowe dla działania w potoku hello.</span><span class="sxs-lookup"><span data-stu-id="c80c9-172">hello JSON defines a dataset named **AzureBlobInput**, which represents input data for an activity in hello pipeline.</span></span> <span data-ttu-id="c80c9-173">Ponadto określa ona, że danych wejściowych hello znajduje się w kontenerze obiektów blob hello o nazwie **adfgetstarted** i hello folder o nazwie **inputdata**.</span><span class="sxs-lookup"><span data-stu-id="c80c9-173">In addition, it specifies that hello input data is located in hello blob container called **adfgetstarted** and hello folder called **inputdata**.</span></span>

<span data-ttu-id="c80c9-174">Witaj Poniższa tabela zawiera opisy właściwości JSON hello używane we fragmencie hello:</span><span class="sxs-lookup"><span data-stu-id="c80c9-174">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

| <span data-ttu-id="c80c9-175">Właściwość</span><span class="sxs-lookup"><span data-stu-id="c80c9-175">Property</span></span> | <span data-ttu-id="c80c9-176">Opis</span><span class="sxs-lookup"><span data-stu-id="c80c9-176">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="c80c9-177">type</span><span class="sxs-lookup"><span data-stu-id="c80c9-177">type</span></span> |<span data-ttu-id="c80c9-178">Witaj właściwość type ma wartość tooAzureBlob, ponieważ dane znajdują się w magazynie obiektów blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c80c9-178">hello type property is set tooAzureBlob because data resides in Azure blob storage.</span></span> |
| <span data-ttu-id="c80c9-179">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="c80c9-179">linkedServiceName</span></span> |<span data-ttu-id="c80c9-180">odwołuje się toohello StorageLinkedService utworzony wcześniej.</span><span class="sxs-lookup"><span data-stu-id="c80c9-180">refers toohello StorageLinkedService you created earlier.</span></span> |
| <span data-ttu-id="c80c9-181">fileName</span><span class="sxs-lookup"><span data-stu-id="c80c9-181">fileName</span></span> |<span data-ttu-id="c80c9-182">Ta właściwość jest opcjonalna.</span><span class="sxs-lookup"><span data-stu-id="c80c9-182">This property is optional.</span></span> <span data-ttu-id="c80c9-183">W przypadku pominięcia tej właściwości, pobierane są wszystkie pliki hello z hello folderPath.</span><span class="sxs-lookup"><span data-stu-id="c80c9-183">If you omit this property, all hello files from hello folderPath are picked.</span></span> <span data-ttu-id="c80c9-184">W takim przypadku tylko input.log hello jest przetwarzany.</span><span class="sxs-lookup"><span data-stu-id="c80c9-184">In this case, only hello input.log is processed.</span></span> |
| <span data-ttu-id="c80c9-185">type</span><span class="sxs-lookup"><span data-stu-id="c80c9-185">type</span></span> |<span data-ttu-id="c80c9-186">pliki dziennika Hello są w formacie tekstowym, więc używamy TextFormat.</span><span class="sxs-lookup"><span data-stu-id="c80c9-186">hello log files are in text format, so we use TextFormat.</span></span> |
| <span data-ttu-id="c80c9-187">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="c80c9-187">columnDelimiter</span></span> |<span data-ttu-id="c80c9-188">kolumn w plikach dziennika hello są rozdzielone znakiem przecinkami ()</span><span class="sxs-lookup"><span data-stu-id="c80c9-188">columns in hello log files are delimited by a comma character (,)</span></span> |
| <span data-ttu-id="c80c9-189">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="c80c9-189">frequency/interval</span></span> |<span data-ttu-id="c80c9-190">tooMonth Ustaw częstotliwość i interwał wynosi 1, co oznacza, że wejściowy wycinków hello są dostępne co miesiąc.</span><span class="sxs-lookup"><span data-stu-id="c80c9-190">frequency set tooMonth and interval is 1, which means that hello input slices are available monthly.</span></span> |
| <span data-ttu-id="c80c9-191">external</span><span class="sxs-lookup"><span data-stu-id="c80c9-191">external</span></span> |<span data-ttu-id="c80c9-192">Ta właściwość ma wartość tootrue, jeśli dane wejściowe hello nie jest generowany przez hello usługi fabryka danych.</span><span class="sxs-lookup"><span data-stu-id="c80c9-192">this property is set tootrue if hello input data is not generated by hello Data Factory service.</span></span> |

### <a name="outputdatasetjson"></a><span data-ttu-id="c80c9-193">outputdataset.json</span><span class="sxs-lookup"><span data-stu-id="c80c9-193">outputdataset.json</span></span>

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

<span data-ttu-id="c80c9-194">Witaj JSON definiuje zestaw danych o nazwie **AzureBlobOutput**, który reprezentuje danych wyjściowych dla działania w potoku hello.</span><span class="sxs-lookup"><span data-stu-id="c80c9-194">hello JSON defines a dataset named **AzureBlobOutput**, which represents output data for an activity in hello pipeline.</span></span> <span data-ttu-id="c80c9-195">Ponadto określa ona, że wyniki hello są przechowywane w kontenerze obiektów blob hello o nazwie **adfgetstarted** i hello folder o nazwie **partitioneddata**.</span><span class="sxs-lookup"><span data-stu-id="c80c9-195">In addition, it specifies that hello results are stored in hello blob container called **adfgetstarted** and hello folder called **partitioneddata**.</span></span> <span data-ttu-id="c80c9-196">Witaj **dostępności** sekcja określa, że wyjściowy zestaw danych hello jest tworzony co miesiąc.</span><span class="sxs-lookup"><span data-stu-id="c80c9-196">hello **availability** section specifies that hello output dataset is produced on a monthly basis.</span></span>

### <a name="pipelinejson"></a><span data-ttu-id="c80c9-197">pipeline.json</span><span class="sxs-lookup"><span data-stu-id="c80c9-197">pipeline.json</span></span>
> [!IMPORTANT]
> <span data-ttu-id="c80c9-198">Zastąp wartość **storageaccountname** nazwą konta usługi Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="c80c9-198">Replace **storageaccountname** with name of your Azure storage account.</span></span>
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

<span data-ttu-id="c80c9-199">We fragmencie JSON hello tworzysz potok, który składa się z jednego działania, który używa danych tooprocess gałęzi w klastrze usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c80c9-199">In hello JSON snippet, you are creating a pipeline that consists of a single activity that uses Hive tooprocess data on a HDInsight cluster.</span></span>

<span data-ttu-id="c80c9-200">plik skryptu Hive Hello, **partitionweblogs.hql**, są przechowywane w hello kontem magazynu platformy Azure (określonego przez element scriptLinkedService hello, nazywany **StorageLinkedService**) i w **skryptu**  folderu w kontenerze hello **adfgetstarted**.</span><span class="sxs-lookup"><span data-stu-id="c80c9-200">hello Hive script file, **partitionweblogs.hql**, is stored in hello Azure storage account (specified by hello scriptLinkedService, called **StorageLinkedService**), and in **script** folder in hello container **adfgetstarted**.</span></span>

<span data-ttu-id="c80c9-201">Witaj **definiuje** sekcji określa ustawienia środowiska uruchomieniowego, które są przekazywane skryptu hive toohello jako wartości konfiguracji gałąź (np. ${hiveconf: inputtable}, {hiveconf:partitionedtable} $).</span><span class="sxs-lookup"><span data-stu-id="c80c9-201">hello **defines** section specifies runtime settings that are passed toohello hive script as Hive configuration values (e.g ${hiveconf:inputtable}, ${hiveconf:partitionedtable}).</span></span>

<span data-ttu-id="c80c9-202">Witaj **start** i **zakończenia** hello aktywny okres potoku hello określa właściwości hello potoku.</span><span class="sxs-lookup"><span data-stu-id="c80c9-202">hello **start** and **end** properties of hello pipeline specifies hello active period of hello pipeline.</span></span>

<span data-ttu-id="c80c9-203">W działaniu hello JSON, możesz określić, tego skryptu Hive hello zostanie uruchomiona na określony przez hello obliczeń hello **linkedServiceName** — **HDInsightOnDemandLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="c80c9-203">In hello activity JSON, you specify that hello Hive script runs on hello compute specified by hello **linkedServiceName** – **HDInsightOnDemandLinkedService**.</span></span>

> [!NOTE]
> <span data-ttu-id="c80c9-204">Zobacz sekcję "JSON potoku" w [potoki i działań w fabryce danych Azure](data-factory-create-pipelines.md) szczegółowe informacje na temat właściwości JSON używane w hello poprzedzających przykład.</span><span class="sxs-lookup"><span data-stu-id="c80c9-204">See "Pipeline JSON" in [Pipelines and activities in Azure Data Factory](data-factory-create-pipelines.md) for details about JSON properties used in hello preceding example.</span></span>
>
>

## <a name="set-global-variables"></a><span data-ttu-id="c80c9-205">Ustawianie zmiennych globalnych</span><span class="sxs-lookup"><span data-stu-id="c80c9-205">Set global variables</span></span>
<span data-ttu-id="c80c9-206">W programie Azure PowerShell wykonaj następujące polecenia, po zastąpieniu hello wartości własnymi hello:</span><span class="sxs-lookup"><span data-stu-id="c80c9-206">In Azure PowerShell, execute hello following commands after replacing hello values with your own:</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c80c9-207">Zobacz sekcję [Wymagania wstępne](#prerequisites), aby uzyskać instrukcje dotyczące pobierania identyfikatora klienta, klucza tajnego klienta, identyfikatora dzierżawy oraz identyfikatora subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="c80c9-207">See [Prerequisites](#prerequisites) section for instructions on getting client ID, client secret, tenant ID, and subscription ID.</span></span>
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


## <a name="authenticate-with-aad"></a><span data-ttu-id="c80c9-208">Uwierzytelnianie przy użyciu usługi AAD</span><span class="sxs-lookup"><span data-stu-id="c80c9-208">Authenticate with AAD</span></span>

```PowerShell
$cmd = { .\curl.exe -X POST https://login.microsoftonline.com/$tenant/oauth2/token  -F grant_type=client_credentials  -F resource=https://management.core.windows.net/ -F client_id=$client_id -F client_secret=$client_secret };
$responseToken = Invoke-Command -scriptblock $cmd;
$accessToken = (ConvertFrom-Json $responseToken).access_token;

(ConvertFrom-Json $responseToken)
```


## <a name="create-data-factory"></a><span data-ttu-id="c80c9-209">Tworzenie fabryki danych</span><span class="sxs-lookup"><span data-stu-id="c80c9-209">Create data factory</span></span>
<span data-ttu-id="c80c9-210">W tym kroku opisano tworzenie fabryki danych Azure o nazwie **FirstDataFactoryREST**.</span><span class="sxs-lookup"><span data-stu-id="c80c9-210">In this step, you create an Azure Data Factory named **FirstDataFactoryREST**.</span></span> <span data-ttu-id="c80c9-211">Fabryka danych może obejmować jeden lub wiele potoków.</span><span class="sxs-lookup"><span data-stu-id="c80c9-211">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="c80c9-212">Potok może obejmować jedno lub wiele działań.</span><span class="sxs-lookup"><span data-stu-id="c80c9-212">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="c80c9-213">Na przykład działanie kopiowania toocopy danych z magazynu danych docelowy tooa źródłowego i HDInsight Hive działania toorun danych tootransform skryptu Hive.</span><span class="sxs-lookup"><span data-stu-id="c80c9-213">For example, a Copy Activity toocopy data from a source tooa destination data store and a HDInsight Hive activity toorun a Hive script tootransform data.</span></span> <span data-ttu-id="c80c9-214">Uruchom powitania po fabryki danych hello toocreate polecenia:</span><span class="sxs-lookup"><span data-stu-id="c80c9-214">Run hello following commands toocreate hello data factory:</span></span>

1. <span data-ttu-id="c80c9-215">Przypisz hello toovariable polecenia o nazwie **cmd**.</span><span class="sxs-lookup"><span data-stu-id="c80c9-215">Assign hello command toovariable named **cmd**.</span></span>

    <span data-ttu-id="c80c9-216">Potwierdzić tę nazwę hello hello fabryki danych określone w tym miejscu (ADFCopyTutorialDF) dopasowań hello nazwa określona w hello **datafactory.json**.</span><span class="sxs-lookup"><span data-stu-id="c80c9-216">Confirm that hello name of hello data factory you specify here (ADFCopyTutorialDF) matches hello name specified in hello **datafactory.json**.</span></span>

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data “@datafactory.json” https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/FirstDataFactoryREST?api-version=2015-10-01};
    ```
2. <span data-ttu-id="c80c9-217">Uruchom polecenie hello przy użyciu **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="c80c9-217">Run hello command by using **Invoke-Command**.</span></span>

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="c80c9-218">Wyświetl wyniki hello.</span><span class="sxs-lookup"><span data-stu-id="c80c9-218">View hello results.</span></span> <span data-ttu-id="c80c9-219">Po pomyślnym utworzeniu hello fabryki danych Zobacz hello JSON dla fabryki danych hello w hello **wyniki**; w przeciwnym razie zostanie wyświetlony komunikat o błędzie.</span><span class="sxs-lookup"><span data-stu-id="c80c9-219">If hello data factory has been successfully created, you see hello JSON for hello data factory in hello **results**; otherwise, you see an error message.</span></span>

    ```PowerShell
    Write-Host $results
    ```

<span data-ttu-id="c80c9-220">Należy zwrócić uwagę hello następujące punkty:</span><span class="sxs-lookup"><span data-stu-id="c80c9-220">Note hello following points:</span></span>

* <span data-ttu-id="c80c9-221">Nazwa Hello hello fabryki danych Azure musi być globalnie unikatowe.</span><span class="sxs-lookup"><span data-stu-id="c80c9-221">hello name of hello Azure Data Factory must be globally unique.</span></span> <span data-ttu-id="c80c9-222">Jeśli zostanie wyświetlony błąd hello w wynikach: **nazwa fabryki danych "FirstDataFactoryREST" nie jest dostępna**, hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="c80c9-222">If you see hello error in results: **Data factory name “FirstDataFactoryREST” is not available**, do hello following steps:</span></span>
  1. <span data-ttu-id="c80c9-223">Zmień nazwę hello (na przykład yournameFirstDataFactoryREST) w hello **datafactory.json** pliku.</span><span class="sxs-lookup"><span data-stu-id="c80c9-223">Change hello name (for example, yournameFirstDataFactoryREST) in hello **datafactory.json** file.</span></span> <span data-ttu-id="c80c9-224">Artykuł [Data Factory — Naming Rules](data-factory-naming-rules.md) (Fabryka danych — zasady nazewnictwa) zawiera zasady nazewnictwa artefaktów usługi Fabryka danych.</span><span class="sxs-lookup"><span data-stu-id="c80c9-224">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>
  2. <span data-ttu-id="c80c9-225">W pierwszym poleceniem hello gdzie hello **$cmd** zmiennej jest przypisywana wartość, Zamień FirstDataFactoryREST hello nowej nazwy i uruchom polecenie hello.</span><span class="sxs-lookup"><span data-stu-id="c80c9-225">In hello first command where hello **$cmd** variable is assigned a value, replace FirstDataFactoryREST with hello new name and run hello command.</span></span>
  3. <span data-ttu-id="c80c9-226">Uruchamianie hello następne dwa polecenia tooinvoke hello interfejsu API REST toocreate hello danych fabryki i Drukuj hello wyników hello operacji.</span><span class="sxs-lookup"><span data-stu-id="c80c9-226">Run hello next two commands tooinvoke hello REST API toocreate hello data factory and print hello results of hello operation.</span></span>
* <span data-ttu-id="c80c9-227">toocreate wystąpienia fabryki danych, należy toobe współautora/administrator hello subskrypcji platformy Azure</span><span class="sxs-lookup"><span data-stu-id="c80c9-227">toocreate Data Factory instances, you need toobe a contributor/administrator of hello Azure subscription</span></span>
* <span data-ttu-id="c80c9-228">Nazwa fabryki danych hello Hello mogą być zarejestrowana jako nazwa DNS w przyszłości hello i dlatego stać się publicznie widoczna.</span><span class="sxs-lookup"><span data-stu-id="c80c9-228">hello name of hello data factory may be registered as a DNS name in hello future and hence become publicly visible.</span></span>
* <span data-ttu-id="c80c9-229">Jeśli wystąpi błąd hello: "**Ta subskrypcja nie jest zarejestrowany toouse przestrzeni nazw Microsoft.DataFactory**", wykonaj jedną z następujących hello i spróbuj ponownie opublikować:</span><span class="sxs-lookup"><span data-stu-id="c80c9-229">If you receive hello error: "**This subscription is not registered toouse namespace Microsoft.DataFactory**", do one of hello following and try publishing again:</span></span>

  * <span data-ttu-id="c80c9-230">W programie Azure PowerShell Uruchom hello następujące polecenia tooregister hello fabryki danych dostawcy:</span><span class="sxs-lookup"><span data-stu-id="c80c9-230">In Azure PowerShell, run hello following command tooregister hello Data Factory provider:</span></span>

    ```PowerShell
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```

      <span data-ttu-id="c80c9-231">Powitania po tooconfirm polecenie można uruchomić tej fabryki danych w zarejestrowany dostawca hello:</span><span class="sxs-lookup"><span data-stu-id="c80c9-231">You can run hello following command tooconfirm that hello Data Factory provider is registered:</span></span>
    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * <span data-ttu-id="c80c9-232">Logowanie przy użyciu hello subskrypcji platformy Azure do hello [portalu Azure](https://portal.azure.com) i przejdź do bloku usługi fabryka danych tooa tworzenie fabryki danych w hello portalu Azure (lub).</span><span class="sxs-lookup"><span data-stu-id="c80c9-232">Login using hello Azure subscription into hello [Azure portal](https://portal.azure.com) and navigate tooa Data Factory blade (or) create a data factory in hello Azure portal.</span></span> <span data-ttu-id="c80c9-233">Ta akcja rejestruje automatycznie hello dostawcy dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="c80c9-233">This action automatically registers hello provider for you.</span></span>

<span data-ttu-id="c80c9-234">Przed utworzeniem potoku, należy toocreate kilku jednostek fabryki danych najpierw.</span><span class="sxs-lookup"><span data-stu-id="c80c9-234">Before creating a pipeline, you need toocreate a few Data Factory entities first.</span></span> <span data-ttu-id="c80c9-235">Najpierw utwórz danych toolink połączonych usług danych tooyour magazyny/oblicza przechowywania, zdefiniuj dane wejściowe i zestawów danych toorepresent dane w magazynach połączone dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="c80c9-235">You first create linked services toolink data stores/computes tooyour data store, define input and output datasets toorepresent data in linked data stores.</span></span>

## <a name="create-linked-services"></a><span data-ttu-id="c80c9-236">Tworzenie połączonych usług</span><span class="sxs-lookup"><span data-stu-id="c80c9-236">Create linked services</span></span>
<span data-ttu-id="c80c9-237">W tym kroku możesz połączyć konta magazynu Azure i fabrykę danych tooyour klastra Azure HDInsight na żądanie.</span><span class="sxs-lookup"><span data-stu-id="c80c9-237">In this step, you link your Azure Storage account and an on-demand Azure HDInsight cluster tooyour data factory.</span></span> <span data-ttu-id="c80c9-238">blokady konta usługi Azure Storage Hello hello danych wejściowych i wyjściowych do potoku hello w tym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="c80c9-238">hello Azure Storage account holds hello input and output data for hello pipeline in this sample.</span></span> <span data-ttu-id="c80c9-239">Hello usługi HDInsight połączony jest używane toorun określony w działaniu hello hello potoku, w tym przykładzie skrypt Hive.</span><span class="sxs-lookup"><span data-stu-id="c80c9-239">hello HDInsight linked service is used toorun a Hive script specified in hello activity of hello pipeline in this sample.</span></span>

### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="c80c9-240">Tworzenie połączonej usługi Azure Storage</span><span class="sxs-lookup"><span data-stu-id="c80c9-240">Create Azure Storage linked service</span></span>
<span data-ttu-id="c80c9-241">W tym kroku możesz połączyć fabrykę danych tooyour konta magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="c80c9-241">In this step, you link your Azure Storage account tooyour data factory.</span></span> <span data-ttu-id="c80c9-242">Z tego samouczka użyjesz hello tego samego konta magazynu Azure toostore wejścia/wyjścia danych i hello HQL plik skryptu.</span><span class="sxs-lookup"><span data-stu-id="c80c9-242">With this tutorial, you use hello same Azure Storage account toostore input/output data and hello HQL script file.</span></span>

1. <span data-ttu-id="c80c9-243">Przypisz hello toovariable polecenia o nazwie **cmd**.</span><span class="sxs-lookup"><span data-stu-id="c80c9-243">Assign hello command toovariable named **cmd**.</span></span>

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data “@azurestoragelinkedservice.json” https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/linkedservices/AzureStorageLinkedService?api-version=2015-10-01};
    ```
2. <span data-ttu-id="c80c9-244">Uruchom polecenie hello przy użyciu **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="c80c9-244">Run hello command by using **Invoke-Command**.</span></span>

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="c80c9-245">Wyświetl wyniki hello.</span><span class="sxs-lookup"><span data-stu-id="c80c9-245">View hello results.</span></span> <span data-ttu-id="c80c9-246">Jeśli hello połączone usługi został utworzony pomyślnie, zobacz hello JSON usługi hello połączone w hello **wyniki**; w przeciwnym razie zostanie wyświetlony komunikat o błędzie.</span><span class="sxs-lookup"><span data-stu-id="c80c9-246">If hello linked service has been successfully created, you see hello JSON for hello linked service in hello **results**; otherwise, you see an error message.</span></span>

    ```PowerShell
    Write-Host $results
    ```

### <a name="create-azure-hdinsight-linked-service"></a><span data-ttu-id="c80c9-247">Tworzenie połączonej usługi Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="c80c9-247">Create Azure HDInsight linked service</span></span>
<span data-ttu-id="c80c9-248">W tym kroku możesz połączyć fabrykę danych tooyour klastra usługi HDInsight na żądanie.</span><span class="sxs-lookup"><span data-stu-id="c80c9-248">In this step, you link an on-demand HDInsight cluster tooyour data factory.</span></span> <span data-ttu-id="c80c9-249">klaster usługi HDInsight Hello jest automatycznie tworzone w czasie wykonywania i usuwane po zakończeniu przetwarzania i bezczynności hello określoną ilość czasu.</span><span class="sxs-lookup"><span data-stu-id="c80c9-249">hello HDInsight cluster is automatically created at runtime and deleted after it is done processing and idle for hello specified amount of time.</span></span> <span data-ttu-id="c80c9-250">Możesz użyć własnego klastra usługi HDInsight zamiast klastra usługi HDInsight na żądanie.</span><span class="sxs-lookup"><span data-stu-id="c80c9-250">You could use your own HDInsight cluster instead of using an on-demand HDInsight cluster.</span></span> <span data-ttu-id="c80c9-251">Szczegółowe informacje znajdują się w artykule [Compute Linked Services](data-factory-compute-linked-services.md) (Połączone usługi obliczeniowe).</span><span class="sxs-lookup"><span data-stu-id="c80c9-251">See [Compute Linked Services](data-factory-compute-linked-services.md) for details.</span></span>

1. <span data-ttu-id="c80c9-252">Przypisz hello toovariable polecenia o nazwie **cmd**.</span><span class="sxs-lookup"><span data-stu-id="c80c9-252">Assign hello command toovariable named **cmd**.</span></span>

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@hdinsightondemandlinkedservice.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/linkedservices/hdinsightondemandlinkedservice?api-version=2015-10-01};
    ```
2. <span data-ttu-id="c80c9-253">Uruchom polecenie hello przy użyciu **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="c80c9-253">Run hello command by using **Invoke-Command**.</span></span>

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="c80c9-254">Wyświetl wyniki hello.</span><span class="sxs-lookup"><span data-stu-id="c80c9-254">View hello results.</span></span> <span data-ttu-id="c80c9-255">Jeśli hello połączone usługi został utworzony pomyślnie, zobacz hello JSON usługi hello połączone w hello **wyniki**; w przeciwnym razie zostanie wyświetlony komunikat o błędzie.</span><span class="sxs-lookup"><span data-stu-id="c80c9-255">If hello linked service has been successfully created, you see hello JSON for hello linked service in hello **results**; otherwise, you see an error message.</span></span>

    ```PowerShell
    Write-Host $results
    ```

## <a name="create-datasets"></a><span data-ttu-id="c80c9-256">Tworzenie zestawów danych</span><span class="sxs-lookup"><span data-stu-id="c80c9-256">Create datasets</span></span>
<span data-ttu-id="c80c9-257">W tym kroku utwórz wprowadzania hello toorepresent zestawów danych i wysyłania danych do przetwarzania Hive.</span><span class="sxs-lookup"><span data-stu-id="c80c9-257">In this step, you create datasets toorepresent hello input and output data for Hive processing.</span></span> <span data-ttu-id="c80c9-258">Te zestawy danych można znaleźć toohello **StorageLinkedService** został utworzony we wcześniejszej części tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="c80c9-258">These datasets refer toohello **StorageLinkedService** you have created earlier in this tutorial.</span></span> <span data-ttu-id="c80c9-259">Witaj tooan punktów połączonej usługi konta usługi Azure Storage i zestawów danych, określ kontener, folder, nazwa pliku w magazynie hello, która przechowuje dane wejściowe i wyjściowe danych.</span><span class="sxs-lookup"><span data-stu-id="c80c9-259">hello linked service points tooan Azure Storage account and datasets specify container, folder, file name in hello storage that holds input and output data.</span></span>

### <a name="create-input-dataset"></a><span data-ttu-id="c80c9-260">Tworzenie wejściowego zestawu danych</span><span class="sxs-lookup"><span data-stu-id="c80c9-260">Create input dataset</span></span>
<span data-ttu-id="c80c9-261">W tym kroku utworzysz hello wejściowy zestaw danych toorepresent danych wejściowych przechowywanych w magazynie obiektów Blob platformy Azure hello.</span><span class="sxs-lookup"><span data-stu-id="c80c9-261">In this step, you create hello input dataset toorepresent input data stored in hello Azure Blob storage.</span></span>

1. <span data-ttu-id="c80c9-262">Przypisz hello toovariable polecenia o nazwie **cmd**.</span><span class="sxs-lookup"><span data-stu-id="c80c9-262">Assign hello command toovariable named **cmd**.</span></span>

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@inputdataset.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/AzureBlobInput?api-version=2015-10-01};
    ```
2. <span data-ttu-id="c80c9-263">Uruchom polecenie hello przy użyciu **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="c80c9-263">Run hello command by using **Invoke-Command**.</span></span>

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="c80c9-264">Wyświetl wyniki hello.</span><span class="sxs-lookup"><span data-stu-id="c80c9-264">View hello results.</span></span> <span data-ttu-id="c80c9-265">Po pomyślnym utworzeniu zestawu danych hello Zobacz hello JSON dla zestawu danych hello w hello **wyniki**; w przeciwnym razie zostanie wyświetlony komunikat o błędzie.</span><span class="sxs-lookup"><span data-stu-id="c80c9-265">If hello dataset has been successfully created, you see hello JSON for hello dataset in hello **results**; otherwise, you see an error message.</span></span>

    ```PowerShell
    Write-Host $results
    ```

### <a name="create-output-dataset"></a><span data-ttu-id="c80c9-266">Tworzenie wyjściowego zestawu danych</span><span class="sxs-lookup"><span data-stu-id="c80c9-266">Create output dataset</span></span>
<span data-ttu-id="c80c9-267">W tym kroku utworzysz hello wyjściowego zestawu danych toorepresent danych wyjściowych danych przechowywanych w hello magazynu obiektów Blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c80c9-267">In this step, you create hello output dataset toorepresent output data stored in hello Azure Blob storage.</span></span>

1. <span data-ttu-id="c80c9-268">Przypisz hello toovariable polecenia o nazwie **cmd**.</span><span class="sxs-lookup"><span data-stu-id="c80c9-268">Assign hello command toovariable named **cmd**.</span></span>

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@outputdataset.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/AzureBlobOutput?api-version=2015-10-01};
    ```
2. <span data-ttu-id="c80c9-269">Uruchom polecenie hello przy użyciu **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="c80c9-269">Run hello command by using **Invoke-Command**.</span></span>

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="c80c9-270">Wyświetl wyniki hello.</span><span class="sxs-lookup"><span data-stu-id="c80c9-270">View hello results.</span></span> <span data-ttu-id="c80c9-271">Po pomyślnym utworzeniu zestawu danych hello Zobacz hello JSON dla zestawu danych hello w hello **wyniki**; w przeciwnym razie zostanie wyświetlony komunikat o błędzie.</span><span class="sxs-lookup"><span data-stu-id="c80c9-271">If hello dataset has been successfully created, you see hello JSON for hello dataset in hello **results**; otherwise, you see an error message.</span></span>

    ```PowerShell
    Write-Host $results
    ```

## <a name="create-pipeline"></a><span data-ttu-id="c80c9-272">Tworzenie potoku</span><span class="sxs-lookup"><span data-stu-id="c80c9-272">Create pipeline</span></span>
<span data-ttu-id="c80c9-273">W tym kroku opisano tworzenie pierwszego potoku za pomocą działania **HDInsightHive**.</span><span class="sxs-lookup"><span data-stu-id="c80c9-273">In this step, you create your first pipeline with a **HDInsightHive** activity.</span></span> <span data-ttu-id="c80c9-274">Wejściowy jest dostępny co miesiąc (częstotliwość: miesiąc, interwał: 1), wycinek danych wyjściowych jest tworzony co miesiąc, a właściwość harmonogramu hello działania hello jest ustawić toomonthly.</span><span class="sxs-lookup"><span data-stu-id="c80c9-274">Input slice is available monthly (frequency: Month, interval: 1), output slice is produced monthly, and hello scheduler property for hello activity is also set toomonthly.</span></span> <span data-ttu-id="c80c9-275">Ustawienia Hello hello wyjściowego zestawu danych i harmonogram działania hello muszą być zgodne.</span><span class="sxs-lookup"><span data-stu-id="c80c9-275">hello settings for hello output dataset and hello activity scheduler must match.</span></span> <span data-ttu-id="c80c9-276">Wyjściowy zestaw danych jest obecnie, jakie dysków hello harmonogramu, dlatego należy utworzyć wyjściowy zestaw danych, nawet wtedy, gdy działanie hello nie generuje żadnego wyniku.</span><span class="sxs-lookup"><span data-stu-id="c80c9-276">Currently, output dataset is what drives hello schedule, so you must create an output dataset even if hello activity does not produce any output.</span></span> <span data-ttu-id="c80c9-277">Jeśli działanie hello nie przyjmuje żadnych danych, możesz pominąć tworzenie zestawu danych wejściowych hello.</span><span class="sxs-lookup"><span data-stu-id="c80c9-277">If hello activity doesn't take any input, you can skip creating hello input dataset.</span></span>

<span data-ttu-id="c80c9-278">Upewnij się, że widoczny hello **input.log** pliku w hello **adfgetstarted/inputdata** folderu w hello magazynu obiektów blob platformy Azure i hello uruchom następujące polecenie toodeploy hello potoku.</span><span class="sxs-lookup"><span data-stu-id="c80c9-278">Confirm that you see hello **input.log** file in hello **adfgetstarted/inputdata** folder in hello Azure blob storage, and run hello following command toodeploy hello pipeline.</span></span> <span data-ttu-id="c80c9-279">Ponieważ hello **start** i **zakończenia** czasy są ustawiane w przeszłości hello i **isPaused** jest zestaw toofalse, potoku hello (działania w potoku hello) uruchamia natychmiast po wdrożeniu.</span><span class="sxs-lookup"><span data-stu-id="c80c9-279">Since hello **start** and **end** times are set in hello past and **isPaused** is set toofalse, hello pipeline (activity in hello pipeline) runs immediately after you deploy.</span></span>

1. <span data-ttu-id="c80c9-280">Przypisz hello toovariable polecenia o nazwie **cmd**.</span><span class="sxs-lookup"><span data-stu-id="c80c9-280">Assign hello command toovariable named **cmd**.</span></span>

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@pipeline.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datapipelines/MyFirstPipeline?api-version=2015-10-01};
    ```
2. <span data-ttu-id="c80c9-281">Uruchom polecenie hello przy użyciu **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="c80c9-281">Run hello command by using **Invoke-Command**.</span></span>

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="c80c9-282">Wyświetl wyniki hello.</span><span class="sxs-lookup"><span data-stu-id="c80c9-282">View hello results.</span></span> <span data-ttu-id="c80c9-283">Po pomyślnym utworzeniu zestawu danych hello Zobacz hello JSON dla zestawu danych hello w hello **wyniki**; w przeciwnym razie zostanie wyświetlony komunikat o błędzie.</span><span class="sxs-lookup"><span data-stu-id="c80c9-283">If hello dataset has been successfully created, you see hello JSON for hello dataset in hello **results**; otherwise, you see an error message.</span></span>

    ```PowerShell
    Write-Host $results
    ```
4. <span data-ttu-id="c80c9-284">Gratulacje! Udało Ci się utworzyć pierwszy potok przy użyciu programu Azure PowerShell!</span><span class="sxs-lookup"><span data-stu-id="c80c9-284">Congratulations, you have successfully created your first pipeline using Azure PowerShell!</span></span>

## <a name="monitor-pipeline"></a><span data-ttu-id="c80c9-285">Monitorowanie potoku</span><span class="sxs-lookup"><span data-stu-id="c80c9-285">Monitor pipeline</span></span>
<span data-ttu-id="c80c9-286">W tym kroku użyjesz tworzonym przez potok hello wycinków toomonitor interfejsu API REST fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="c80c9-286">In this step, you use Data Factory REST API toomonitor slices being produced by hello pipeline.</span></span>

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
> <span data-ttu-id="c80c9-287">Tworzenie klastra usługi HDInsight na żądanie zwykle trwa trochę czasu (około 20 minut).</span><span class="sxs-lookup"><span data-stu-id="c80c9-287">Creation of an on-demand HDInsight cluster usually takes sometime (approximately 20 minutes).</span></span> <span data-ttu-id="c80c9-288">W związku z tym spodziewać się hello potoku tootake **około 30 minut** tooprocess hello wycinka.</span><span class="sxs-lookup"><span data-stu-id="c80c9-288">Therefore, expect hello pipeline tootake **approximately 30 minutes** tooprocess hello slice.</span></span>
>
>

<span data-ttu-id="c80c9-289">Uruchom hello Invoke-Command i hello kolejnego do momentu wyświetlenia wycinek hello **gotowe** stanu lub **** stanu.</span><span class="sxs-lookup"><span data-stu-id="c80c9-289">Run hello Invoke-Command and hello next one until you see hello slice in **Ready** state or **Failed** state.</span></span> <span data-ttu-id="c80c9-290">Gdy wycinek hello jest w stanie gotowe, sprawdź hello **partitioneddata** folderu w hello **adfgetstarted** kontenera w magazynie obiektów blob na powitania dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="c80c9-290">When hello slice is in Ready state, check hello **partitioneddata** folder in hello **adfgetstarted** container in your blob storage for hello output data.</span></span>  <span data-ttu-id="c80c9-291">Tworzenie klastra usługi HDInsight na żądanie Hello zazwyczaj trwa trochę czasu.</span><span class="sxs-lookup"><span data-stu-id="c80c9-291">hello creation of an on-demand HDInsight cluster usually takes some time.</span></span>

![Dane wyjściowe](./media/data-factory-build-your-first-pipeline-using-rest-api/three-ouptut-files.png)

> [!IMPORTANT]
> <span data-ttu-id="c80c9-293">Plik wejściowy Hello zostaje usunięta, gdy hello wycinek jest przetwarzany pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="c80c9-293">hello input file gets deleted when hello slice is processed successfully.</span></span> <span data-ttu-id="c80c9-294">W związku z tym hello plik wejściowy (input.log) toohello inputdata folder kontenera adfgetstarted hello przekazywania wycinek hello toorerun lub Witaj ponownie samouczek.</span><span class="sxs-lookup"><span data-stu-id="c80c9-294">Therefore, if you want toorerun hello slice or do hello tutorial again, upload hello input file (input.log) toohello inputdata folder of hello adfgetstarted container.</span></span>
>
>

<span data-ttu-id="c80c9-295">Można również użyć wycinków toomonitor portalu Azure i rozwiązać wszelkie napotkane problemy.</span><span class="sxs-lookup"><span data-stu-id="c80c9-295">You can also use Azure portal toomonitor slices and troubleshoot any issues.</span></span> <span data-ttu-id="c80c9-296">Aby poznać szczegóły, zapoznaj się z informacjami dotyczącymi [monitorowania potoków w witrynie Azure Portal](data-factory-build-your-first-pipeline-using-editor.md#monitor-pipeline).</span><span class="sxs-lookup"><span data-stu-id="c80c9-296">See [Monitor pipelines using Azure portal](data-factory-build-your-first-pipeline-using-editor.md#monitor-pipeline) details.</span></span>

## <a name="summary"></a><span data-ttu-id="c80c9-297">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="c80c9-297">Summary</span></span>
<span data-ttu-id="c80c9-298">W tym samouczku danych tooprocess fabryki danych Azure została utworzona przez uruchomienie skryptu Hive w klastrze HDInsight hadoop.</span><span class="sxs-lookup"><span data-stu-id="c80c9-298">In this tutorial, you created an Azure data factory tooprocess data by running Hive script on a HDInsight hadoop cluster.</span></span> <span data-ttu-id="c80c9-299">Użyto hello Edytor fabryki danych w hello Azure toodo portalu hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="c80c9-299">You used hello Data Factory Editor in hello Azure portal toodo hello following steps:</span></span>

1. <span data-ttu-id="c80c9-300">Tworzenie **fabryki danych** Azure.</span><span class="sxs-lookup"><span data-stu-id="c80c9-300">Created an Azure **data factory**.</span></span>
2. <span data-ttu-id="c80c9-301">Utworzyć dwie **połączone usługi**:</span><span class="sxs-lookup"><span data-stu-id="c80c9-301">Created two **linked services**:</span></span>
   1. <span data-ttu-id="c80c9-302">**Usługa Azure Storage** połączone usługi toolink Twojego magazynu Azure blob storage przechowuje pliki danych wejściowych/wyjściowych toohello usługi fabryka danych.</span><span class="sxs-lookup"><span data-stu-id="c80c9-302">**Azure Storage** linked service toolink your Azure blob storage that holds input/output files toohello data factory.</span></span>
   2. <span data-ttu-id="c80c9-303">**Usługa Azure HDInsight** na żądanie połączone usługi toolink fabrykę danych toohello klastra usługi HDInsight Hadoop na żądanie.</span><span class="sxs-lookup"><span data-stu-id="c80c9-303">**Azure HDInsight** on-demand linked service toolink an on-demand HDInsight Hadoop cluster toohello data factory.</span></span> <span data-ttu-id="c80c9-304">Fabryka danych Azure tworzy HDInsight Hadoop dane wejściowe w czasie tooprocess klastra i danych wyjściowych produktu.</span><span class="sxs-lookup"><span data-stu-id="c80c9-304">Azure Data Factory creates a HDInsight Hadoop cluster just-in-time tooprocess input data and produce output data.</span></span>
3. <span data-ttu-id="c80c9-305">Utworzone dwie **zestawów danych**, które opisują danych wejściowych i wyjściowych dla działania HDInsight Hive w potoku hello.</span><span class="sxs-lookup"><span data-stu-id="c80c9-305">Created two **datasets**, which describe input and output data for HDInsight Hive activity in hello pipeline.</span></span>
4. <span data-ttu-id="c80c9-306">Utworzyć **potok** za pomocą działania **programu Hive w usłudze HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="c80c9-306">Created a **pipeline** with a **HDInsight Hive** activity.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c80c9-307">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c80c9-307">Next steps</span></span>
<span data-ttu-id="c80c9-308">W tym artykule opisano tworzenie potoku za pomocą działania przekształcania (działanie usługi HDInsight), które uruchamia skrypt programu Hive w klastrze usługi HDInsight platformy Azure na żądanie.</span><span class="sxs-lookup"><span data-stu-id="c80c9-308">In this article, you have created a pipeline with a transformation activity (HDInsight Activity) that runs a Hive script on an on-demand Azure HDInsight cluster.</span></span> <span data-ttu-id="c80c9-309">toosee toouse toocopy działanie kopiowania danych z tooAzure obiektów Blob platformy Azure SQL, zobacz temat [samouczek: kopiowanie danych z obiektu Blob Azure tooAzure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="c80c9-309">toosee how toouse a Copy Activity toocopy data from an Azure Blob tooAzure SQL, see [Tutorial: Copy data from an Azure Blob tooAzure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="c80c9-310">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="c80c9-310">See Also</span></span>
| <span data-ttu-id="c80c9-311">Temat</span><span class="sxs-lookup"><span data-stu-id="c80c9-311">Topic</span></span> | <span data-ttu-id="c80c9-312">Opis</span><span class="sxs-lookup"><span data-stu-id="c80c9-312">Description</span></span> |
|:--- |:--- |
| [<span data-ttu-id="c80c9-313">Dokumentacja interfejsu API REST usługi Data Factory</span><span class="sxs-lookup"><span data-stu-id="c80c9-313">Data Factory REST API Reference</span></span>](/rest/api/datafactory/) |<span data-ttu-id="c80c9-314">Zobacz pełną dokumentację dotyczącą poleceń cmdlet w usłudze Fabryka danych.</span><span class="sxs-lookup"><span data-stu-id="c80c9-314">See comprehensive documentation on Data Factory cmdlets</span></span> |
| [<span data-ttu-id="c80c9-315">Potoki</span><span class="sxs-lookup"><span data-stu-id="c80c9-315">Pipelines</span></span>](data-factory-create-pipelines.md) |<span data-ttu-id="c80c9-316">Ten artykuł pomaga w zrozumieniu potoki i działań w fabryce danych Azure i w jaki sposób toouse ich tooconstruct end-to-end danymi przepływy pracy dla Twojego scenariusza lub firmy.</span><span class="sxs-lookup"><span data-stu-id="c80c9-316">This article helps you understand pipelines and activities in Azure Data Factory and how toouse them tooconstruct end-to-end data-driven workflows for your scenario or business.</span></span> |
| [<span data-ttu-id="c80c9-317">Zestawy danych</span><span class="sxs-lookup"><span data-stu-id="c80c9-317">Datasets</span></span>](data-factory-create-datasets.md) |<span data-ttu-id="c80c9-318">Ten artykuł ułatwia zapoznanie się z zestawami danych w usłudze Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="c80c9-318">This article helps you understand datasets in Azure Data Factory.</span></span> |
| [<span data-ttu-id="c80c9-319">Planowanie i wykonywanie</span><span class="sxs-lookup"><span data-stu-id="c80c9-319">Scheduling and Execution</span></span>](data-factory-scheduling-and-execution.md) |<span data-ttu-id="c80c9-320">W tym artykule opisano aspekty planowania i wykonywania hello modelu aplikacji fabryki danych Azure.</span><span class="sxs-lookup"><span data-stu-id="c80c9-320">This article explains hello scheduling and execution aspects of Azure Data Factory application model.</span></span> |
| [<span data-ttu-id="c80c9-321">Monitorowanie potoków i zarządzanie nimi za pomocą aplikacji do monitorowania</span><span class="sxs-lookup"><span data-stu-id="c80c9-321">Monitor and manage pipelines using Monitoring App</span></span>](data-factory-monitor-manage-app.md) |<span data-ttu-id="c80c9-322">W tym artykule opisano sposób toomonitor, zarządzania i debugowania potoki przy użyciu hello monitorowanie & aplikacji do zarządzania.</span><span class="sxs-lookup"><span data-stu-id="c80c9-322">This article describes how toomonitor, manage, and debug pipelines using hello Monitoring & Management App.</span></span> |
