---
title: "Tworzenie klastrów Hadoop przy użyciu szablonów - Azure HDInsight | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie tworzenia klastrów dla usługi HDInsight przy użyciu szablonów usługi Resource Manager"
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
ms.openlocfilehash: b2cdc954530daea2a641599c946ce3787149e762
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="create-hadoop-clusters-in-hdinsight-by-using-resource-manager-templates"></a><span data-ttu-id="35a34-103">Tworzenie klastrów Hadoop w usłudze HDInsight przy użyciu szablonów usługi Resource Manager</span><span class="sxs-lookup"><span data-stu-id="35a34-103">Create Hadoop clusters in HDInsight by using Resource Manager templates</span></span>
[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

<span data-ttu-id="35a34-104">W tym artykule dowiesz się kilka sposobów tworzenia klastrów usługi HDInsight Azure przy użyciu szablonów usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="35a34-104">In this article, you learn several ways to create Azure HDInsight clusters with Azure Resource Manager templates.</span></span> <span data-ttu-id="35a34-105">Aby uzyskać więcej informacji, zobacz [wdrażania aplikacji przy użyciu szablonu usługi Azure Resource Manager](../azure-resource-manager/resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="35a34-105">For more information, see [Deploy an application with Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md).</span></span> <span data-ttu-id="35a34-106">Informacje na temat innych funkcji i narzędzi tworzenia klastra, kliknij selektor karty w górnej części strony, lub zobacz [metody tworzenia klastrów](hdinsight-hadoop-provision-linux-clusters.md#cluster-setup-methods).</span><span class="sxs-lookup"><span data-stu-id="35a34-106">To learn about other cluster creation tools and features, click the tab selector on the top of this page or see [Cluster creation methods](hdinsight-hadoop-provision-linux-clusters.md#cluster-setup-methods).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="35a34-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="35a34-107">Prerequisites</span></span>
[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="35a34-108">Postępuj zgodnie z instrukcjami w tym artykule, będą potrzebne:</span><span class="sxs-lookup"><span data-stu-id="35a34-108">To follow the instructions in this article, you'll need:</span></span>

* <span data-ttu-id="35a34-109">[Subskrypcji platformy Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="35a34-109">An [Azure subscription](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="35a34-110">Program Azure PowerShell i/lub Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="35a34-110">Azure PowerShell and/or Azure CLI.</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-powershell-and-cli.md)]

### <a name="resource-manager-templates"></a><span data-ttu-id="35a34-111">Szablony usługi Resource Manager</span><span class="sxs-lookup"><span data-stu-id="35a34-111">Resource Manager templates</span></span>
<span data-ttu-id="35a34-112">Szablon usługi Resource Manager ułatwia tworzenie następujących aplikacji w jednej, skoordynowanej operacji:</span><span class="sxs-lookup"><span data-stu-id="35a34-112">A Resource Manager template makes it easy to create the following for your application in a single, coordinated operation:</span></span>
* <span data-ttu-id="35a34-113">Klastry usługi HDInsight i ich zasoby zależne (takie jak domyślne konto magazynu)</span><span class="sxs-lookup"><span data-stu-id="35a34-113">HDInsight clusters and their dependent resources (such as the default storage account)</span></span>
* <span data-ttu-id="35a34-114">Inne zasoby (takie jak bazy danych SQL Azure do narzędzia Apache sqoop)</span><span class="sxs-lookup"><span data-stu-id="35a34-114">Other resources (such as Azure SQL Database to use Apache Sqoop)</span></span>

<span data-ttu-id="35a34-115">W szablonie można zdefiniować zasoby, które są wymagane dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="35a34-115">In the template, you define the resources that are needed for the application.</span></span> <span data-ttu-id="35a34-116">Należy także określić parametry wdrożenia wprowadzanie wartości dla różnych środowisk.</span><span class="sxs-lookup"><span data-stu-id="35a34-116">You also specify deployment parameters to input values for different environments.</span></span> <span data-ttu-id="35a34-117">Szablon składa się z kodu JSON i wyrażeń, których można używać do tworzenia wartości dla danego wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="35a34-117">The template consists of JSON and expressions that you use to construct values for your deployment.</span></span>

<span data-ttu-id="35a34-118">Można znaleźć przykłady szablonu usługi HDInsight w [szablonów Szybki Start Azure](https://azure.microsoft.com/resources/templates/?term=hdinsight).</span><span class="sxs-lookup"><span data-stu-id="35a34-118">You can find HDInsight template samples at [Azure Quickstart Templates](https://azure.microsoft.com/resources/templates/?term=hdinsight).</span></span> <span data-ttu-id="35a34-119">Użyj wielu platform [Visual Studio Code](https://code.visualstudio.com/#alt-downloads) z [rozszerzenia usługi Resource Manager](https://marketplace.visualstudio.com/items?itemName=msazurermtools.azurerm-vscode-tools) lub edytora tekstu, aby zapisać szablon do pliku na stację roboczą.</span><span class="sxs-lookup"><span data-stu-id="35a34-119">Use cross-platform [Visual Studio Code](https://code.visualstudio.com/#alt-downloads) with the [Resource Manager extension](https://marketplace.visualstudio.com/items?itemName=msazurermtools.azurerm-vscode-tools) or a text editor to save the template into a file on your workstation.</span></span> <span data-ttu-id="35a34-120">Sposób wywołać szablonu przy użyciu różnych metod.</span><span class="sxs-lookup"><span data-stu-id="35a34-120">You learn how to call the template by using different methods.</span></span>

<span data-ttu-id="35a34-121">Aby uzyskać więcej informacji na temat szablonów usługi Resource Manager zobacz następujące artykuły:</span><span class="sxs-lookup"><span data-stu-id="35a34-121">For more information about Resource Manager templates, see the following articles:</span></span>

* [<span data-ttu-id="35a34-122">Tworzenie szablonów usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="35a34-122">Author Azure Resource Manager templates</span></span>](../azure-resource-manager/resource-group-authoring-templates.md)
* [<span data-ttu-id="35a34-123">Wdrażanie aplikacji przy użyciu szablonów usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="35a34-123">Deploy an application with Azure Resource Manager templates</span></span>](../azure-resource-manager/resource-group-template-deploy.md)

## <a name="generate-templates"></a><span data-ttu-id="35a34-124">Generowanie szablonów</span><span class="sxs-lookup"><span data-stu-id="35a34-124">Generate templates</span></span>

<span data-ttu-id="35a34-125">Za pomocą portalu Azure, można skonfigurować właściwości klastra, a następnie zapisz szablon przed jego wdrożeniem.</span><span class="sxs-lookup"><span data-stu-id="35a34-125">By using the Azure portal, you can configure all the properties of a cluster and then save the template before deploying it.</span></span> <span data-ttu-id="35a34-126">Następnie można ponownie użyć tego szablonu.</span><span class="sxs-lookup"><span data-stu-id="35a34-126">You can then reuse the template.</span></span>

<span data-ttu-id="35a34-127">**Aby wygenerować szablonu przy użyciu portalu Azure**</span><span class="sxs-lookup"><span data-stu-id="35a34-127">**To generate a template by using the Azure portal**</span></span>

1. <span data-ttu-id="35a34-128">Zaloguj się w witrynie [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="35a34-128">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="35a34-129">Kliknij przycisk **nowy** w menu po lewej stronie kliknij **analizy i analiza**, a następnie kliknij przycisk **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="35a34-129">Click **New** on the left menu, click **Intelligence + analytics**, and then click **HDInsight**.</span></span>
3. <span data-ttu-id="35a34-130">Postępuj zgodnie z instrukcjami, aby wprowadzić właściwości.</span><span class="sxs-lookup"><span data-stu-id="35a34-130">Follow the instructions to enter properties.</span></span> <span data-ttu-id="35a34-131">Możesz użyć dowolnej **szybkie tworzenie** lub **niestandardowy** opcji.</span><span class="sxs-lookup"><span data-stu-id="35a34-131">You can use either the **Quick create** or the **Custom** option.</span></span>
4. <span data-ttu-id="35a34-132">Na **Podsumowanie** , kliknij pozycję **Pobierz szablon i parametry**:</span><span class="sxs-lookup"><span data-stu-id="35a34-132">On the **Summary** tab, click **Download template and parameters**:</span></span>

    ![Pobieranie szablonu usługi Resource Manager klastra tworzenia HDInsight Hadoop](./media/hdinsight-hadoop-create-linux-clusters-arm-templates/hdinsight-create-cluster-resource-manager-template-download.png)

    <span data-ttu-id="35a34-134">Możesz wyświetlić listę pliku szablonu pliku parametrów i przykładów kodu użyty do wdrożenia szablonu:</span><span class="sxs-lookup"><span data-stu-id="35a34-134">You see a list of the template file, parameters file, and code samples used to deploy the template:</span></span>

    ![HDInsight Hadoop tworzenia klastra opcje pobierania szablonu usługi Resource Manager](./media/hdinsight-hadoop-create-linux-clusters-arm-templates/hdinsight-create-cluster-resource-manager-template-download-options.png)

    <span data-ttu-id="35a34-136">W tym miejscu można pobrać szablonu, zapisać go do biblioteki szablonów lub wdrożenia szablonu.</span><span class="sxs-lookup"><span data-stu-id="35a34-136">From here, you can download the template, save it to your template library, or deploy the template.</span></span>

    <span data-ttu-id="35a34-137">Aby uzyskać dostęp do szablonu w bibliotece, kliknij przycisk **więcej usług** z menu po lewej stronie, a następnie kliknij przycisk **szablony** (w obszarze **innych** kategorii).</span><span class="sxs-lookup"><span data-stu-id="35a34-137">To access a template in your library, click **More services** from the left menu, and then click **Templates** (under the **Other** category).</span></span>

    > [!Note]
    > <span data-ttu-id="35a34-138">Plik szablonu i parametry muszą być używane razem.</span><span class="sxs-lookup"><span data-stu-id="35a34-138">The template and parameters file must be used together.</span></span> <span data-ttu-id="35a34-139">W przeciwnym razie może uzyskać nieoczekiwane wyniki.</span><span class="sxs-lookup"><span data-stu-id="35a34-139">Otherwise, you might get unexpected results.</span></span> <span data-ttu-id="35a34-140">Na przykład, wartość domyślna **clusterKind** wartość właściwości jest zawsze **hadoop**, pomimo należy określić przed pobraniem szablonu.</span><span class="sxs-lookup"><span data-stu-id="35a34-140">For example, the default **clusterKind** property value is always **hadoop**, despite what you specify before you download the template.</span></span>



## <a name="deploy-with-powershell"></a><span data-ttu-id="35a34-141">Wdrażanie przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="35a34-141">Deploy with PowerShell</span></span>

<span data-ttu-id="35a34-142">Ta procedura powoduje utworzenie klastra usługi Hadoop w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="35a34-142">This procedure creates a Hadoop cluster in HDInsight.</span></span>

1. <span data-ttu-id="35a34-143">Zapisz plik JSON w [dodatku](#appx-a-arm-template) na stację roboczą.</span><span class="sxs-lookup"><span data-stu-id="35a34-143">Save the JSON file in the [Appendix](#appx-a-arm-template) to your workstation.</span></span> <span data-ttu-id="35a34-144">W skrypcie programu PowerShell, nazwa pliku jest `C:\HDITutorials-ARM\hdinsight-arm-template.json`.</span><span class="sxs-lookup"><span data-stu-id="35a34-144">In the PowerShell script, the file name is `C:\HDITutorials-ARM\hdinsight-arm-template.json`.</span></span>
2. <span data-ttu-id="35a34-145">Jeśli to konieczne, należy ustawić parametry i zmienne.</span><span class="sxs-lookup"><span data-stu-id="35a34-145">Set the parameters and variables if needed.</span></span>
3. <span data-ttu-id="35a34-146">Uruchom szablonu przy użyciu następujący skrypt programu PowerShell:</span><span class="sxs-lookup"><span data-stu-id="35a34-146">Run the template by using the following PowerShell script:</span></span>

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
        # Connect to Azure
        ####################################
        #region - Connect to Azure subscription
        Write-Host "`nConnecting to your Azure subscription ..." -ForegroundColor Green
        try{Get-AzureRmContext}
        catch{Login-AzureRmAccount}
        #endregion

        # Create a resource group
        New-AzureRmResourceGroup -Name $resourceGroupName -Location $Location

        # Create cluster and the dependent storage account
        $parameters = @{clusterName="$hdinsightClusterName"}

        New-AzureRmResourceGroupDeployment `
            -Name $armDeploymentName `
            -ResourceGroupName $resourceGroupName `
            -TemplateFile $templateFile `
            -TemplateParameterObject $parameters

        # List cluster
        Get-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $hdinsightClusterName

    <span data-ttu-id="35a34-147">Skrypt programu PowerShell konfiguruje tylko nazwę klastra.</span><span class="sxs-lookup"><span data-stu-id="35a34-147">The PowerShell script configures only the cluster name.</span></span> <span data-ttu-id="35a34-148">Nazwa konta magazynu jest ustalony w szablonie.</span><span class="sxs-lookup"><span data-stu-id="35a34-148">The storage account name is hard-coded in the template.</span></span> <span data-ttu-id="35a34-149">Monit o wprowadzenie hasła użytkownika klastra.</span><span class="sxs-lookup"><span data-stu-id="35a34-149">You are prompted to enter the cluster user password.</span></span> <span data-ttu-id="35a34-150">(Domyślna nazwa użytkownika to **admin**.) Możesz również monit o wprowadzenie hasła użytkownika SSH.</span><span class="sxs-lookup"><span data-stu-id="35a34-150">(The default username is **admin**.) You are also prompted to enter the SSH user password.</span></span> <span data-ttu-id="35a34-151">(Domyślna nazwa użytkownika SSH to **sshuser**.)</span><span class="sxs-lookup"><span data-stu-id="35a34-151">(The default SSH username is **sshuser**.)</span></span>  

<span data-ttu-id="35a34-152">Aby uzyskać więcej informacji, zobacz [wdrażanie przy użyciu programu PowerShell](../azure-resource-manager/resource-group-template-deploy.md#deploy-local-template).</span><span class="sxs-lookup"><span data-stu-id="35a34-152">For more information, see  [Deploy with PowerShell](../azure-resource-manager/resource-group-template-deploy.md#deploy-local-template).</span></span>

## <a name="deploy-with-cli"></a><span data-ttu-id="35a34-153">Rozmieszczanie za pomocą interfejsu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="35a34-153">Deploy with CLI</span></span>
<span data-ttu-id="35a34-154">W poniższym przykładzie użyto Azure interfejsu wiersza polecenia (CLI).</span><span class="sxs-lookup"><span data-stu-id="35a34-154">The following sample uses Azure command-line interface (CLI).</span></span> <span data-ttu-id="35a34-155">Tworzy klastra i jego zależne konto magazynu i kontener wywołując szablonu usługi Resource Manager:</span><span class="sxs-lookup"><span data-stu-id="35a34-155">It creates a cluster and its dependent storage account and container by calling a Resource Manager template:</span></span>

    azure login
    azure config mode arm
    azure group create -n hdi1229rg -l "East US"
    azure group deployment create --resource-group "hdi1229rg" --name "hdi1229" --template-file "C:\HDITutorials-ARM\hdinsight-arm-template.json"

<span data-ttu-id="35a34-156">Zostanie wyświetlony monit o wprowadzenie:</span><span class="sxs-lookup"><span data-stu-id="35a34-156">You are prompted to enter:</span></span>
* <span data-ttu-id="35a34-157">Nazwa klastra.</span><span class="sxs-lookup"><span data-stu-id="35a34-157">The cluster name.</span></span>
* <span data-ttu-id="35a34-158">Hasło użytkownika klastra.</span><span class="sxs-lookup"><span data-stu-id="35a34-158">The cluster user password.</span></span> <span data-ttu-id="35a34-159">(Domyślna nazwa użytkownika to **admin**.)</span><span class="sxs-lookup"><span data-stu-id="35a34-159">(The default username is **admin**.)</span></span>
* <span data-ttu-id="35a34-160">Hasło użytkownika SSH.</span><span class="sxs-lookup"><span data-stu-id="35a34-160">The SSH user password.</span></span> <span data-ttu-id="35a34-161">(Domyślna nazwa użytkownika SSH to **sshuser**.)</span><span class="sxs-lookup"><span data-stu-id="35a34-161">(The default SSH username is **sshuser**.)</span></span>

<span data-ttu-id="35a34-162">Poniższy kod zapewnia wbudowany parametry:</span><span class="sxs-lookup"><span data-stu-id="35a34-162">The following code provides inline parameters:</span></span>

    azure group deployment create --resource-group "hdi1229rg" --name "hdi1229" --template-file "c:\Tutorials\HDInsightARM\create-linux-based-hadoop-cluster-in-hdinsight.json" --parameters '{\"clusterName\":{\"value\":\"hdi1229\"},\"clusterLoginPassword\":{\"value\":\"Pass@word1\"},\"sshPassword\":{\"value\":\"Pass@word1\"}}'

## <a name="deploy-with-the-rest-api"></a><span data-ttu-id="35a34-163">Rozmieszczanie za pomocą interfejsu API REST</span><span class="sxs-lookup"><span data-stu-id="35a34-163">Deploy with the REST API</span></span>
<span data-ttu-id="35a34-164">Zobacz [wdrażanie przy użyciu interfejsu API REST](../azure-resource-manager/resource-group-template-deploy-rest.md).</span><span class="sxs-lookup"><span data-stu-id="35a34-164">See [Deploy with the REST API](../azure-resource-manager/resource-group-template-deploy-rest.md).</span></span>

## <a name="deploy-with-visual-studio"></a><span data-ttu-id="35a34-165">Wdrażanie za pomocą programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="35a34-165">Deploy with Visual Studio</span></span>
 <span data-ttu-id="35a34-166">Tworzenie projektu grupy zasobów i wdrożyć go na platformie Azure za pomocą interfejsu użytkownika za pomocą programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="35a34-166">Use Visual Studio to create a resource group project and deploy it to Azure through the user interface.</span></span> <span data-ttu-id="35a34-167">Należy wybrać typ zasobów do uwzględnienia w projekcie.</span><span class="sxs-lookup"><span data-stu-id="35a34-167">You select the type of resources to include in your project.</span></span> <span data-ttu-id="35a34-168">Te zasoby są automatycznie dodawane do szablonu usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="35a34-168">Those resources are automatically added to the Resource Manager template.</span></span> <span data-ttu-id="35a34-169">Projekt zapewnia również skrypt programu PowerShell do wdrożenia szablonu.</span><span class="sxs-lookup"><span data-stu-id="35a34-169">The project also provides a PowerShell script to deploy the template.</span></span>

<span data-ttu-id="35a34-170">Aby obejrzeć wprowadzenie do korzystania z programu Visual Studio z grupami zasobów, zobacz [tworzenie i wdrażanie grup zasobów platformy Azure za pomocą programu Visual Studio](../azure-resource-manager/vs-azure-tools-resource-groups-deployment-projects-create-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="35a34-170">For an introduction to using Visual Studio with resource groups, see [Creating and deploying Azure resource groups through Visual Studio](../azure-resource-manager/vs-azure-tools-resource-groups-deployment-projects-create-deploy.md).</span></span>

## <a name="troubleshoot"></a><span data-ttu-id="35a34-171">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="35a34-171">Troubleshoot</span></span>

<span data-ttu-id="35a34-172">W razie problemów podczas tworzenia klastrów usługi HDInsight zapoznaj się z [wymaganiami dotyczącymi kontroli dostępu](hdinsight-administer-use-portal-linux.md#create-clusters).</span><span class="sxs-lookup"><span data-stu-id="35a34-172">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="35a34-173">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="35a34-173">Next steps</span></span>
<span data-ttu-id="35a34-174">W tym artykule uzyskanych kilka sposobów tworzenia klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="35a34-174">In this article, you have learned several ways to create an HDInsight cluster.</span></span> <span data-ttu-id="35a34-175">Aby dowiedzieć się więcej, zobacz następujące artykuły:</span><span class="sxs-lookup"><span data-stu-id="35a34-175">To learn more, see the following articles:</span></span>

* <span data-ttu-id="35a34-176">Na przykład wdrażania zasobów za pomocą biblioteki klienta .NET, zobacz [wdrażanie zasobów przy użyciu bibliotek .NET oraz szablonu](../virtual-machines/windows/csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="35a34-176">For an example of deploying resources through the .NET client library, see [Deploy resources by using .NET libraries and a template](../virtual-machines/windows/csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="35a34-177">Szczegółowy przykład wdrażania aplikacji, zobacz [udostępniania i wdrażanie mikrousług przewidywalnego na platformie Azure](../app-service-web/app-service-deploy-complex-application-predictably.md).</span><span class="sxs-lookup"><span data-stu-id="35a34-177">For an in-depth example of deploying an application, see [Provision and deploy microservices predictably in Azure](../app-service-web/app-service-deploy-complex-application-predictably.md).</span></span>
* <span data-ttu-id="35a34-178">Aby uzyskać wskazówki dotyczące wdrażania rozwiązania w różnych środowiskach, zobacz [Development and test environments in Microsoft Azure](../solution-dev-test-environments.md) (Środowiska projektowe i testowe na platformie Microsoft Azure).</span><span class="sxs-lookup"><span data-stu-id="35a34-178">For guidance on deploying your solution to different environments, see [Development and test environments in Microsoft Azure](../solution-dev-test-environments.md).</span></span>
* <span data-ttu-id="35a34-179">Informacje na temat części szablonu usługi Azure Resource Manager, zobacz [tworzenia szablonów](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="35a34-179">To learn about the sections of the Azure Resource Manager template, see [Authoring templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="35a34-180">Aby uzyskać listę funkcji, można użyć w szablonie usługi Azure Resource Manager, zobacz [szablonu funkcji](../azure-resource-manager/resource-group-template-functions.md).</span><span class="sxs-lookup"><span data-stu-id="35a34-180">For a list of the functions you can use in an Azure Resource Manager template, see [Template functions](../azure-resource-manager/resource-group-template-functions.md).</span></span>

## <a name="appendix-resource-manager-template-to-create-a-hadoop-cluster"></a><span data-ttu-id="35a34-181">Dodatek: Szablonu usługi Resource Manager do tworzenia klastra usługi Hadoop</span><span class="sxs-lookup"><span data-stu-id="35a34-181">Appendix: Resource Manager template to create a Hadoop cluster</span></span>
<span data-ttu-id="35a34-182">Następujący szablon usługi Azure Resource Manager tworzy klaster opartą na systemie Linux platformą Hadoop przy użyciu konta magazynu Azure zależnego.</span><span class="sxs-lookup"><span data-stu-id="35a34-182">The following Azure Resource Manager template creates a Linux-based Hadoop cluster with the dependent Azure storage account.</span></span>

> [!NOTE]
> <span data-ttu-id="35a34-183">Ten przykład zawiera informacje o konfiguracji na potrzeby magazynu metadanych Hive i potrzeby magazynu metadanych Oozie.</span><span class="sxs-lookup"><span data-stu-id="35a34-183">This sample includes configuration information for Hive metastore and Oozie metastore.</span></span> <span data-ttu-id="35a34-184">Usuń sekcję lub skonfiguruj sekcji przed rozpoczęciem korzystania z szablonu.</span><span class="sxs-lookup"><span data-stu-id="35a34-184">Remove the section or configure the section before using the template.</span></span>
>
>

    {
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "clusterName": {
        "type": "string",
        "metadata": {
            "description": "The name of the HDInsight cluster to create."
        }
        },
        "clusterLoginUserName": {
        "type": "string",
        "defaultValue": "admin",
        "metadata": {
            "description": "These credentials can be used to submit jobs to the cluster and to log into cluster dashboards."
        }
        },
        "clusterLoginPassword": {
        "type": "securestring",
        "metadata": {
            "description": "The password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
        }
        },
        "sshUserName": {
        "type": "string",
        "defaultValue": "sshuser",
        "metadata": {
            "description": "These credentials can be used to remotely access the cluster."
        }
        },
        "sshPassword": {
        "type": "securestring",
        "metadata": {
            "description": "The password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
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
            "description": "The location where all azure resources will be deployed."
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
            "description": "The type of the HDInsight cluster to create."
        }
        },
        "clusterWorkerNodeCount": {
        "type": "int",
        "defaultValue": 2,
        "metadata": {
            "description": "The number of nodes in the HDInsight cluster."
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

## <a name="appendix-resource-manager-template-to-create-a-spark-cluster"></a><span data-ttu-id="35a34-185">Dodatek: Menedżer zasobów szablonu w celu utworzenia klastra Spark</span><span class="sxs-lookup"><span data-stu-id="35a34-185">Appendix: Resource Manager template to create a Spark cluster</span></span>

<span data-ttu-id="35a34-186">Ta sekcja zawiera szablonu usługi Resource Manager, który można użyć do utworzenia klastra Spark w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="35a34-186">This section provides a Resource Manager template that you can use to create an HDInsight Spark cluster.</span></span> <span data-ttu-id="35a34-187">Ten szablon obejmuje konfiguracje `spark-defaults` i `spark-thrift-sparkconf` (dla klastry Spark 1.6) i `spark2-defaults` i `spark2-thrift-sparkconf` (dla klastry Spark 2).</span><span class="sxs-lookup"><span data-stu-id="35a34-187">This template includes configurations for `spark-defaults` and `spark-thrift-sparkconf` (for Spark 1.6 clusters) and `spark2-defaults` and `spark2-thrift-sparkconf` (for Spark 2 clusters).</span></span> <span data-ttu-id="35a34-188">Oprócz tego HDInsight oblicza i ustawia konfiguracje, takie jak `spark.executor.instances`, `spark.executor.memory`, i `spark.executor.cores` na podstawie rozmiaru klastra.</span><span class="sxs-lookup"><span data-stu-id="35a34-188">In addition to this, HDInsight calculates and sets configurations such as `spark.executor.instances`, `spark.executor.memory`, and `spark.executor.cores` based on the cluster size.</span></span> 

<span data-ttu-id="35a34-189">Jeśli ustawisz wszystkie jeden parametr w sekcji jako część samego szablonu HDInsight nie Oblicz i ustaw inne parametry tej samej sekcji.</span><span class="sxs-lookup"><span data-stu-id="35a34-189">If you set any one parameter in a section as part of the template itself, HDInsight does not calculate and set the other parameters of the same section.</span></span> <span data-ttu-id="35a34-190">Na przykład parametr `spark.executor.instances` w `spark-defaults` konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="35a34-190">For example, parameter `spark.executor.instances` is in the  `spark-defaults` configuration.</span></span> <span data-ttu-id="35a34-191">Jeśli ustawisz parametr innego (na przykład `spark.yarn.exector.memoryOverhead`) w `spark-defaults` konfiguracji, HDInsight nie obliczenia i ustaw `spark.executor.instances` również parametr.</span><span class="sxs-lookup"><span data-stu-id="35a34-191">If you set another parameter (for example, `spark.yarn.exector.memoryOverhead`) in the `spark-defaults` configuration, HDInsight does not calculate and set the `spark.executor.instances` parameter as well.</span></span>

    {
    "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
    "contentVersion": "0.9.0.0",
    "parameters": {
        "clusterName": {
            "type": "string",
            "metadata": {
                "description": "The name of the HDInsight cluster to create."
            }
        },
        "clusterLoginUserName": {
            "type": "string",
            "defaultValue": "admin",
            "metadata": {
                "description": "These credentials can be used to submit jobs to the cluster and to log into cluster dashboards."
            }
        },
        "clusterLoginPassword": {
            "type": "securestring",
            "metadata": {
                "description": "The password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
            }
        },
        "location": {
            "type": "string",
            "defaultValue": "southcentralus",
            "metadata": {
                "description": "The location where all azure resources will be deployed."
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
                "description": "The number of nodes in the HDInsight cluster."
            }
        },
        "clusterKind": {
            "type": "string",
            "defaultValue": "SPARK",
            "metadata": {
                "description": "The type of the HDInsight cluster to create."
            }
        },
        "sshUserName": {
            "type": "string",
            "defaultValue": "sshuser",
            "metadata": {
                "description": "These credentials can be used to remotely access the cluster."
            }
        },
        "sshPassword": {
            "type": "securestring",
            "metadata": {
                "description": "The password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
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
