---
title: "aaaCreate Hadoop clusters przy użyciu szablonów - Azure HDInsight | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate klastrów dla usługi HDInsight przy użyciu szablonów usługi Resource Manager"
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 00a80dea-011f-44f0-92a4-25d09db9d996
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/30/2017
ms.author: jgao
ms.openlocfilehash: 92a6c1d888e401a11537dba34f188245ac17f448
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-hadoop-clusters-in-hdinsight-by-using-resource-manager-templates"></a><span data-ttu-id="21878-103">Tworzenie klastrów Hadoop w usłudze HDInsight przy użyciu szablonów usługi Resource Manager</span><span class="sxs-lookup"><span data-stu-id="21878-103">Create Hadoop clusters in HDInsight by using Resource Manager templates</span></span>
[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

<span data-ttu-id="21878-104">W tym artykule dowiesz się na kilka sposobów toocreate Azure HDInsight clusters przy użyciu szablonów usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="21878-104">In this article, you learn several ways toocreate Azure HDInsight clusters with Azure Resource Manager templates.</span></span> <span data-ttu-id="21878-105">Aby uzyskać więcej informacji, zobacz [wdrażania aplikacji przy użyciu szablonu usługi Azure Resource Manager](../azure-resource-manager/resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="21878-105">For more information, see [Deploy an application with Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md).</span></span> <span data-ttu-id="21878-106">toolearn o inne narzędzia do tworzenia klastra i funkcje, kliknij selektor karty hello na powitania początku tej strony lub zobacz [metody tworzenia klastrów](hdinsight-hadoop-provision-linux-clusters.md#cluster-setup-methods).</span><span class="sxs-lookup"><span data-stu-id="21878-106">toolearn about other cluster creation tools and features, click hello tab selector on hello top of this page or see [Cluster creation methods](hdinsight-hadoop-provision-linux-clusters.md#cluster-setup-methods).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="21878-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="21878-107">Prerequisites</span></span>
[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="21878-108">toofollow hello instrukcje w tym artykule, będą potrzebne:</span><span class="sxs-lookup"><span data-stu-id="21878-108">toofollow hello instructions in this article, you'll need:</span></span>

* <span data-ttu-id="21878-109">[Subskrypcji platformy Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="21878-109">An [Azure subscription](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="21878-110">Program Azure PowerShell i/lub Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="21878-110">Azure PowerShell and/or Azure CLI.</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-powershell-and-cli.md)]

### <a name="resource-manager-templates"></a><span data-ttu-id="21878-111">Szablony usługi Resource Manager</span><span class="sxs-lookup"><span data-stu-id="21878-111">Resource Manager templates</span></span>
<span data-ttu-id="21878-112">Szablonu usługi Resource Manager umożliwia łatwe toocreate powitania po aplikacji w jednej, skoordynowanej operacji:</span><span class="sxs-lookup"><span data-stu-id="21878-112">A Resource Manager template makes it easy toocreate hello following for your application in a single, coordinated operation:</span></span>
* <span data-ttu-id="21878-113">Klastry usługi HDInsight i ich zasoby zależne (takie jak hello domyślne konto magazynu)</span><span class="sxs-lookup"><span data-stu-id="21878-113">HDInsight clusters and their dependent resources (such as hello default storage account)</span></span>
* <span data-ttu-id="21878-114">Inne zasoby (na przykład baza danych SQL Azure toouse Apache Sqoop)</span><span class="sxs-lookup"><span data-stu-id="21878-114">Other resources (such as Azure SQL Database toouse Apache Sqoop)</span></span>

<span data-ttu-id="21878-115">W szablonie hello należy zdefiniować hello zasoby, które są wymagane dla aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="21878-115">In hello template, you define hello resources that are needed for hello application.</span></span> <span data-ttu-id="21878-116">Należy także określić wartości tooinput parametrów wdrożenia dla różnych środowisk.</span><span class="sxs-lookup"><span data-stu-id="21878-116">You also specify deployment parameters tooinput values for different environments.</span></span> <span data-ttu-id="21878-117">Szablon Hello składa się z kodu JSON i wyrażeń, użyj wartości tooconstruct dla danego wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="21878-117">hello template consists of JSON and expressions that you use tooconstruct values for your deployment.</span></span>

<span data-ttu-id="21878-118">Można znaleźć przykłady szablonu usługi HDInsight w [szablonów Szybki Start Azure](https://azure.microsoft.com/resources/templates/?term=hdinsight).</span><span class="sxs-lookup"><span data-stu-id="21878-118">You can find HDInsight template samples at [Azure Quickstart Templates](https://azure.microsoft.com/resources/templates/?term=hdinsight).</span></span> <span data-ttu-id="21878-119">Użyj wielu platform [Visual Studio Code](https://code.visualstudio.com/#alt-downloads) z hello [rozszerzenia usługi Resource Manager](https://marketplace.visualstudio.com/items?itemName=msazurermtools.azurerm-vscode-tools) lub w szablonie hello toosave Edytor tekstu do pliku na stację roboczą.</span><span class="sxs-lookup"><span data-stu-id="21878-119">Use cross-platform [Visual Studio Code](https://code.visualstudio.com/#alt-downloads) with hello [Resource Manager extension](https://marketplace.visualstudio.com/items?itemName=msazurermtools.azurerm-vscode-tools) or a text editor toosave hello template into a file on your workstation.</span></span> <span data-ttu-id="21878-120">Dowiedz się, jak toocall hello szablonu przy użyciu różnych metod.</span><span class="sxs-lookup"><span data-stu-id="21878-120">You learn how toocall hello template by using different methods.</span></span>

<span data-ttu-id="21878-121">Aby uzyskać więcej informacji na temat szablonów usługi Resource Manager zobacz następujące artykuły hello:</span><span class="sxs-lookup"><span data-stu-id="21878-121">For more information about Resource Manager templates, see hello following articles:</span></span>

* [<span data-ttu-id="21878-122">Tworzenie szablonów usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="21878-122">Author Azure Resource Manager templates</span></span>](../azure-resource-manager/resource-group-authoring-templates.md)
* [<span data-ttu-id="21878-123">Wdrażanie aplikacji przy użyciu szablonów usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="21878-123">Deploy an application with Azure Resource Manager templates</span></span>](../azure-resource-manager/resource-group-template-deploy.md)

## <a name="generate-templates"></a><span data-ttu-id="21878-124">Generowanie szablonów</span><span class="sxs-lookup"><span data-stu-id="21878-124">Generate templates</span></span>

<span data-ttu-id="21878-125">Za pomocą hello portalu Azure, można skonfigurować wszystkie właściwości hello klastra, a następnie zapisz hello szablon przed jego wdrożeniem.</span><span class="sxs-lookup"><span data-stu-id="21878-125">By using hello Azure portal, you can configure all hello properties of a cluster and then save hello template before deploying it.</span></span> <span data-ttu-id="21878-126">Następnie można ponownie użyć hello szablonu.</span><span class="sxs-lookup"><span data-stu-id="21878-126">You can then reuse hello template.</span></span>

<span data-ttu-id="21878-127">**toogenerate szablonu przy użyciu hello portalu Azure**</span><span class="sxs-lookup"><span data-stu-id="21878-127">**toogenerate a template by using hello Azure portal**</span></span>

1. <span data-ttu-id="21878-128">Zaloguj się toohello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="21878-128">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="21878-129">Kliknij przycisk **nowy** w menu po lewej stronie powitania kliknij **analizy i analiza**, a następnie kliknij przycisk **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="21878-129">Click **New** on hello left menu, click **Intelligence + analytics**, and then click **HDInsight**.</span></span>
3. <span data-ttu-id="21878-130">Wykonaj hello instrukcje tooenter właściwości.</span><span class="sxs-lookup"><span data-stu-id="21878-130">Follow hello instructions tooenter properties.</span></span> <span data-ttu-id="21878-131">Można użyć albo hello **szybkie tworzenie** lub hello **niestandardowy** opcji.</span><span class="sxs-lookup"><span data-stu-id="21878-131">You can use either hello **Quick create** or hello **Custom** option.</span></span>
4. <span data-ttu-id="21878-132">Na powitania **Podsumowanie** , kliknij pozycję **Pobierz szablon i parametry**:</span><span class="sxs-lookup"><span data-stu-id="21878-132">On hello **Summary** tab, click **Download template and parameters**:</span></span>

    ![Pobieranie szablonu usługi Resource Manager klastra tworzenia HDInsight Hadoop](./media/hdinsight-hadoop-create-linux-clusters-arm-templates/hdinsight-create-cluster-resource-manager-template-download.png)

    <span data-ttu-id="21878-134">Możesz wyświetlić listę hello pliku szablonu, pliku parametrów i kod próbek używanych toodeploy hello szablonu:</span><span class="sxs-lookup"><span data-stu-id="21878-134">You see a list of hello template file, parameters file, and code samples used toodeploy hello template:</span></span>

    ![HDInsight Hadoop tworzenia klastra opcje pobierania szablonu usługi Resource Manager](./media/hdinsight-hadoop-create-linux-clusters-arm-templates/hdinsight-create-cluster-resource-manager-template-download-options.png)

    <span data-ttu-id="21878-136">W tym miejscu można pobrać szablonu hello, bibliotekę szablonu tooyour zapisać lub wdrażanie szablonu hello.</span><span class="sxs-lookup"><span data-stu-id="21878-136">From here, you can download hello template, save it tooyour template library, or deploy hello template.</span></span>

    <span data-ttu-id="21878-137">tooaccess szablon w bibliotece, kliknij przycisk **więcej usług** z menu po lewej stronie powitania, a następnie kliknij przycisk **szablony** (w obszarze hello **innych** kategorii).</span><span class="sxs-lookup"><span data-stu-id="21878-137">tooaccess a template in your library, click **More services** from hello left menu, and then click **Templates** (under hello **Other** category).</span></span>

    > [!Note]
    > <span data-ttu-id="21878-138">Witaj pliku szablonu i parametry muszą być używane razem.</span><span class="sxs-lookup"><span data-stu-id="21878-138">hello template and parameters file must be used together.</span></span> <span data-ttu-id="21878-139">W przeciwnym razie może uzyskać nieoczekiwane wyniki.</span><span class="sxs-lookup"><span data-stu-id="21878-139">Otherwise, you might get unexpected results.</span></span> <span data-ttu-id="21878-140">Na przykład Witaj domyślne **clusterKind** wartość właściwości jest zawsze **hadoop**, pomimo należy określić przed pobraniem hello szablonu.</span><span class="sxs-lookup"><span data-stu-id="21878-140">For example, hello default **clusterKind** property value is always **hadoop**, despite what you specify before you download hello template.</span></span>



## <a name="deploy-with-powershell"></a><span data-ttu-id="21878-141">Wdrażanie przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="21878-141">Deploy with PowerShell</span></span>

<span data-ttu-id="21878-142">Ta procedura powoduje utworzenie klastra usługi Hadoop w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="21878-142">This procedure creates a Hadoop cluster in HDInsight.</span></span>

1. <span data-ttu-id="21878-143">Zapisz plik JSON hello w hello [dodatku](#appx-a-arm-template) tooyour stacji roboczej.</span><span class="sxs-lookup"><span data-stu-id="21878-143">Save hello JSON file in hello [Appendix](#appx-a-arm-template) tooyour workstation.</span></span> <span data-ttu-id="21878-144">W hello skrypt programu PowerShell, nazwa pliku hello jest `C:\HDITutorials-ARM\hdinsight-arm-template.json`.</span><span class="sxs-lookup"><span data-stu-id="21878-144">In hello PowerShell script, hello file name is `C:\HDITutorials-ARM\hdinsight-arm-template.json`.</span></span>
2. <span data-ttu-id="21878-145">W razie potrzeby wybierz hello parametry i zmienne.</span><span class="sxs-lookup"><span data-stu-id="21878-145">Set hello parameters and variables if needed.</span></span>
3. <span data-ttu-id="21878-146">Uruchom hello szablonu przy użyciu hello następującego skryptu programu PowerShell:</span><span class="sxs-lookup"><span data-stu-id="21878-146">Run hello template by using hello following PowerShell script:</span></span>

        ####################################
        # Set these variables
        ####################################
        #region - used for creating Azure service names
        $nameToken = "<Enter an Alias>"
        $templateFile = "C:\HDITutorials-ARM\hdinsight-arm-template.json"
        #endregion

        ####################################
        # Service names and variables
        ####################################
        #region - service names
        $namePrefix = $nameToken.ToLower() + (Get-Date -Format "MMdd")

        $resourceGroupName = $namePrefix + "rg"
        $hdinsightClusterName = $namePrefix + "hdi"
        $defaultStorageAccountName = $namePrefix + "store"
        $defaultBlobContainerName = $hdinsightClusterName

        $location = "East US 2"

        $armDeploymentName = $namePrefix
        #endregion

        ####################################
        # Connect tooAzure
        ####################################
        #region - Connect tooAzure subscription
        Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
        try{Get-AzureRmContext}
        catch{Login-AzureRmAccount}
        #endregion

        # Create a resource group
        New-AzureRmResourceGroup -Name $resourceGroupName -Location $Location

        # Create cluster and hello dependent storage account
        $parameters = @{clusterName="$hdinsightClusterName"}

        New-AzureRmResourceGroupDeployment `
            -Name $armDeploymentName `
            -ResourceGroupName $resourceGroupName `
            -TemplateFile $templateFile `
            -TemplateParameterObject $parameters

        # List cluster
        Get-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $hdinsightClusterName

    <span data-ttu-id="21878-147">Witaj skrypt programu PowerShell konfiguruje tylko nazwę klastra hello.</span><span class="sxs-lookup"><span data-stu-id="21878-147">hello PowerShell script configures only hello cluster name.</span></span> <span data-ttu-id="21878-148">Nazwa konta magazynu Hello jest ustalony w szablonie hello.</span><span class="sxs-lookup"><span data-stu-id="21878-148">hello storage account name is hard-coded in hello template.</span></span> <span data-ttu-id="21878-149">To hasło użytkownika klastra hello zostanie wyświetlony monit o tooenter.</span><span class="sxs-lookup"><span data-stu-id="21878-149">You are prompted tooenter hello cluster user password.</span></span> <span data-ttu-id="21878-150">(hello domyślna nazwa użytkownika to **admin**.) Ma również hasło użytkownika SSH hello zostanie wyświetlony monit o tooenter.</span><span class="sxs-lookup"><span data-stu-id="21878-150">(hello default username is **admin**.) You are also prompted tooenter hello SSH user password.</span></span> <span data-ttu-id="21878-151">(nazwa użytkownika SSH domyślne hello jest **sshuser**.)</span><span class="sxs-lookup"><span data-stu-id="21878-151">(hello default SSH username is **sshuser**.)</span></span>  

<span data-ttu-id="21878-152">Aby uzyskać więcej informacji, zobacz [wdrażanie przy użyciu programu PowerShell](../azure-resource-manager/resource-group-template-deploy.md#deploy-local-template).</span><span class="sxs-lookup"><span data-stu-id="21878-152">For more information, see  [Deploy with PowerShell](../azure-resource-manager/resource-group-template-deploy.md#deploy-local-template).</span></span>

## <a name="deploy-with-cli"></a><span data-ttu-id="21878-153">Rozmieszczanie za pomocą interfejsu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="21878-153">Deploy with CLI</span></span>
<span data-ttu-id="21878-154">następujące przykładowe Hello używa Azure interfejsu wiersza polecenia (CLI).</span><span class="sxs-lookup"><span data-stu-id="21878-154">hello following sample uses Azure command-line interface (CLI).</span></span> <span data-ttu-id="21878-155">Tworzy klastra i jego zależne konto magazynu i kontener wywołując szablonu usługi Resource Manager:</span><span class="sxs-lookup"><span data-stu-id="21878-155">It creates a cluster and its dependent storage account and container by calling a Resource Manager template:</span></span>

    azure login
    azure config mode arm
    azure group create -n hdi1229rg -l "East US"
    azure group deployment create --resource-group "hdi1229rg" --name "hdi1229" --template-file "C:\HDITutorials-ARM\hdinsight-arm-template.json"

<span data-ttu-id="21878-156">Jesteś tooenter monitem:</span><span class="sxs-lookup"><span data-stu-id="21878-156">You are prompted tooenter:</span></span>
* <span data-ttu-id="21878-157">Nazwa klastra Hello.</span><span class="sxs-lookup"><span data-stu-id="21878-157">hello cluster name.</span></span>
* <span data-ttu-id="21878-158">Witaj hasło użytkownika klastra.</span><span class="sxs-lookup"><span data-stu-id="21878-158">hello cluster user password.</span></span> <span data-ttu-id="21878-159">(hello domyślna nazwa użytkownika to **admin**.)</span><span class="sxs-lookup"><span data-stu-id="21878-159">(hello default username is **admin**.)</span></span>
* <span data-ttu-id="21878-160">hasło użytkownika SSH Hello.</span><span class="sxs-lookup"><span data-stu-id="21878-160">hello SSH user password.</span></span> <span data-ttu-id="21878-161">(nazwa użytkownika SSH domyślne hello jest **sshuser**.)</span><span class="sxs-lookup"><span data-stu-id="21878-161">(hello default SSH username is **sshuser**.)</span></span>

<span data-ttu-id="21878-162">Hello następującego kodu zawiera wbudowany parametry:</span><span class="sxs-lookup"><span data-stu-id="21878-162">hello following code provides inline parameters:</span></span>

    azure group deployment create --resource-group "hdi1229rg" --name "hdi1229" --template-file "c:\Tutorials\HDInsightARM\create-linux-based-hadoop-cluster-in-hdinsight.json" --parameters '{\"clusterName\":{\"value\":\"hdi1229\"},\"clusterLoginPassword\":{\"value\":\"Pass@word1\"},\"sshPassword\":{\"value\":\"Pass@word1\"}}'

## <a name="deploy-with-hello-rest-api"></a><span data-ttu-id="21878-163">Wdrażanie z hello interfejsu API REST</span><span class="sxs-lookup"><span data-stu-id="21878-163">Deploy with hello REST API</span></span>
<span data-ttu-id="21878-164">Zobacz [Rozmieszczanie za pomocą interfejsu API REST hello](../azure-resource-manager/resource-group-template-deploy-rest.md).</span><span class="sxs-lookup"><span data-stu-id="21878-164">See [Deploy with hello REST API](../azure-resource-manager/resource-group-template-deploy-rest.md).</span></span>

## <a name="deploy-with-visual-studio"></a><span data-ttu-id="21878-165">Wdrażanie za pomocą programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="21878-165">Deploy with Visual Studio</span></span>
 <span data-ttu-id="21878-166">Użyj programu Visual Studio toocreate projekt grupy zasobów i wdrożyć ją tooAzure za pomocą interfejsu użytkownika hello.</span><span class="sxs-lookup"><span data-stu-id="21878-166">Use Visual Studio toocreate a resource group project and deploy it tooAzure through hello user interface.</span></span> <span data-ttu-id="21878-167">Wybrany typ hello tooinclude zasobów w projekcie.</span><span class="sxs-lookup"><span data-stu-id="21878-167">You select hello type of resources tooinclude in your project.</span></span> <span data-ttu-id="21878-168">Te zasoby są automatycznie dodawane toohello szablonu usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="21878-168">Those resources are automatically added toohello Resource Manager template.</span></span> <span data-ttu-id="21878-169">Projekt Hello udostępnia również szablonu hello toodeploy skrypt programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="21878-169">hello project also provides a PowerShell script toodeploy hello template.</span></span>

<span data-ttu-id="21878-170">Do wprowadzenia toousing programu Visual Studio z grupami zasobów, zobacz [tworzenie i wdrażanie grup zasobów platformy Azure za pomocą programu Visual Studio](../azure-resource-manager/vs-azure-tools-resource-groups-deployment-projects-create-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="21878-170">For an introduction toousing Visual Studio with resource groups, see [Creating and deploying Azure resource groups through Visual Studio](../azure-resource-manager/vs-azure-tools-resource-groups-deployment-projects-create-deploy.md).</span></span>

## <a name="troubleshoot"></a><span data-ttu-id="21878-171">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="21878-171">Troubleshoot</span></span>

<span data-ttu-id="21878-172">W razie problemów podczas tworzenia klastrów usługi HDInsight zapoznaj się z [wymaganiami dotyczącymi kontroli dostępu](hdinsight-administer-use-portal-linux.md#create-clusters).</span><span class="sxs-lookup"><span data-stu-id="21878-172">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="21878-173">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="21878-173">Next steps</span></span>
<span data-ttu-id="21878-174">W tym artykule uzyskanych kilka sposobów toocreate klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="21878-174">In this article, you have learned several ways toocreate an HDInsight cluster.</span></span> <span data-ttu-id="21878-175">toolearn więcej, zobacz następujące artykuły hello:</span><span class="sxs-lookup"><span data-stu-id="21878-175">toolearn more, see hello following articles:</span></span>

* <span data-ttu-id="21878-176">Na przykład wdrażania zasobów za pomocą biblioteki klienta .NET hello zobacz [wdrażanie zasobów przy użyciu bibliotek .NET oraz szablonu](../virtual-machines/windows/csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="21878-176">For an example of deploying resources through hello .NET client library, see [Deploy resources by using .NET libraries and a template](../virtual-machines/windows/csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="21878-177">Szczegółowy przykład wdrażania aplikacji, zobacz [udostępniania i wdrażanie mikrousług przewidywalnego na platformie Azure](../app-service-web/app-service-deploy-complex-application-predictably.md).</span><span class="sxs-lookup"><span data-stu-id="21878-177">For an in-depth example of deploying an application, see [Provision and deploy microservices predictably in Azure](../app-service-web/app-service-deploy-complex-application-predictably.md).</span></span>
* <span data-ttu-id="21878-178">Aby uzyskać wskazówki dotyczące wdrażania środowiska toodifferent rozwiązania, zobacz [środowisk projektowania i testowania na platformie Microsoft Azure](../solution-dev-test-environments.md).</span><span class="sxs-lookup"><span data-stu-id="21878-178">For guidance on deploying your solution toodifferent environments, see [Development and test environments in Microsoft Azure](../solution-dev-test-environments.md).</span></span>
* <span data-ttu-id="21878-179">toolearn o sekcje hello hello szablonu usługi Azure Resource Manager, zobacz [tworzenia szablonów](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="21878-179">toolearn about hello sections of hello Azure Resource Manager template, see [Authoring templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="21878-180">Listę funkcji hello można użyć w szablonie usługi Azure Resource Manager, zobacz [szablonu funkcji](../azure-resource-manager/resource-group-template-functions.md).</span><span class="sxs-lookup"><span data-stu-id="21878-180">For a list of hello functions you can use in an Azure Resource Manager template, see [Template functions](../azure-resource-manager/resource-group-template-functions.md).</span></span>

## <a name="appendix-resource-manager-template-toocreate-a-hadoop-cluster"></a><span data-ttu-id="21878-181">Dodatek: Menedżer zasobów szablonu toocreate klastra usługi Hadoop</span><span class="sxs-lookup"><span data-stu-id="21878-181">Appendix: Resource Manager template toocreate a Hadoop cluster</span></span>
<span data-ttu-id="21878-182">Witaj następującego szablonu usługi Azure Resource Manager tworzy opartą na systemie Linux platformą Hadoop klaster z hello zależne konto magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="21878-182">hello following Azure Resource Manager template creates a Linux-based Hadoop cluster with hello dependent Azure storage account.</span></span>

> [!NOTE]
> <span data-ttu-id="21878-183">Ten przykład zawiera informacje o konfiguracji na potrzeby magazynu metadanych Hive i potrzeby magazynu metadanych Oozie.</span><span class="sxs-lookup"><span data-stu-id="21878-183">This sample includes configuration information for Hive metastore and Oozie metastore.</span></span> <span data-ttu-id="21878-184">Usuwanie sekcji hello lub skonfiguruj sekcji hello przed użyciem hello szablonu.</span><span class="sxs-lookup"><span data-stu-id="21878-184">Remove hello section or configure hello section before using hello template.</span></span>
>
>

    {
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "clusterName": {
        "type": "string",
        "metadata": {
            "description": "hello name of hello HDInsight cluster toocreate."
        }
        },
        "clusterLoginUserName": {
        "type": "string",
        "defaultValue": "admin",
        "metadata": {
            "description": "These credentials can be used toosubmit jobs toohello cluster and toolog into cluster dashboards."
        }
        },
        "clusterLoginPassword": {
        "type": "securestring",
        "metadata": {
            "description": "hello password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
        }
        },
        "sshUserName": {
        "type": "string",
        "defaultValue": "sshuser",
        "metadata": {
            "description": "These credentials can be used tooremotely access hello cluster."
        }
        },
        "sshPassword": {
        "type": "securestring",
        "metadata": {
            "description": "hello password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
        }
        },
        "location": {
        "type": "string",
        "defaultValue": "East US",
        "allowedValues": [
            "East US",
            "East US 2",
            "North Central US",
            "South Central US",
            "West US",
            "North Europe",
            "West Europe",
            "East Asia",
            "Southeast Asia",
            "Japan East",
            "Japan West",
            "Australia East",
            "Australia Southeast"
        ],
        "metadata": {
            "description": "hello location where all azure resources will be deployed."
        }
        },
        "clusterType": {
        "type": "string",
        "defaultValue": "hadoop",
        "allowedValues": [
            "hadoop",
            "hbase",
            "storm",
            "spark"
        ],
        "metadata": {
            "description": "hello type of hello HDInsight cluster toocreate."
        }
        },
        "clusterWorkerNodeCount": {
        "type": "int",
        "defaultValue": 2,
        "metadata": {
            "description": "hello number of nodes in hello HDInsight cluster."
        }
        }
    },
    "variables": {
        "defaultApiVersion": "2015-05-01-preview",
        "clusterApiVersion": "2015-03-01-preview",
        "clusterStorageAccountName": "[concat(parameters('clusterName'),'store')]"
    },
    "resources": [
        {
        "name": "[variables('clusterStorageAccountName')]",
        "type": "Microsoft.Storage/storageAccounts",
        "location": "[parameters('location')]",
        "apiVersion": "[variables('defaultApiVersion')]",
        "dependsOn": [ ],
        "tags": { },
        "properties": {
            "accountType": "Standard_LRS"
        }
        },
        {
        "name": "[parameters('clusterName')]",
        "type": "Microsoft.HDInsight/clusters",
        "location": "[parameters('location')]",
        "apiVersion": "[variables('clusterApiVersion')]",
        "dependsOn": [ "[concat('Microsoft.Storage/storageAccounts/',variables('clusterStorageAccountName'))]" ],
        "tags": {

        },
        "properties": {
            "clusterVersion": "3.4",
            "osType": "Linux",
            "tier": "standard",
            "clusterDefinition": {
            "kind": "[parameters('clusterType')]",
            "configurations": {
                "gateway": {
                "restAuthCredential.isEnabled": true,
                "restAuthCredential.username": "[parameters('clusterLoginUserName')]",
                "restAuthCredential.password": "[parameters('clusterLoginPassword')]"
                },
                "hive-site": {
                    "javax.jdo.option.ConnectionDriverName": "com.microsoft.sqlserver.jdbc.SQLServerDriver",
                    "javax.jdo.option.ConnectionURL": "jdbc:sqlserver://myadla0901dbserver.database.windows.net;database=myhive20160901;encrypt=true;trustServerCertificate=true;create=false;loginTimeout=300",
                    "javax.jdo.option.ConnectionUserName": "johndole",
                    "javax.jdo.option.ConnectionPassword": "myPassword$"
                },
                "hive-env": {
                    "hive_database": "Existing MSSQL Server database with SQL authentication",
                    "hive_database_name": "myhive20160901",
                    "hive_database_type": "mssql",
                    "hive_existing_mssql_server_database": "myhive20160901",
                    "hive_existing_mssql_server_host": "myadla0901dbserver.database.windows.net",
                    "hive_hostname": "myadla0901dbserver.database.windows.net"
                },
                "oozie-site": {
                    "oozie.service.JPAService.jdbc.driver": "com.microsoft.sqlserver.jdbc.SQLServerDriver",
                    "oozie.service.JPAService.jdbc.url": "jdbc:sqlserver://myadla0901dbserver.database.windows.net;database=myhive20160901;encrypt=true;trustServerCertificate=true;create=false;loginTimeout=300",
                    "oozie.service.JPAService.jdbc.username": "johndole",
                    "oozie.service.JPAService.jdbc.password": "myPassword$",
                    "oozie.db.schema.name": "oozie"
                },
                "oozie-env": {
                    "oozie_database": "Existing MSSQL Server database with SQL authentication",
                    "oozie_database_name": "myhive20160901",
                    "oozie_database_type": "mssql",
                    "oozie_existing_mssql_server_database": "myhive20160901",
                    "oozie_existing_mssql_server_host": "myadla0901dbserver.database.windows.net",
                    "oozie_hostname": "myadla0901dbserver.database.windows.net"
                }            
            }
            },
            "storageProfile": {
            "storageaccounts": [
                {
                "name": "[concat(variables('clusterStorageAccountName'),'.blob.core.windows.net')]",
                "isDefault": true,
                "container": "[parameters('clusterName')]",
                "key": "[listKeys(resourceId('Microsoft.Storage/storageAccounts', variables('clusterStorageAccountName')), variables('defaultApiVersion')).keys[0].value]"
                }
            ]
            },
            "computeProfile": {
            "roles": [
                {
                "name": "headnode",
                "targetInstanceCount": "2",
                "hardwareProfile": {
                    "vmSize": "Standard_D3"
                },
                "osProfile": {
                    "linuxOperatingSystemProfile": {
                    "username": "[parameters('sshUserName')]",
                    "password": "[parameters('sshPassword')]"
                    }
                }
                },
                {
                "name": "workernode",
                "targetInstanceCount": "[parameters('clusterWorkerNodeCount')]",
                "hardwareProfile": {
                    "vmSize": "Standard_D3"
                },
                "osProfile": {
                    "linuxOperatingSystemProfile": {
                    "username": "[parameters('sshUserName')]",
                    "password": "[parameters('sshPassword')]"
                    }
                }
                }
            ]
            }
        }
        }
    ],
    "outputs": {
        "cluster": {
        "type": "object",
        "value": "[reference(resourceId('Microsoft.HDInsight/clusters',parameters('clusterName')))]"
        }
    }
    }

## <a name="appendix-resource-manager-template-toocreate-a-spark-cluster"></a><span data-ttu-id="21878-185">Dodatek: Menedżer zasobów szablonu toocreate klastra Spark</span><span class="sxs-lookup"><span data-stu-id="21878-185">Appendix: Resource Manager template toocreate a Spark cluster</span></span>

<span data-ttu-id="21878-186">Ta sekcja zawiera szablonu usługi Resource Manager służy toocreate klastra Spark w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="21878-186">This section provides a Resource Manager template that you can use toocreate an HDInsight Spark cluster.</span></span> <span data-ttu-id="21878-187">Ten szablon obejmuje konfiguracje `spark-defaults` i `spark-thrift-sparkconf` (dla klastry Spark 1.6) i `spark2-defaults` i `spark2-thrift-sparkconf` (dla klastry Spark 2).</span><span class="sxs-lookup"><span data-stu-id="21878-187">This template includes configurations for `spark-defaults` and `spark-thrift-sparkconf` (for Spark 1.6 clusters) and `spark2-defaults` and `spark2-thrift-sparkconf` (for Spark 2 clusters).</span></span> <span data-ttu-id="21878-188">Ponadto toothis, HDInsight jest obliczana i ustawia konfiguracje, takie jak `spark.executor.instances`, `spark.executor.memory`, i `spark.executor.cores` na podstawie hello rozmiaru klastra.</span><span class="sxs-lookup"><span data-stu-id="21878-188">In addition toothis, HDInsight calculates and sets configurations such as `spark.executor.instances`, `spark.executor.memory`, and `spark.executor.cores` based on hello cluster size.</span></span> 

<span data-ttu-id="21878-189">Jeśli ustawisz wszystkie jeden parametr w sekcji jako część szablonu hello HDInsight nie obliczenia i ustaw hello inne parametry hello tej samej sekcji.</span><span class="sxs-lookup"><span data-stu-id="21878-189">If you set any one parameter in a section as part of hello template itself, HDInsight does not calculate and set hello other parameters of hello same section.</span></span> <span data-ttu-id="21878-190">Na przykład parametr `spark.executor.instances` w hello `spark-defaults` konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="21878-190">For example, parameter `spark.executor.instances` is in hello  `spark-defaults` configuration.</span></span> <span data-ttu-id="21878-191">Jeśli ustawisz parametr innego (na przykład `spark.yarn.exector.memoryOverhead`) w hello `spark-defaults` konfiguracji, HDInsight nie obliczenia i ustaw hello `spark.executor.instances` również parametr.</span><span class="sxs-lookup"><span data-stu-id="21878-191">If you set another parameter (for example, `spark.yarn.exector.memoryOverhead`) in hello `spark-defaults` configuration, HDInsight does not calculate and set hello `spark.executor.instances` parameter as well.</span></span>

    {
    "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
    "contentVersion": "0.9.0.0",
    "parameters": {
        "clusterName": {
            "type": "string",
            "metadata": {
                "description": "hello name of hello HDInsight cluster toocreate."
            }
        },
        "clusterLoginUserName": {
            "type": "string",
            "defaultValue": "admin",
            "metadata": {
                "description": "These credentials can be used toosubmit jobs toohello cluster and toolog into cluster dashboards."
            }
        },
        "clusterLoginPassword": {
            "type": "securestring",
            "metadata": {
                "description": "hello password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
            }
        },
        "location": {
            "type": "string",
            "defaultValue": "southcentralus",
            "metadata": {
                "description": "hello location where all azure resources will be deployed."
            }
        },
        "clusterVersion": {
            "type": "string",
            "defaultValue": "3.5",
            "metadata": {
                "description": "HDInsight cluster version."
            }
        },
        "clusterWorkerNodeCount": {
            "type": "int",
            "defaultValue": 4,
            "metadata": {
                "description": "hello number of nodes in hello HDInsight cluster."
            }
        },
        "clusterKind": {
            "type": "string",
            "defaultValue": "SPARK",
            "metadata": {
                "description": "hello type of hello HDInsight cluster toocreate."
            }
        },
        "sshUserName": {
            "type": "string",
            "defaultValue": "sshuser",
            "metadata": {
                "description": "These credentials can be used tooremotely access hello cluster."
            }
        },
        "sshPassword": {
            "type": "securestring",
            "metadata": {
                "description": "hello password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
            }
        }
    },
    "variables": {
        "defaultApiVersion": "2017-06-01",
        "clusterStorageAccountName": "[concat(parameters('clusterName'),'store')]"
    },
    "resources": [
        {
        "name": "[variables('clusterStorageAccountName')]",
        "type": "Microsoft.Storage/storageAccounts",
        "location": "[parameters('location')]",
        "apiVersion": "[variables('defaultApiVersion')]",
        "dependsOn": [ ],
        "tags": { },
        "properties": {
            "accountType": "Standard_LRS"
        }
        },
    {
            "apiVersion": "2015-03-01-preview",
            "name": "[parameters('clusterName')]",
            "type": "Microsoft.HDInsight/clusters",
            "location": "[parameters('location')]",
            "dependsOn": [],
            "properties": {
                "clusterVersion": "[parameters('clusterVersion')]",
                "osType": "Linux",
                "tier": "standard",
                "clusterDefinition": {
                    "kind": "[parameters('clusterKind')]",
                    "configurations": {
                        "gateway": {
                            "restAuthCredential.isEnabled": true,
                            "restAuthCredential.username": "[parameters('clusterLoginUserName')]",
                            "restAuthCredential.password": "[parameters('clusterLoginPassword')]"
                        },
                        "spark-defaults": {
                            "spark.executor.cores": "2"
                        },
                        "spark-thrift-sparkconf": {
                            "spark.yarn.executor.memoryOverhead": "896"
                        }
                    }
                },
                "storageProfile": {
                    "storageaccounts": [
                        {
                            "name": "[concat(variables('clusterStorageAccountName'),'.blob.core.windows.net')]",
                            "isDefault": true,
                            "container": "[parameters('clusterName')]",
                            "key": "[listKeys(resourceId('Microsoft.Storage/storageAccounts', variables('clusterStorageAccountName')), variables('defaultApiVersion')).keys[0].value]"
                        }
                    ]
                },
                "computeProfile": {
                    "roles": [
                        {
                            "name": "headnode",
                            "minInstanceCount": 1,
                            "targetInstanceCount": 2,
                            "hardwareProfile": {
                                "vmSize": "Standard_D12"
                            },
                            "osProfile": {
                                "linuxOperatingSystemProfile": {
                                    "username": "[parameters('sshUserName')]",
                                    "password": "[parameters('sshPassword')]"
                                }
                            },
                            "virtualNetworkProfile": null,
                            "scriptActions": []
                        },
                        {
                            "name": "workernode",
                            "minInstanceCount": 1,
                            "targetInstanceCount": 4,
                            "hardwareProfile": {
                                "vmSize": "Standard_D4"
                            },
                            "osProfile": {
                                "linuxOperatingSystemProfile": {
                                    "username": "[parameters('sshUserName')]",
                                    "password": "[parameters('sshPassword')]"
                                    }
                                },
                                "virtualNetworkProfile": null,
                                "scriptActions": []
                            }
                        ]
                    }
                }
            }
        ]
    }
