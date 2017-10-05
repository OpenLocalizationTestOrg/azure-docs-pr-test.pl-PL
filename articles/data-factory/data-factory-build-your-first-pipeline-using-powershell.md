---
title: Tworzenie pierwszej fabryki danych (PowerShell) | Microsoft Docs
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
ms.openlocfilehash: 40a63339be90d0c5d972605c7f6fa029ca1e2ba4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="tutorial-build-your-first-azure-data-factory-using-azure-powershell"></a><span data-ttu-id="d682f-103">Samouczek: tworzenie pierwszej fabryki danych platformy Azure przy użyciu programu Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="d682f-103">Tutorial: Build your first Azure data factory using Azure PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d682f-104">Przegląd i wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="d682f-104">Overview and prerequisites</span></span>](data-factory-build-your-first-pipeline.md)
> * [<span data-ttu-id="d682f-105">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="d682f-105">Azure portal</span></span>](data-factory-build-your-first-pipeline-using-editor.md)
> * [<span data-ttu-id="d682f-106">Program Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d682f-106">Visual Studio</span></span>](data-factory-build-your-first-pipeline-using-vs.md)
> * [<span data-ttu-id="d682f-107">Program PowerShell</span><span class="sxs-lookup"><span data-stu-id="d682f-107">PowerShell</span></span>](data-factory-build-your-first-pipeline-using-powershell.md)
> * [<span data-ttu-id="d682f-108">Szablon usługi Resource Manager</span><span class="sxs-lookup"><span data-stu-id="d682f-108">Resource Manager Template</span></span>](data-factory-build-your-first-pipeline-using-arm.md)
> * [<span data-ttu-id="d682f-109">Interfejs API REST</span><span class="sxs-lookup"><span data-stu-id="d682f-109">REST API</span></span>](data-factory-build-your-first-pipeline-using-rest-api.md)
>
>

<span data-ttu-id="d682f-110">Ten artykuł opisuje korzystanie z programu Azure PowerShell w celu utworzenia pierwszej fabryki danych platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="d682f-110">In this article, you use Azure PowerShell to create your first Azure data factory.</span></span> <span data-ttu-id="d682f-111">Aby wykonać instrukcje z tego samouczka przy użyciu innych narzędzi/zestawów SDK, wybierz jedną z opcji z listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="d682f-111">To do the tutorial using other tools/SDKs, select one of the options from the drop-down list.</span></span>

<span data-ttu-id="d682f-112">Potok w tym samouczku zawiera jedno działanie: **działanie Hive usługi HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="d682f-112">The pipeline in this tutorial has one activity: **HDInsight Hive activity**.</span></span> <span data-ttu-id="d682f-113">To działanie uruchamia skrypt Hive w klastrze Azure HDInsight, który przekształca dane wejściowe, aby wygenerować dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="d682f-113">This activity runs a hive script on an Azure HDInsight cluster that transforms input data to produce output data.</span></span> <span data-ttu-id="d682f-114">Uruchamianie potoku zaplanowano raz w miesiącu między określonym czasem rozpoczęcia i zakończenia.</span><span class="sxs-lookup"><span data-stu-id="d682f-114">The pipeline is scheduled to run once a month between the specified start and end times.</span></span> 

> [!NOTE]
> <span data-ttu-id="d682f-115">Potok danych przedstawiony w tym samouczku przekształca dane wejściowe w celu wygenerowania danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="d682f-115">The data pipeline in this tutorial transforms input data to produce output data.</span></span> <span data-ttu-id="d682f-116">Nie kopiuje on danych ze źródłowego do docelowego magazynu danych.</span><span class="sxs-lookup"><span data-stu-id="d682f-116">It does not copy data from a source data store to a destination data store.</span></span> <span data-ttu-id="d682f-117">Aby zapoznać się z samouczkiem dotyczącym kopiowania danych przy użyciu usługi Azure Data Factory, zobacz [Tutorial: Copy data from Blob Storage to SQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) (Samouczek: Kopiowanie danych z usługi Blob Storage do usługi SQL Database).</span><span class="sxs-lookup"><span data-stu-id="d682f-117">For a tutorial on how to copy data using Azure Data Factory, see [Tutorial: Copy data from Blob Storage to SQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
> 
> <span data-ttu-id="d682f-118">Potok może obejmować więcej niż jedno działanie.</span><span class="sxs-lookup"><span data-stu-id="d682f-118">A pipeline can have more than one activity.</span></span> <span data-ttu-id="d682f-119">Dwa działania można połączyć w łańcuch (uruchomić jedno działanie po drugim), ustawiając wyjściowy zestaw danych jednego działania jako zestaw wejściowy drugiego.</span><span class="sxs-lookup"><span data-stu-id="d682f-119">And, you can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity.</span></span> <span data-ttu-id="d682f-120">Więcej informacji znajduje się w artykule dotyczącym [planowania i wykonywania w usłudze Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span><span class="sxs-lookup"><span data-stu-id="d682f-120">For more information, see [scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d682f-121">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="d682f-121">Prerequisites</span></span>
* <span data-ttu-id="d682f-122">Przeczytanie artykułu [Omówienie samouczka](data-factory-build-your-first-pipeline.md) oraz wykonanie kroków **wymagań wstępnych**.</span><span class="sxs-lookup"><span data-stu-id="d682f-122">Read through [Tutorial Overview](data-factory-build-your-first-pipeline.md) article and complete the **prerequisite** steps.</span></span>
* <span data-ttu-id="d682f-123">Postępuj zgodnie z instrukcjami w artykule [How to install and configure Azure PowerShell](/powershell/azure/overview) (Instalowanie i konfigurowanie programu Azure PowerShell), aby zainstalować najnowszą wersję programu Azure PowerShell na komputerze.</span><span class="sxs-lookup"><span data-stu-id="d682f-123">Follow instructions in [How to install and configure Azure PowerShell](/powershell/azure/overview) article to install latest version of Azure PowerShell on your computer.</span></span>
* <span data-ttu-id="d682f-124">(opcjonalnie) Ten artykuł nie obejmuje wszystkich poleceń cmdlet dla usługi Fabryka danych.</span><span class="sxs-lookup"><span data-stu-id="d682f-124">(optional) This article does not cover all the Data Factory cmdlets.</span></span> <span data-ttu-id="d682f-125">Pełna dokumentacja dotycząca poleceń cmdlet dla usługi Fabryka danych znajduje się w artykule [Data Factory Cmdlet Reference](/powershell/module/azurerm.datafactories) (Dokumentacja dotycząca poleceń cmdlet dla usługi Fabryka danych).</span><span class="sxs-lookup"><span data-stu-id="d682f-125">See [Data Factory Cmdlet Reference](/powershell/module/azurerm.datafactories) for comprehensive documentation on Data Factory cmdlets.</span></span>

## <a name="create-data-factory"></a><span data-ttu-id="d682f-126">Tworzenie fabryki danych</span><span class="sxs-lookup"><span data-stu-id="d682f-126">Create data factory</span></span>
<span data-ttu-id="d682f-127">W tym kroku opisano użycie programu Azure PowerShell do utworzenia fabryki danych Azure o nazwie **FirstDataFactoryPSH**.</span><span class="sxs-lookup"><span data-stu-id="d682f-127">In this step, you use Azure PowerShell to create an Azure Data Factory named **FirstDataFactoryPSH**.</span></span> <span data-ttu-id="d682f-128">Fabryka danych może obejmować jeden lub wiele potoków.</span><span class="sxs-lookup"><span data-stu-id="d682f-128">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="d682f-129">Potok może obejmować jedno lub wiele działań.</span><span class="sxs-lookup"><span data-stu-id="d682f-129">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="d682f-130">Na przykład działanie kopiowania może służyć do skopiowania danych ze źródła do docelowego magazynu danych, a działanie programu Hive w usłudze HDInsight do uruchomienia skryptu programu Hive, który przekształci dane wejściowe.</span><span class="sxs-lookup"><span data-stu-id="d682f-130">For example, a Copy Activity to copy data from a source to a destination data store and a HDInsight Hive activity to run a Hive script to transform input data.</span></span> <span data-ttu-id="d682f-131">Zacznijmy tworzenie fabryki danych w tym kroku.</span><span class="sxs-lookup"><span data-stu-id="d682f-131">Let's start with creating the data factory in this step.</span></span>

1. <span data-ttu-id="d682f-132">Uruchom program Azure PowerShell i uruchom następujące polecenie.</span><span class="sxs-lookup"><span data-stu-id="d682f-132">Start Azure PowerShell and run the following command.</span></span> <span data-ttu-id="d682f-133">Nie zamykaj programu Azure PowerShell, zanim nie wykonasz wszystkich instrukcji z tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="d682f-133">Keep Azure PowerShell open until the end of this tutorial.</span></span> <span data-ttu-id="d682f-134">Jeśli go zamkniesz i otworzysz ponownie, musisz uruchomić te polecenia jeszcze raz.</span><span class="sxs-lookup"><span data-stu-id="d682f-134">If you close and reopen, you need to run these commands again.</span></span>
   * <span data-ttu-id="d682f-135">Uruchom poniższe polecenie i wprowadź nazwę użytkownika oraz hasło, których używasz do logowania się w witrynie Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="d682f-135">Run the following command and enter the user name and password that you use to sign in to the Azure portal.</span></span>
    ```PowerShell
    Login-AzureRmAccount
    ```    
   * <span data-ttu-id="d682f-136">Uruchom poniższe polecenie, aby wyświetlić wszystkie subskrypcje dla tego konta.</span><span class="sxs-lookup"><span data-stu-id="d682f-136">Run the following command to view all the subscriptions for this account.</span></span>
    ```PowerShell
    Get-AzureRmSubscription 
    ```
   * <span data-ttu-id="d682f-137">Uruchom poniższe polecenie, aby wybrać subskrypcję, z którą chcesz pracować.</span><span class="sxs-lookup"><span data-stu-id="d682f-137">Run the following command to select the subscription that you want to work with.</span></span> <span data-ttu-id="d682f-138">Ta subskrypcja powinna być taka sama jak używana w witrynie Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="d682f-138">This subscription should be the same as the one you used in the Azure portal.</span></span>
    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <SUBSCRIPTION NAME> | Set-AzureRmContext
    ```     
2. <span data-ttu-id="d682f-139">Utwórz grupę zasobów platformy Azure o nazwie **ADFTutorialResourceGroup** przez uruchomienie następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="d682f-139">Create an Azure resource group named **ADFTutorialResourceGroup** by running the following command:</span></span>
    
    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```
    <span data-ttu-id="d682f-140">W niektórych krokach w tym samouczku zakłada się, że używana jest grupa zasobów o nazwie ADFTutorialResourceGroup.</span><span class="sxs-lookup"><span data-stu-id="d682f-140">Some of the steps in this tutorial assume that you use the resource group named ADFTutorialResourceGroup.</span></span> <span data-ttu-id="d682f-141">Jeśli używasz innej grupy zasobów, podczas wykonywania instrukcji w tym samouczku trzeba będzie wstawić jej nazwę zamiast nazwy ADFTutorialResourceGroup.</span><span class="sxs-lookup"><span data-stu-id="d682f-141">If you use a different resource group, you need to use it in place of ADFTutorialResourceGroup in this tutorial.</span></span>
3. <span data-ttu-id="d682f-142">Uruchom polecenie cmdlet **New-AzureRmDataFactory**, aby utworzyć fabrykę danych o nazwie **FirstDataFactoryPSH**.</span><span class="sxs-lookup"><span data-stu-id="d682f-142">Run the **New-AzureRmDataFactory** cmdlet that creates a data factory named **FirstDataFactoryPSH**.</span></span>

    ```PowerShell
    New-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name FirstDataFactoryPSH –Location "West US"
    ```
<span data-ttu-id="d682f-143">Pamiętaj o następujących kwestiach:</span><span class="sxs-lookup"><span data-stu-id="d682f-143">Note the following points:</span></span>

* <span data-ttu-id="d682f-144">Nazwa fabryki danych Azure musi być globalnie unikatowa.</span><span class="sxs-lookup"><span data-stu-id="d682f-144">The name of the Azure Data Factory must be globally unique.</span></span> <span data-ttu-id="d682f-145">Jeśli wystąpi błąd **Nazwa fabryki danych „FirstDataFactoryPSH” jest niedostępna**, zmień nazwę (np. TwojaNazwaFirstDataFactoryPSH).</span><span class="sxs-lookup"><span data-stu-id="d682f-145">If you receive the error **Data factory name “FirstDataFactoryPSH” is not available**, change the name (for example, yournameFirstDataFactoryPSH).</span></span> <span data-ttu-id="d682f-146">Użyj tej nazwy zamiast ADFTutorialFactoryPSH podczas wykonywania kroków w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="d682f-146">Use this name in place of ADFTutorialFactoryPSH while performing steps in this tutorial.</span></span> <span data-ttu-id="d682f-147">Artykuł [Data Factory — Naming Rules](data-factory-naming-rules.md) (Fabryka danych — zasady nazewnictwa) zawiera zasady nazewnictwa artefaktów usługi Fabryka danych.</span><span class="sxs-lookup"><span data-stu-id="d682f-147">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>
* <span data-ttu-id="d682f-148">Aby tworzyć wystąpienia usługi Fabryka danych, musisz być współautorem/administratorem subskrypcji Azure</span><span class="sxs-lookup"><span data-stu-id="d682f-148">To create Data Factory instances, you need to be a contributor/administrator of the Azure subscription</span></span>
* <span data-ttu-id="d682f-149">W przyszłości nazwa fabryki danych może zostać zarejestrowana jako nazwa DNS, a wówczas stanie się widoczna publicznie.</span><span class="sxs-lookup"><span data-stu-id="d682f-149">The name of the data factory may be registered as a DNS name in the future and hence become publically visible.</span></span>
* <span data-ttu-id="d682f-150">Jeśli zostanie wyświetlony komunikat o błędzie: „**Subskrypcja nie jest zarejestrowana w celu używania przestrzeni nazw Microsoft.DataFactory**”, wykonaj jedną z następujących czynności i spróbuj opublikować ponownie:</span><span class="sxs-lookup"><span data-stu-id="d682f-150">If you receive the error: "**This subscription is not registered to use namespace Microsoft.DataFactory**", do one of the following and try publishing again:</span></span>

  * <span data-ttu-id="d682f-151">W programie Azure PowerShell uruchom następujące polecenie, aby zarejestrować dostawcę usługi Data Factory:</span><span class="sxs-lookup"><span data-stu-id="d682f-151">In Azure PowerShell, run the following command to register the Data Factory provider:</span></span>

    ```PowerShell
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```
      <span data-ttu-id="d682f-152">Możesz uruchomić następujące polecenie, aby potwierdzić, że dostawca usługi Fabryka danych jest zarejestrowany:</span><span class="sxs-lookup"><span data-stu-id="d682f-152">You can run the following command to confirm that the Data Factory provider is registered:</span></span>

    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * <span data-ttu-id="d682f-153">Zaloguj się przy użyciu subskrypcji Azure do [portalu Azure](https://portal.azure.com) i przejdź do bloku Fabryka danych lub utwórz fabrykę danych w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="d682f-153">Login using the Azure subscription into the [Azure portal](https://portal.azure.com) and navigate to a Data Factory blade (or) create a data factory in the Azure portal.</span></span> <span data-ttu-id="d682f-154">Ta akcja powoduje automatyczne zarejestrowanie dostawcy.</span><span class="sxs-lookup"><span data-stu-id="d682f-154">This action automatically registers the provider for you.</span></span>

<span data-ttu-id="d682f-155">Przed utworzeniem potoku musisz utworzyć kilka jednostek usługi Fabryka danych.</span><span class="sxs-lookup"><span data-stu-id="d682f-155">Before creating a pipeline, you need to create a few Data Factory entities first.</span></span> <span data-ttu-id="d682f-156">Najpierw utwórz połączone usługi, aby połączyć usługi magazynu danych/usługi obliczeniowe ze swoim magazynem danych, zdefiniuj wejściowe i wyjściowe zestawy danych do reprezentowania danych wejściowych/wyjściowych w połączonych magazynach danych, a następnie utwórz potok zawierający działanie, które korzysta z tych zestawów danych.</span><span class="sxs-lookup"><span data-stu-id="d682f-156">You first create linked services to link data stores/computes to your data store, define input and output datasets to represent input/output data in linked data stores, and then create the pipeline with an activity that uses these datasets.</span></span>

## <a name="create-linked-services"></a><span data-ttu-id="d682f-157">Tworzenie połączonych usług</span><span class="sxs-lookup"><span data-stu-id="d682f-157">Create linked services</span></span>
<span data-ttu-id="d682f-158">W tym kroku opisano połączenie konta usługi Azure Storage oraz klastra Azure HDInsight na żądanie z fabryką danych.</span><span class="sxs-lookup"><span data-stu-id="d682f-158">In this step, you link your Azure Storage account and an on-demand Azure HDInsight cluster to your data factory.</span></span> <span data-ttu-id="d682f-159">Konto usługi Azure Storage będzie przechowywać dane wejściowe i wyjściowe dla potoku w tym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="d682f-159">The Azure Storage account holds the input and output data for the pipeline in this sample.</span></span> <span data-ttu-id="d682f-160">Połączona usługa HDInsight służy do uruchamiania skryptu programu Hive określonego w działaniu potoku w tym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="d682f-160">The HDInsight linked service is used to run a Hive script specified in the activity of the pipeline in this sample.</span></span> <span data-ttu-id="d682f-161">Zidentyfikuj usługi magazynu danych/usługi obliczeniowe, które są używane w tym scenariuszu, oraz połącz te usługi z fabryką danych przez utworzenie połączonych usług.</span><span class="sxs-lookup"><span data-stu-id="d682f-161">Identify what data store/compute services are used in your scenario and link those services to the data factory by creating linked services.</span></span>

### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="d682f-162">Tworzenie połączonej usługi Azure Storage</span><span class="sxs-lookup"><span data-stu-id="d682f-162">Create Azure Storage linked service</span></span>
<span data-ttu-id="d682f-163">W tym kroku opisano łączenie konta usługi Azure Storage z fabryką danych.</span><span class="sxs-lookup"><span data-stu-id="d682f-163">In this step, you link your Azure Storage account to your data factory.</span></span> <span data-ttu-id="d682f-164">Do przechowywania danych wejściowych/wyjściowych oraz pliku skryptu HQL używa się tego samego konta usługi Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="d682f-164">You use the same Azure Storage account to store input/output data and the HQL script file.</span></span>

1. <span data-ttu-id="d682f-165">W folderze C:\ADFGetStarted utwórz plik JSON o nazwie StorageLinkedService.json o następującej zawartości.</span><span class="sxs-lookup"><span data-stu-id="d682f-165">Create a JSON file named StorageLinkedService.json in the C:\ADFGetStarted folder with the following content.</span></span> <span data-ttu-id="d682f-166">Utwórz folder ADFGetStarted, jeśli jeszcze nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="d682f-166">Create the folder ADFGetStarted if it does not already exist.</span></span>

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
    <span data-ttu-id="d682f-167">Zastąp wartość **account name** nazwą konta usługi Azure Storage oraz wartość **account key** kluczem dostępu konta usługi Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="d682f-167">Replace **account name** with the name of your Azure storage account and **account key** with the access key of the Azure storage account.</span></span> <span data-ttu-id="d682f-168">Aby dowiedzieć się, jak uzyskać klucz dostępu do magazynu, zapoznaj się z informacjami na temat sposobów wyświetlania, kopiowania i ponownego generowania kluczy dostępu do magazynu w sekcji [Zarządzanie kontem magazynu](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="d682f-168">To learn how to get your storage access key, see the information about how to view, copy, and regenerate storage access keys in [Manage your storage account](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>
2. <span data-ttu-id="d682f-169">W programie PowerShell Azure przejdź do folderu ADFGetStarted.</span><span class="sxs-lookup"><span data-stu-id="d682f-169">In Azure PowerShell, switch to the ADFGetStarted folder.</span></span>
3. <span data-ttu-id="d682f-170">Możesz użyć polecenia cmdlet **New-AzureRmDataFactoryLinkedService**, aby utworzyć połączoną usługę.</span><span class="sxs-lookup"><span data-stu-id="d682f-170">You can use the **New-AzureRmDataFactoryLinkedService** cmdlet that creates a linked service.</span></span> <span data-ttu-id="d682f-171">To polecenie cmdlet i inne polecenia cmdlet usługi Data Factory używane w tym samouczku wymagają przekazania wartości dla parametrów *ResourceGroupName* i *DataFactoryName*.</span><span class="sxs-lookup"><span data-stu-id="d682f-171">This cmdlet and other Data Factory cmdlets you use in this tutorial requires you to pass values for the *ResourceGroupName* and *DataFactoryName* parameters.</span></span> <span data-ttu-id="d682f-172">Możesz też użyć polecenia **Get-AzureRmDataFactory**, aby pobrać obiekt **DataFactory** i przekazać obiekt bez wpisywania parametrów *ResourceGroupName* i *DataFactoryName* za każdym razem, gdy uruchamiasz polecenie cmdlet.</span><span class="sxs-lookup"><span data-stu-id="d682f-172">Alternatively, you can use **Get-AzureRmDataFactory** to get a **DataFactory** object and pass the object without typing *ResourceGroupName* and *DataFactoryName* each time you run a cmdlet.</span></span> <span data-ttu-id="d682f-173">Uruchom następujące polecenie, aby przypisać dane wyjściowe polecenia cmdlet **Get-AzureRmDataFactory** do zmiennej **$df**.</span><span class="sxs-lookup"><span data-stu-id="d682f-173">Run the following command to assign the output of the **Get-AzureRmDataFactory** cmdlet to a **$df** variable.</span></span>

    ```PowerShell
    $df=Get-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name FirstDataFactoryPSH
    ```
4. <span data-ttu-id="d682f-174">Teraz uruchom polecenie cmdlet **New-AzureRmDataFactoryLinkedService**, aby utworzyć połączoną usługę **StorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="d682f-174">Now, run the **New-AzureRmDataFactoryLinkedService** cmdlet that creates the linked **StorageLinkedService** service.</span></span>

    ```PowerShell
    New-AzureRmDataFactoryLinkedService $df -File .\StorageLinkedService.json
    ```
    <span data-ttu-id="d682f-175">Jeśli polecenie cmdlet **Get-AzureRmDataFactory** nie zostało uruchomione i nie przypisano danych wyjściowych do zmiennej **$df**, trzeba określić wartości dla parametrów *ResourceGroupName* i *DataFactoryName* w następujący sposób.</span><span class="sxs-lookup"><span data-stu-id="d682f-175">If you hadn't run the **Get-AzureRmDataFactory** cmdlet and assigned the output to the **$df** variable, you would have to specify values for the *ResourceGroupName* and *DataFactoryName* parameters as follows.</span></span>

    ```PowerShell
    New-AzureRmDataFactoryLinkedService -ResourceGroupName ADFTutorialResourceGroup -DataFactoryName FirstDataFactoryPSH -File .\StorageLinkedService.json
    ```
    <span data-ttu-id="d682f-176">Jeśli zamkniesz program Azure PowerShell w trakcie wykonywania samouczka, w celu dokończenia go trzeba będzie uruchomić polecenie cmdlet **Get-AzureRmDataFactory** po następnym uruchomieniu programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d682f-176">If you close Azure PowerShell in the middle of the tutorial, you have to run the **Get-AzureRmDataFactory** cmdlet next time you start Azure PowerShell to complete the tutorial.</span></span>

### <a name="create-azure-hdinsight-linked-service"></a><span data-ttu-id="d682f-177">Tworzenie połączonej usługi Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="d682f-177">Create Azure HDInsight linked service</span></span>
<span data-ttu-id="d682f-178">W tym kroku przedstawiono łączenie klastra usługi HDInsight na żądanie z fabryką danych.</span><span class="sxs-lookup"><span data-stu-id="d682f-178">In this step, you link an on-demand HDInsight cluster to your data factory.</span></span> <span data-ttu-id="d682f-179">Klaster usługi HDInsight jest automatycznie tworzony w czasie wykonywania oraz usuwany po zakończeniu przetwarzania i określonym czasie bezczynności.</span><span class="sxs-lookup"><span data-stu-id="d682f-179">The HDInsight cluster is automatically created at runtime and deleted after it is done processing and idle for the specified amount of time.</span></span> <span data-ttu-id="d682f-180">Możesz użyć własnego klastra usługi HDInsight zamiast klastra usługi HDInsight na żądanie.</span><span class="sxs-lookup"><span data-stu-id="d682f-180">You could use your own HDInsight cluster instead of using an on-demand HDInsight cluster.</span></span> <span data-ttu-id="d682f-181">Szczegółowe informacje znajdują się w artykule [Compute Linked Services](data-factory-compute-linked-services.md) (Połączone usługi obliczeniowe).</span><span class="sxs-lookup"><span data-stu-id="d682f-181">See [Compute Linked Services](data-factory-compute-linked-services.md) for details.</span></span>

1. <span data-ttu-id="d682f-182">W folderze **C:\ADFGetStarted** utwórz plik JSON o nazwie **HDInsightOnDemandLinkedService**.json o następującej zawartości.</span><span class="sxs-lookup"><span data-stu-id="d682f-182">Create a JSON file named **HDInsightOnDemandLinkedService**.json in the **C:\ADFGetStarted** folder with the following content.</span></span>

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
    <span data-ttu-id="d682f-183">Poniższa tabela zawiera opis właściwości kodu JSON użytych w tym fragmencie kodu:</span><span class="sxs-lookup"><span data-stu-id="d682f-183">The following table provides descriptions for the JSON properties used in the snippet:</span></span>

   | <span data-ttu-id="d682f-184">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d682f-184">Property</span></span> | <span data-ttu-id="d682f-185">Opis</span><span class="sxs-lookup"><span data-stu-id="d682f-185">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="d682f-186">ClusterSize</span><span class="sxs-lookup"><span data-stu-id="d682f-186">ClusterSize</span></span> |<span data-ttu-id="d682f-187">Określa rozmiar klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d682f-187">Specifies the size of the HDInsight cluster.</span></span> |
   | <span data-ttu-id="d682f-188">TimeToLive</span><span class="sxs-lookup"><span data-stu-id="d682f-188">TimeToLive</span></span> |<span data-ttu-id="d682f-189">Określa czas bezczynności, po którym klaster usługi HDInsight zostanie usunięty.</span><span class="sxs-lookup"><span data-stu-id="d682f-189">Specifies that the idle time for the HDInsight cluster, before it is deleted.</span></span> |
   | <span data-ttu-id="d682f-190">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="d682f-190">linkedServiceName</span></span> |<span data-ttu-id="d682f-191">Określa konto magazynu używane do przechowywania dzienników generowanych w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d682f-191">Specifies the storage account that is used to store the logs that are generated by HDInsight</span></span> |

    <span data-ttu-id="d682f-192">Pamiętaj o następujących kwestiach:</span><span class="sxs-lookup"><span data-stu-id="d682f-192">Note the following points:</span></span>

   * <span data-ttu-id="d682f-193">Usługa Data Factory tworzy klaster usługi HDInsight **oparty na systemie Linux** za pomocą kodu JSON.</span><span class="sxs-lookup"><span data-stu-id="d682f-193">The Data Factory creates a **Linux-based** HDInsight cluster for you with the JSON.</span></span> <span data-ttu-id="d682f-194">Szczegółowe informacje znajdują się w artykule [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) (Połączona usługa HDInsight na żądanie).</span><span class="sxs-lookup"><span data-stu-id="d682f-194">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>
   * <span data-ttu-id="d682f-195">Możesz użyć **własnego klastra usługi HDInsight** zamiast klastra usługi HDInsight na żądanie.</span><span class="sxs-lookup"><span data-stu-id="d682f-195">You could use **your own HDInsight cluster** instead of using an on-demand HDInsight cluster.</span></span> <span data-ttu-id="d682f-196">Szczegółowe informacje znajdują się w artykule [HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) (Połączona usługa HDInsight).</span><span class="sxs-lookup"><span data-stu-id="d682f-196">See [HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) for details.</span></span>
   * <span data-ttu-id="d682f-197">Klaster usługi HDInsight tworzy **kontener domyślny** w magazynie obiektów blob określonym w kodzie JSON (**linkedServiceName**).</span><span class="sxs-lookup"><span data-stu-id="d682f-197">The HDInsight cluster creates a **default container** in the blob storage you specified in the JSON (**linkedServiceName**).</span></span> <span data-ttu-id="d682f-198">Usługa HDInsight nie powoduje usunięcia tego kontenera w przypadku usunięcia klastra.</span><span class="sxs-lookup"><span data-stu-id="d682f-198">HDInsight does not delete this container when the cluster is deleted.</span></span> <span data-ttu-id="d682f-199">To zachowanie jest celowe.</span><span class="sxs-lookup"><span data-stu-id="d682f-199">This behavior is by design.</span></span> <span data-ttu-id="d682f-200">W przypadku połączonej usługi HDInsight na żądanie klaster usługi HDInsight jest tworzony przy każdym przetwarzaniu wycinka — o ile w tym momencie nie istnieje aktywny klaster (**timeToLive**).</span><span class="sxs-lookup"><span data-stu-id="d682f-200">With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice is processed unless there is an existing live cluster (**timeToLive**).</span></span> <span data-ttu-id="d682f-201">Klaster jest automatycznie usuwany po zakończeniu przetwarzania.</span><span class="sxs-lookup"><span data-stu-id="d682f-201">The cluster is automatically deleted when the processing is done.</span></span>

       <span data-ttu-id="d682f-202">Po przetworzeniu większej liczby wycinków w usłudze Azure Blob Storage będzie widocznych wiele kontenerów.</span><span class="sxs-lookup"><span data-stu-id="d682f-202">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="d682f-203">Jeśli nie są potrzebne do rozwiązywania problemów z zadaniami, można je usunąć, aby zmniejszyć koszt przechowywania.</span><span class="sxs-lookup"><span data-stu-id="d682f-203">If you do not need them for troubleshooting of the jobs, you may want to delete them to reduce the storage cost.</span></span> <span data-ttu-id="d682f-204">Nazwy tych kontenerów są zgodne ze wzorcem: „adf**twojanazwafabrykidanych**-**nazwapołączonejusługi**-znacznikdatygodziny”.</span><span class="sxs-lookup"><span data-stu-id="d682f-204">The names of these containers follow a pattern: "adf**yourdatafactoryname**-**linkedservicename**-datetimestamp".</span></span> <span data-ttu-id="d682f-205">Aby usunąć kontenery z usługi Azure Blob Storage, użyj takich narzędzi, jak [Microsoft Storage Explorer](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="d682f-205">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) to delete containers in your Azure blob storage.</span></span>

     <span data-ttu-id="d682f-206">Szczegółowe informacje znajdują się w artykule [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) (Połączona usługa HDInsight na żądanie).</span><span class="sxs-lookup"><span data-stu-id="d682f-206">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>
2. <span data-ttu-id="d682f-207">Uruchom polecenie cmdlet **New-AzureRmDataFactoryLinkedService**, aby utworzyć połączoną usługę o nazwie HDInsightOnDemandLinkedService.</span><span class="sxs-lookup"><span data-stu-id="d682f-207">Run the **New-AzureRmDataFactoryLinkedService** cmdlet that creates the linked service called HDInsightOnDemandLinkedService.</span></span>
    
    ```PowerShell
    New-AzureRmDataFactoryLinkedService $df -File .\HDInsightOnDemandLinkedService.json
    ```

## <a name="create-datasets"></a><span data-ttu-id="d682f-208">Tworzenie zestawów danych</span><span class="sxs-lookup"><span data-stu-id="d682f-208">Create datasets</span></span>
<span data-ttu-id="d682f-209">W tym kroku opisano tworzenie zestawów danych do reprezentowania danych wejściowych i wyjściowych na potrzeby przetwarzania przy użyciu programu Hive.</span><span class="sxs-lookup"><span data-stu-id="d682f-209">In this step, you create datasets to represent the input and output data for Hive processing.</span></span> <span data-ttu-id="d682f-210">Te zestawy danych dotyczą elementu **StorageLinkedService** utworzonego wcześniej w ramach tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="d682f-210">These datasets refer to the **StorageLinkedService** you have created earlier in this tutorial.</span></span> <span data-ttu-id="d682f-211">Połączona usługa wskazuje konto usługi Azure Storage, a zestawy danych określają kontener, folder i nazwę pliku w magazynie, w którym przechowywane są dane wejściowe i wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="d682f-211">The linked service points to an Azure Storage account and datasets specify container, folder, file name in the storage that holds input and output data.</span></span>

### <a name="create-input-dataset"></a><span data-ttu-id="d682f-212">Tworzenie wejściowego zestawu danych</span><span class="sxs-lookup"><span data-stu-id="d682f-212">Create input dataset</span></span>
1. <span data-ttu-id="d682f-213">W folderze **C:\ADFGetStarted**twórz plik JSON o nazwie **InputTable.json** o następującej zawartości:</span><span class="sxs-lookup"><span data-stu-id="d682f-213">Create a JSON file named **InputTable.json** in the **C:\ADFGetStarted** folder with the following content:</span></span>

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
    <span data-ttu-id="d682f-214">Ten kod JSON definiuje zestaw danych o nazwie **AzureBlobInput**, który reprezentuje dane wejściowe dla działania w potoku.</span><span class="sxs-lookup"><span data-stu-id="d682f-214">The JSON defines a dataset named **AzureBlobInput**, which represents input data for an activity in the pipeline.</span></span> <span data-ttu-id="d682f-215">Ponadto określa, że dane wejściowe znajdują się w kontenerze obiektów blob o nazwie **adfgetstarted** oraz w folderze o nazwie **inputdata**.</span><span class="sxs-lookup"><span data-stu-id="d682f-215">In addition, it specifies that the input data is located in the blob container called **adfgetstarted** and the folder called **inputdata**.</span></span>

    <span data-ttu-id="d682f-216">Poniższa tabela zawiera opis właściwości kodu JSON użytych w tym fragmencie kodu:</span><span class="sxs-lookup"><span data-stu-id="d682f-216">The following table provides descriptions for the JSON properties used in the snippet:</span></span>

   | <span data-ttu-id="d682f-217">Właściwość</span><span class="sxs-lookup"><span data-stu-id="d682f-217">Property</span></span> | <span data-ttu-id="d682f-218">Opis</span><span class="sxs-lookup"><span data-stu-id="d682f-218">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="d682f-219">type</span><span class="sxs-lookup"><span data-stu-id="d682f-219">type</span></span> |<span data-ttu-id="d682f-220">Właściwość type jest ustawiona na wartość AzureBlob, ponieważ dane znajdują się w magazynie obiektów blob Azure.</span><span class="sxs-lookup"><span data-stu-id="d682f-220">The type property is set to AzureBlob because data resides in Azure blob storage.</span></span> |
   | <span data-ttu-id="d682f-221">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="d682f-221">linkedServiceName</span></span> |<span data-ttu-id="d682f-222">Odnosi się do elementu StorageLinkedService utworzonego wcześniej.</span><span class="sxs-lookup"><span data-stu-id="d682f-222">refers to the StorageLinkedService you created earlier.</span></span> |
   | <span data-ttu-id="d682f-223">fileName</span><span class="sxs-lookup"><span data-stu-id="d682f-223">fileName</span></span> |<span data-ttu-id="d682f-224">Ta właściwość jest opcjonalna.</span><span class="sxs-lookup"><span data-stu-id="d682f-224">This property is optional.</span></span> <span data-ttu-id="d682f-225">Jeśli tę właściwość pominiesz, zostaną wybrane wszystkie pliki z folderu folderPath.</span><span class="sxs-lookup"><span data-stu-id="d682f-225">If you omit this property, all the files from the folderPath are picked.</span></span> <span data-ttu-id="d682f-226">W tym przypadku zostanie przetworzony tylko plik input.log.</span><span class="sxs-lookup"><span data-stu-id="d682f-226">In this case, only the input.log is processed.</span></span> |
   | <span data-ttu-id="d682f-227">type</span><span class="sxs-lookup"><span data-stu-id="d682f-227">type</span></span> |<span data-ttu-id="d682f-228">Pliki dziennika są w formacie tekstowym, więc używana jest wartość TextFormat.</span><span class="sxs-lookup"><span data-stu-id="d682f-228">The log files are in text format, so we use TextFormat.</span></span> |
   | <span data-ttu-id="d682f-229">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="d682f-229">columnDelimiter</span></span> |<span data-ttu-id="d682f-230">Kolumny w plikach dziennika są rozdzielane przecinkami (,).</span><span class="sxs-lookup"><span data-stu-id="d682f-230">columns in the log files are delimited by the comma character (,).</span></span> |
   | <span data-ttu-id="d682f-231">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="d682f-231">frequency/interval</span></span> |<span data-ttu-id="d682f-232">Właściwość frequency (częstotliwość) jest ustawiona na wartość Month (Miesiąc), a wartość interwału wynosi 1, co oznacza, że wycinki wejściowe są dostępne co miesiąc.</span><span class="sxs-lookup"><span data-stu-id="d682f-232">frequency set to Month and interval is 1, which means that the input slices are available monthly.</span></span> |
   | <span data-ttu-id="d682f-233">external</span><span class="sxs-lookup"><span data-stu-id="d682f-233">external</span></span> |<span data-ttu-id="d682f-234">Ta właściwość ma wartość true (prawda), jeśli dane wejściowe nie są generowane przez usługę Fabryka danych.</span><span class="sxs-lookup"><span data-stu-id="d682f-234">this property is set to true if the input data is not generated by the Data Factory service.</span></span> |
2. <span data-ttu-id="d682f-235">Uruchom następujące polecenie w programie Azure PowerShell, aby utworzyć zestaw danych usługi Data Factory:</span><span class="sxs-lookup"><span data-stu-id="d682f-235">Run the following command in Azure PowerShell to create the Data Factory dataset:</span></span>

    ```PowerShell
    New-AzureRmDataFactoryDataset $df -File .\InputTable.json
    ```

### <a name="create-output-dataset"></a><span data-ttu-id="d682f-236">Tworzenie wyjściowego zestawu danych</span><span class="sxs-lookup"><span data-stu-id="d682f-236">Create output dataset</span></span>
<span data-ttu-id="d682f-237">Teraz utworzysz wyjściowy zestaw danych do reprezentowania danych wyjściowych przechowywanych w usłudze Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="d682f-237">Now, you create the output dataset to represent the output data stored in the Azure Blob storage.</span></span>

1. <span data-ttu-id="d682f-238">W folderze **C:\ADFGetStarted**twórz plik JSON o nazwie **OutputTable.json** o następującej zawartości:</span><span class="sxs-lookup"><span data-stu-id="d682f-238">Create a JSON file named **OutputTable.json** in the **C:\ADFGetStarted** folder with the following content:</span></span>

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
    <span data-ttu-id="d682f-239">Ten kod JSON definiuje zestaw danych o nazwie **AzureBlobOutput**, który reprezentuje dane wyjściowe dla działania w potoku.</span><span class="sxs-lookup"><span data-stu-id="d682f-239">The JSON defines a dataset named **AzureBlobOutput**, which represents output data for an activity in the pipeline.</span></span> <span data-ttu-id="d682f-240">Ponadto określa, że wyniki są przechowywane w kontenerze obiektów blob o nazwie **adfgetstarted** oraz folderze o nazwie **partitioneddata**.</span><span class="sxs-lookup"><span data-stu-id="d682f-240">In addition, it specifies that the results are stored in the blob container called **adfgetstarted** and the folder called **partitioneddata**.</span></span> <span data-ttu-id="d682f-241">W sekcji **availability** (dostępność) określono, że wyjściowy zestaw danych jest generowany co miesiąc.</span><span class="sxs-lookup"><span data-stu-id="d682f-241">The **availability** section specifies that the output dataset is produced on a monthly basis.</span></span>
2. <span data-ttu-id="d682f-242">Uruchom następujące polecenie w programie Azure PowerShell, aby utworzyć zestaw danych usługi Data Factory:</span><span class="sxs-lookup"><span data-stu-id="d682f-242">Run the following command in Azure PowerShell to create the Data Factory dataset:</span></span>

    ```PowerShell
    New-AzureRmDataFactoryDataset $df -File .\OutputTable.json
    ```

## <a name="create-pipeline"></a><span data-ttu-id="d682f-243">Tworzenie potoku</span><span class="sxs-lookup"><span data-stu-id="d682f-243">Create pipeline</span></span>
<span data-ttu-id="d682f-244">W tym kroku opisano tworzenie pierwszego potoku za pomocą działania **HDInsightHive**.</span><span class="sxs-lookup"><span data-stu-id="d682f-244">In this step, you create your first pipeline with a **HDInsightHive** activity.</span></span> <span data-ttu-id="d682f-245">Wycinek danych wejściowych jest dostępny co miesiąc (frequency: Month, interval: 1), wycinek danych wyjściowych jest generowany co miesiąc, a właściwość scheduler dla działania jest również ustawiona na wartość miesięczną.</span><span class="sxs-lookup"><span data-stu-id="d682f-245">Input slice is available monthly (frequency: Month, interval: 1), output slice is produced monthly, and the scheduler property for the activity is also set to monthly.</span></span> <span data-ttu-id="d682f-246">Ustawienia dla wyjściowego zestawu danych i harmonogramu działania muszą być zgodne.</span><span class="sxs-lookup"><span data-stu-id="d682f-246">The settings for the output dataset and the activity scheduler must match.</span></span> <span data-ttu-id="d682f-247">W tym przypadku wyjściowy zestaw danych jest elementem wpływającym na ustawienia harmonogramu, więc musisz utworzyć wyjściowy zestaw danych nawet wtedy, gdy działanie nie generuje żadnych danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="d682f-247">Currently, output dataset is what drives the schedule, so you must create an output dataset even if the activity does not produce any output.</span></span> <span data-ttu-id="d682f-248">Jeśli w działaniu nie są używane żadne dane wejściowe, możesz pominąć tworzenie zestawu danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="d682f-248">If the activity doesn't take any input, you can skip creating the input dataset.</span></span> <span data-ttu-id="d682f-249">Właściwości użyte w poniższym fragmencie kodu JSON zostały wyjaśnione na końcu tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="d682f-249">The properties used in the following JSON are explained at the end of this section.</span></span>

1. <span data-ttu-id="d682f-250">W folderze C:\ADFGetStarted utwórz plik JSON o nazwie MyFirstPipelinePSH.json o następującej zawartości:</span><span class="sxs-lookup"><span data-stu-id="d682f-250">Create a JSON file named MyFirstPipelinePSH.json in the C:\ADFGetStarted folder with the following content:</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="d682f-251">Zastąp wartość **storageaccountname** w kodzie JSON nazwą swojego konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="d682f-251">Replace **storageaccountname** with the name of your storage account in the JSON.</span></span>
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
    <span data-ttu-id="d682f-252">Ten fragment kodu JSON służy do utworzenia potoku obejmującego jedno działanie, które korzysta z programu Hive do przetwarzania danych w klastrze usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d682f-252">In the JSON snippet, you are creating a pipeline that consists of a single activity that uses Hive to process Data on an HDInsight cluster.</span></span>

    <span data-ttu-id="d682f-253">Plik skryptu programu Hive **partitionweblogs.hql** jest przechowywany na koncie usługi Azure Storage (określonym za pomocą elementu scriptLinkedService o nazwie **StorageLinkedService**) oraz w folderze **script** w kontenerze **adfgetstarted**.</span><span class="sxs-lookup"><span data-stu-id="d682f-253">The Hive script file, **partitionweblogs.hql**, is stored in the Azure storage account (specified by the scriptLinkedService, called **StorageLinkedService**), and in **script** folder in the container **adfgetstarted**.</span></span>

    <span data-ttu-id="d682f-254">Sekcja **defines** służy do określenia ustawień środowiska uruchomieniowego, które zostaną przekazane do skryptu programu Hive w formie wartości konfiguracyjnych programu Hive (np. ${hiveconf:inputtable}, ${hiveconf:partitionedtable}).</span><span class="sxs-lookup"><span data-stu-id="d682f-254">The **defines** section is used to specify the runtime settings that be passed to the hive script as Hive configuration values (e.g ${hiveconf:inputtable}, ${hiveconf:partitionedtable}).</span></span>

    <span data-ttu-id="d682f-255">Właściwości **start** i **end** potoku określają aktywny okres potoku.</span><span class="sxs-lookup"><span data-stu-id="d682f-255">The **start** and **end** properties of the pipeline specifies the active period of the pipeline.</span></span>

    <span data-ttu-id="d682f-256">W kodzie JSON dotyczącym działania określasz, że skrypt programu Hive jest uruchamiany w usłudze obliczeniowej określonej przez właściwość **linkedServiceName** — **HDInsightOnDemandLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="d682f-256">In the activity JSON, you specify that the Hive script runs on the compute specified by the **linkedServiceName** – **HDInsightOnDemandLinkedService**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="d682f-257">Aby uzyskać szczegółowe informacje na temat właściwości kodu JSON używanych w przykładzie, zobacz sekcję „Pipeline JSON” (Kod JSON potoku) w temacie [Pipelines and activities in Azure Data Factory](data-factory-create-pipelines.md) (Potoki i działania w usłudze Azure Data Factory).</span><span class="sxs-lookup"><span data-stu-id="d682f-257">See "Pipeline JSON" in [Pipelines and activities in Azure Data Factory](data-factory-create-pipelines.md) for details about JSON properties that are used in the example.</span></span>

2. <span data-ttu-id="d682f-258">Upewnij się, że plik **input.log** jest wyświetlany w folderze **adfgetstarted/inputdata** w magazynie obiektów blob Azure, i uruchom następujące polecenie, aby wdrożyć potok.</span><span class="sxs-lookup"><span data-stu-id="d682f-258">Confirm that you see the **input.log** file in the **adfgetstarted/inputdata** folder in the Azure blob storage, and run the following command to deploy the pipeline.</span></span> <span data-ttu-id="d682f-259">Ponieważ właściwości **start** i **end** są ustawione na wartość w przeszłości i właściwość **isPaused** została ustawiona na wartość „false”, potok (działanie w potoku) jest uruchamiany natychmiast po wdrożeniu.</span><span class="sxs-lookup"><span data-stu-id="d682f-259">Since the **start** and **end** times are set in the past and **isPaused** is set to false, the pipeline (activity in the pipeline) runs immediately after you deploy.</span></span>

    ```PowerShell
    New-AzureRmDataFactoryPipeline $df -File .\MyFirstPipelinePSH.json
    ```
3. <span data-ttu-id="d682f-260">Gratulacje! Udało Ci się utworzyć pierwszy potok przy użyciu programu Azure PowerShell!</span><span class="sxs-lookup"><span data-stu-id="d682f-260">Congratulations, you have successfully created your first pipeline using Azure PowerShell!</span></span>

## <a name="monitor-pipeline"></a><span data-ttu-id="d682f-261">Monitorowanie potoku</span><span class="sxs-lookup"><span data-stu-id="d682f-261">Monitor pipeline</span></span>
<span data-ttu-id="d682f-262">W tym kroku opisano użycie programu Azure PowerShell do monitorowania tego, co dzieje się w fabryce danych platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="d682f-262">In this step, you use Azure PowerShell to monitor what’s going on in an Azure data factory.</span></span>

1. <span data-ttu-id="d682f-263">Uruchom polecenie **Get-AzureRmDataFactory** i przypisz dane wyjściowe do zmiennej **$df**.</span><span class="sxs-lookup"><span data-stu-id="d682f-263">Run **Get-AzureRmDataFactory** and assign the output to a **$df** variable.</span></span>

    ```PowerShell
    $df=Get-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name FirstDataFactoryPSH
    ```
2. <span data-ttu-id="d682f-264">Uruchom polecenie **Get-AzureRmDataFactorySlice**, aby uzyskać szczegółowe informacje na temat wszystkich wycinków elementu **EmpSQLTable**, który stanowi tabelę wyjściową potoku.</span><span class="sxs-lookup"><span data-stu-id="d682f-264">Run **Get-AzureRmDataFactorySlice** to get details about all slices of the **EmpSQLTable**, which is the output table of the pipeline.</span></span>

    ```PowerShell
    Get-AzureRmDataFactorySlice $df -DatasetName AzureBlobOutput -StartDateTime 2017-07-01
    ```
    <span data-ttu-id="d682f-265">Zauważ, że określana tutaj właściwość StartDateTime oznacza taki sam czas rozpoczęcia jak określony w potoku JSON.</span><span class="sxs-lookup"><span data-stu-id="d682f-265">Notice that the StartDateTime you specify here is the same start time specified in the pipeline JSON.</span></span> <span data-ttu-id="d682f-266">Oto przykładowe dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="d682f-266">Here is the sample output:</span></span>

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
3. <span data-ttu-id="d682f-267">Uruchom polecenie **Get-AzureRmDataFactoryRun**, aby uzyskać szczegółowe informacje o uruchomieniach działania dla określonego wycinka.</span><span class="sxs-lookup"><span data-stu-id="d682f-267">Run **Get-AzureRmDataFactoryRun** to get the details of activity runs for a specific slice.</span></span>

    ```PowerShell
    Get-AzureRmDataFactoryRun $df -DatasetName AzureBlobOutput -StartDateTime 2017-07-01
    ```

    <span data-ttu-id="d682f-268">Oto przykładowe dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="d682f-268">Here is the sample output:</span></span> 

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
    <span data-ttu-id="d682f-269">Możesz kontynuować uruchamianie tego polecenia cmdlet do momentu, gdy wycinek będzie widoczny w stanie **Gotowe** lub **Niepowodzenie**.</span><span class="sxs-lookup"><span data-stu-id="d682f-269">You can keep running this cmdlet until you see the slice in **Ready** state or **Failed** state.</span></span> <span data-ttu-id="d682f-270">Gdy wycinek będzie w stanie Gotowe, sprawdź folder **partitioneddata** w kontenerze **adfgetstarted** w magazynie obiektów blob pod kątem danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="d682f-270">When the slice is in Ready state, check the **partitioneddata** folder in the **adfgetstarted** container in your blob storage for the output data.</span></span>  <span data-ttu-id="d682f-271">Tworzenie klastra usługi HDInsight na żądanie zwykle zajmuje trochę czasu.</span><span class="sxs-lookup"><span data-stu-id="d682f-271">Creation of an on-demand HDInsight cluster usually takes some time.</span></span>

    ![Dane wyjściowe](./media/data-factory-build-your-first-pipeline-using-powershell/three-ouptut-files.png)

> [!IMPORTANT]
> <span data-ttu-id="d682f-273">Tworzenie klastra usługi HDInsight na żądanie zwykle trwa trochę czasu (około 20 minut).</span><span class="sxs-lookup"><span data-stu-id="d682f-273">Creation of an on-demand HDInsight cluster usually takes sometime (approximately 20 minutes).</span></span> <span data-ttu-id="d682f-274">Dlatego należy oczekiwać, że przetworzenie wycinka przez potok zajmie **około 30 minut**.</span><span class="sxs-lookup"><span data-stu-id="d682f-274">Therefore, expect the pipeline to take **approximately 30 minutes** to process the slice.</span></span>
>
> <span data-ttu-id="d682f-275">Po pomyślnym przetworzeniu wycinka plik wejściowy zostanie usunięty.</span><span class="sxs-lookup"><span data-stu-id="d682f-275">The input file gets deleted when the slice is processed successfully.</span></span> <span data-ttu-id="d682f-276">Tak więc, jeśli chcesz ponownie uruchomić wycinek lub ponownie wykonać instrukcje z tego samouczka, przekaż plik wejściowy (input.log) do folderu inputdata kontenera adfgetstarted.</span><span class="sxs-lookup"><span data-stu-id="d682f-276">Therefore, if you want to rerun the slice or do the tutorial again, upload the input file (input.log) to the inputdata folder of the adfgetstarted container.</span></span>
>
>

## <a name="summary"></a><span data-ttu-id="d682f-277">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="d682f-277">Summary</span></span>
<span data-ttu-id="d682f-278">W tym samouczku opisano tworzenie fabryki danych Azure do przetwarzania danych przez uruchomienie skryptu programu Hive w klastrze platformy Hadoop w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d682f-278">In this tutorial, you created an Azure data factory to process data by running Hive script on a HDInsight hadoop cluster.</span></span> <span data-ttu-id="d682f-279">Użyto Edytora fabryki danych w witrynie Azure Portal, aby:</span><span class="sxs-lookup"><span data-stu-id="d682f-279">You used the Data Factory Editor in the Azure portal to do the following steps:</span></span>

1. <span data-ttu-id="d682f-280">Tworzenie **fabryki danych** Azure.</span><span class="sxs-lookup"><span data-stu-id="d682f-280">Created an Azure **data factory**.</span></span>
2. <span data-ttu-id="d682f-281">Utworzyć dwie **połączone usługi**:</span><span class="sxs-lookup"><span data-stu-id="d682f-281">Created two **linked services**:</span></span>
   1. <span data-ttu-id="d682f-282">Połączoną usługę **Azure Storage** w celu połączenia magazynu obiektów blob Azure, w którym przechowywane są pliki wejściowe/wyjściowe, z fabryką danych.</span><span class="sxs-lookup"><span data-stu-id="d682f-282">**Azure Storage** linked service to link your Azure blob storage that holds input/output files to the data factory.</span></span>
   2. <span data-ttu-id="d682f-283">Połączoną usługę **Azure HDInsight** na żądanie w celu połączenia klastra platformy Hadoop w usłudze HDInsight na żądanie z fabryką danych.</span><span class="sxs-lookup"><span data-stu-id="d682f-283">**Azure HDInsight** on-demand linked service to link an on-demand HDInsight Hadoop cluster to the data factory.</span></span> <span data-ttu-id="d682f-284">Usługa Fabryka danych Azure tworzy klaster just in time platformy Hadoop w usłudze HDInsight, aby przetwarzać dane wejściowe i generować dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="d682f-284">Azure Data Factory creates a HDInsight Hadoop cluster just-in-time to process input data and produce output data.</span></span>
3. <span data-ttu-id="d682f-285">Utworzyć dwa **zestawy danych** zawierające dane wejściowe i wyjściowe dla działania programu Hive w usłudze HDInsight w potoku.</span><span class="sxs-lookup"><span data-stu-id="d682f-285">Created two **datasets**, which describe input and output data for HDInsight Hive activity in the pipeline.</span></span>
4. <span data-ttu-id="d682f-286">Utworzyć **potok** za pomocą działania **programu Hive w usłudze HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="d682f-286">Created a **pipeline** with a **HDInsight Hive** activity.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d682f-287">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d682f-287">Next steps</span></span>
<span data-ttu-id="d682f-288">W tym artykule opisano tworzenie potoku za pomocą działania przekształcania (działanie usługi HDInsight), które uruchamia skrypt programu Hive w klastrze usługi HDInsight platformy Azure na żądanie.</span><span class="sxs-lookup"><span data-stu-id="d682f-288">In this article, you have created a pipeline with a transformation activity (HDInsight Activity) that runs a Hive script on an on-demand Azure HDInsight cluster.</span></span> <span data-ttu-id="d682f-289">Instrukcje dotyczące korzystania z działania kopiowania w celu kopiowania danych z magazynu obiektów blob Azure do usług SQL Azure znajdują się w artykule [Tutorial: Copy data from an Azure Blob to Azure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) (Samouczek: kopiowanie danych z magazynu obiektów blob Azure do usług SQL Azure).</span><span class="sxs-lookup"><span data-stu-id="d682f-289">To see how to use a Copy Activity to copy data from an Azure Blob to Azure SQL, see [Tutorial: Copy data from an Azure Blob to Azure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="d682f-290">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="d682f-290">See Also</span></span>
| <span data-ttu-id="d682f-291">Temat</span><span class="sxs-lookup"><span data-stu-id="d682f-291">Topic</span></span> | <span data-ttu-id="d682f-292">Opis</span><span class="sxs-lookup"><span data-stu-id="d682f-292">Description</span></span> |
|:--- |:--- |
| [<span data-ttu-id="d682f-293">Dokumentacja dotycząca poleceń cmdlet usługi Data Factory</span><span class="sxs-lookup"><span data-stu-id="d682f-293">Data Factory Cmdlet Reference</span></span>](/powershell/module/azurerm.datafactories) |<span data-ttu-id="d682f-294">Zobacz pełną dokumentację dotyczącą poleceń cmdlet w usłudze Fabryka danych.</span><span class="sxs-lookup"><span data-stu-id="d682f-294">See comprehensive documentation on Data Factory cmdlets</span></span> |
| [<span data-ttu-id="d682f-295">Potoki</span><span class="sxs-lookup"><span data-stu-id="d682f-295">Pipelines</span></span>](data-factory-create-pipelines.md) |<span data-ttu-id="d682f-296">Ten artykuł ułatwia zapoznanie się z potokami i działaniami w usłudze Azure Data Factory oraz ze sposobem konstruowania za ich pomocą przepływów pracy typu end-to-end opartych na danych na potrzeby scenariusza lub firmy.</span><span class="sxs-lookup"><span data-stu-id="d682f-296">This article helps you understand pipelines and activities in Azure Data Factory and how to use them to construct end-to-end data-driven workflows for your scenario or business.</span></span> |
| [<span data-ttu-id="d682f-297">Zestawy danych</span><span class="sxs-lookup"><span data-stu-id="d682f-297">Datasets</span></span>](data-factory-create-datasets.md) |<span data-ttu-id="d682f-298">Ten artykuł ułatwia zapoznanie się z zestawami danych w usłudze Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="d682f-298">This article helps you understand datasets in Azure Data Factory.</span></span> |
| [<span data-ttu-id="d682f-299">Planowanie i wykonywanie</span><span class="sxs-lookup"><span data-stu-id="d682f-299">Scheduling and Execution</span></span>](data-factory-scheduling-and-execution.md) |<span data-ttu-id="d682f-300">W tym artykule wyjaśniono aspekty planowania i wykonywania modelu aplikacji usługi Fabryka danych Azure.</span><span class="sxs-lookup"><span data-stu-id="d682f-300">This article explains the scheduling and execution aspects of Azure Data Factory application model.</span></span> |
| [<span data-ttu-id="d682f-301">Monitorowanie potoków i zarządzanie nimi za pomocą aplikacji do monitorowania</span><span class="sxs-lookup"><span data-stu-id="d682f-301">Monitor and manage pipelines using Monitoring App</span></span>](data-factory-monitor-manage-app.md) |<span data-ttu-id="d682f-302">Ten artykuł zawiera instrukcje dotyczące monitorowania i debugowania potoków oraz zarządzania nimi przy użyciu aplikacji do monitorowania i zarządzania.</span><span class="sxs-lookup"><span data-stu-id="d682f-302">This article describes how to monitor, manage, and debug pipelines using the Monitoring & Management App.</span></span> |
