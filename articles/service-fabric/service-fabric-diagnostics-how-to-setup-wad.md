---
title: "Zbieranie dzienników przy użyciu diagnostyki Azure | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak skonfigurować diagnostyki Azure do zbierania dzienników z klastra sieci szkieletowej usług działających na platformie Azure."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 9f7e1fa5-6543-4efd-b53f-39510f18df56
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/30/2017
ms.author: dekapur
ms.openlocfilehash: 190a8a393f2e7d74a792db4efa81f94a18b02221
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="collect-logs-by-using-azure-diagnostics"></a><span data-ttu-id="fe072-103">Zbieranie dzienników za pomocą Diagnostyki Azure</span><span class="sxs-lookup"><span data-stu-id="fe072-103">Collect logs by using Azure Diagnostics</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="fe072-104">Windows</span><span class="sxs-lookup"><span data-stu-id="fe072-104">Windows</span></span>](service-fabric-diagnostics-how-to-setup-wad.md)
> * [<span data-ttu-id="fe072-105">Linux</span><span class="sxs-lookup"><span data-stu-id="fe072-105">Linux</span></span>](service-fabric-diagnostics-how-to-setup-lad.md)
> 
> 

<span data-ttu-id="fe072-106">Jeśli korzystasz z klastra usługi sieć szkieletowa usług Azure, jest dobrym pomysłem jest zebrać dzienniki ze wszystkich węzłów w centralnej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="fe072-106">When you're running an Azure Service Fabric cluster, it's a good idea to collect the logs from all the nodes in a central location.</span></span> <span data-ttu-id="fe072-107">Posiadanie dzienniki w centralnej lokalizacji ułatwiają analizowanie i rozwiązywanie problemów w klastrze lub problemy w aplikacji i usług działających w klastrze.</span><span class="sxs-lookup"><span data-stu-id="fe072-107">Having the logs in a central location helps you analyze and troubleshoot issues in your cluster, or issues in the applications and services running in that cluster.</span></span>

<span data-ttu-id="fe072-108">Jednym ze sposobów przekazywania i zbierania dzienników jest używane rozszerzenie diagnostyki Azure, która przekazuje dzienniki do magazynu Azure, Azure Application Insights lub usługi Azure Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="fe072-108">One way to upload and collect logs is to use the Azure Diagnostics extension, which uploads logs to Azure Storage, Azure Application Insights, or Azure Event Hubs.</span></span> <span data-ttu-id="fe072-109">Dzienniki nie są to przydatne, bezpośrednio w magazynie lub w usłudze Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="fe072-109">The logs are not that useful directly in storage or in Event Hubs.</span></span> <span data-ttu-id="fe072-110">Proces zewnętrzny można używać do odczytywania zdarzenia z magazynu i umieszczenie ich w produkcie takich jak [analizy dzienników](../log-analytics/log-analytics-service-fabric.md) lub innego rozwiązania do analizowania dziennika.</span><span class="sxs-lookup"><span data-stu-id="fe072-110">But you can use an external process to read the events from storage and place them in a product such as [Log Analytics](../log-analytics/log-analytics-service-fabric.md) or another log-parsing solution.</span></span> <span data-ttu-id="fe072-111">[Azure Application Insights](https://azure.microsoft.com/services/application-insights/) zawiera kompleksowe dziennik wyszukiwania i analiza usługi wbudowanych.</span><span class="sxs-lookup"><span data-stu-id="fe072-111">[Azure Application Insights](https://azure.microsoft.com/services/application-insights/) comes with a comprehensive log search and analytics service built-in.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fe072-112">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="fe072-112">Prerequisites</span></span>
<span data-ttu-id="fe072-113">Za pomocą tych narzędzi do wykonywania niektórych czynności w tym dokumencie:</span><span class="sxs-lookup"><span data-stu-id="fe072-113">You use these tools to perform some of the operations in this document:</span></span>

* <span data-ttu-id="fe072-114">[Diagnostyka Azure](../cloud-services/cloud-services-dotnet-diagnostics.md) (związane z usług Azure Cloud Services, ale ma dobrej informacje i przykłady)</span><span class="sxs-lookup"><span data-stu-id="fe072-114">[Azure Diagnostics](../cloud-services/cloud-services-dotnet-diagnostics.md) (related to Azure Cloud Services but has good information and examples)</span></span>
* [<span data-ttu-id="fe072-115">Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="fe072-115">Azure Resource Manager</span></span>](../azure-resource-manager/resource-group-overview.md)
* [<span data-ttu-id="fe072-116">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="fe072-116">Azure PowerShell</span></span>](/powershell/azure/overview)
* [<span data-ttu-id="fe072-117">Klient usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="fe072-117">Azure Resource Manager client</span></span>](https://github.com/projectkudu/ARMClient)
* [<span data-ttu-id="fe072-118">Szablon usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="fe072-118">Azure Resource Manager template</span></span>](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="log-sources-that-you-might-want-to-collect"></a><span data-ttu-id="fe072-119">Dziennik źródła, które mają być zbierane</span><span class="sxs-lookup"><span data-stu-id="fe072-119">Log sources that you might want to collect</span></span>
* <span data-ttu-id="fe072-120">**Dzienniki usługi sieć szkieletowa**: emitowanych przez platformę do standardowych kanałów funkcji Śledzenie zdarzeń systemu Windows () i EventSource.</span><span class="sxs-lookup"><span data-stu-id="fe072-120">**Service Fabric logs**: Emitted from the platform to standard Event Tracing for Windows (ETW) and EventSource channels.</span></span> <span data-ttu-id="fe072-121">Dzienniki może być jednym z kilku typów:</span><span class="sxs-lookup"><span data-stu-id="fe072-121">Logs can be one of several types:</span></span>
  * <span data-ttu-id="fe072-122">Zdarzenia operacyjne: dzienniki dla operacji, które wykonuje platformy sieć szkieletowa usług.</span><span class="sxs-lookup"><span data-stu-id="fe072-122">Operational events: Logs for operations that the Service Fabric platform performs.</span></span> <span data-ttu-id="fe072-123">Tworzenie aplikacji i usług, zmian stanu węzła i informacje o uaktualnianiu przykładami.</span><span class="sxs-lookup"><span data-stu-id="fe072-123">Examples include creation of applications and services, node state changes, and upgrade information.</span></span>
  * [<span data-ttu-id="fe072-124">Reliable Actors zdarzeń modelu programowania</span><span class="sxs-lookup"><span data-stu-id="fe072-124">Reliable Actors programming model events</span></span>](service-fabric-reliable-actors-diagnostics.md)
  * [<span data-ttu-id="fe072-125">Niezawodne usługi zdarzeń modelu programowania</span><span class="sxs-lookup"><span data-stu-id="fe072-125">Reliable Services programming model events</span></span>](service-fabric-reliable-services-diagnostics.md)
* <span data-ttu-id="fe072-126">**Zdarzenia aplikacji**: zdarzenia wysyłanego z kodu z usługą i zapisany przy użyciu Pomocnika EventSource — klasa w szablony programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="fe072-126">**Application events**: Events emitted from your service's code and written out by using the EventSource helper class provided in the Visual Studio templates.</span></span> <span data-ttu-id="fe072-127">Aby uzyskać więcej informacji na temat zapisywania dzienników z aplikacji, zobacz [monitora i diagnozowania usług w Instalatorze programowanie komputera lokalnego](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).</span><span class="sxs-lookup"><span data-stu-id="fe072-127">For more information on how to write logs from your application, see [Monitor and diagnose services in a local machine development setup](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).</span></span>

## <a name="deploy-the-diagnostics-extension"></a><span data-ttu-id="fe072-128">Wdrażanie rozszerzenia diagnostyki</span><span class="sxs-lookup"><span data-stu-id="fe072-128">Deploy the Diagnostics extension</span></span>
<span data-ttu-id="fe072-129">Pierwszym etapem zbierania dzienników jest wdrażanie rozszerzenia diagnostyki na wszystkich maszynach wirtualnych w klastrze usługi sieć szkieletowa usług.</span><span class="sxs-lookup"><span data-stu-id="fe072-129">The first step in collecting logs is to deploy the Diagnostics extension on each of the VMs in the Service Fabric cluster.</span></span> <span data-ttu-id="fe072-130">Rozszerzenie diagnostycznych zbiera dzienniki na każdej maszynie Wirtualnej i przekazuje je do konta magazynu, który określisz.</span><span class="sxs-lookup"><span data-stu-id="fe072-130">The Diagnostics extension collects logs on each VM and uploads them to the storage account that you specify.</span></span> <span data-ttu-id="fe072-131">Kroki zależą od nieco przy użyciu portalu Azure lub usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="fe072-131">The steps vary a little based on whether you use the Azure portal or Azure Resource Manager.</span></span> <span data-ttu-id="fe072-132">Kroki również różnić w zależności od tego, czy wdrożenie jest częścią tworzenia klastra lub jest dla klastra, który już istnieje.</span><span class="sxs-lookup"><span data-stu-id="fe072-132">The steps also vary based on whether the deployment is part of cluster creation or is for a cluster that already exists.</span></span> <span data-ttu-id="fe072-133">Oto kroki dla każdego scenariusza.</span><span class="sxs-lookup"><span data-stu-id="fe072-133">Let's look at the steps for each scenario.</span></span>

### <a name="deploy-the-diagnostics-extension-as-part-of-cluster-creation-through-the-portal"></a><span data-ttu-id="fe072-134">Wdrażanie rozszerzenia diagnostyki w ramach tworzenia klastra za pośrednictwem portalu</span><span class="sxs-lookup"><span data-stu-id="fe072-134">Deploy the Diagnostics extension as part of cluster creation through the portal</span></span>
<span data-ttu-id="fe072-135">Aby wdrożyć rozszerzenie diagnostyki maszyny wirtualne w klastrze, w ramach tworzenia klastra, należy użyć panelu Ustawienia diagnostyki pokazano na poniższej ilustracji.</span><span class="sxs-lookup"><span data-stu-id="fe072-135">To deploy the Diagnostics extension to the VMs in the cluster as part of cluster creation, you use the Diagnostics settings panel shown in the following image.</span></span> <span data-ttu-id="fe072-136">Aby włączyć zbieranie zdarzeń Reliable Actors lub niezawodne usługi, upewnij się, że diagnostyki jest ustawiona na **na** (ustawienie domyślne).</span><span class="sxs-lookup"><span data-stu-id="fe072-136">To enable Reliable Actors or Reliable Services event collection, ensure that Diagnostics is set to **On** (the default setting).</span></span> <span data-ttu-id="fe072-137">Po utworzeniu klastra, nie możesz zmienić te ustawienia przy użyciu portalu.</span><span class="sxs-lookup"><span data-stu-id="fe072-137">After you create the cluster, you can't change these settings by using the portal.</span></span>

![Azure ustawień diagnostycznych w portalu do tworzenia klastra](./media/service-fabric-diagnostics-how-to-setup-wad/portal-cluster-creation-diagnostics-setting.png)

<span data-ttu-id="fe072-139">Zespół pomocy technicznej platformy Azure *wymaga* obsługuje dzienniki, aby ułatwić żądań pomocy technicznej utworzonych przez Ciebie.</span><span class="sxs-lookup"><span data-stu-id="fe072-139">The Azure support team *requires* support logs to help resolve any support requests that you create.</span></span> <span data-ttu-id="fe072-140">Te dzienniki są zbierane w czasie rzeczywistym i są przechowywane w jednym z kont magazynu utworzonych w grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="fe072-140">These logs are collected in real time and are stored in one of the storage accounts created in the resource group.</span></span> <span data-ttu-id="fe072-141">Ustawienia diagnostyki skonfigurować zdarzenia na poziomie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="fe072-141">The Diagnostics settings configure application-level events.</span></span> <span data-ttu-id="fe072-142">Te zdarzenia zawierają [Reliable Actors](service-fabric-reliable-actors-diagnostics.md) zdarzenia, [niezawodne usługi](service-fabric-reliable-services-diagnostics.md) zdarzenia i niektóre zdarzenia platformy Service Fabric systemowe mają być przechowywane w usłudze Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="fe072-142">These events include [Reliable Actors](service-fabric-reliable-actors-diagnostics.md) events, [Reliable Services](service-fabric-reliable-services-diagnostics.md) events, and some system-level Service Fabric events to be stored in Azure Storage.</span></span>

<span data-ttu-id="fe072-143">Produkty, takie jak [Elasticsearch](https://www.elastic.co/guide/index.html) lub własnego procesu można pobrać zdarzenia z konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="fe072-143">Products such as [Elasticsearch](https://www.elastic.co/guide/index.html) or your own process can get the events from the storage account.</span></span> <span data-ttu-id="fe072-144">Nie ma można filtrować lub czyścić zdarzenia, które są wysyłane do tabeli.</span><span class="sxs-lookup"><span data-stu-id="fe072-144">There is currently no way to filter or groom the events that are sent to the table.</span></span> <span data-ttu-id="fe072-145">Nie można wdrożyć proces Usuń zdarzenia z tabeli, będzie nadal wzrostu tabeli.</span><span class="sxs-lookup"><span data-stu-id="fe072-145">If you don't implement a process to remove events from the table, the table will continue to grow.</span></span>

<span data-ttu-id="fe072-146">Podczas tworzenia klastra przy użyciu portalu, zalecamy pobranie szablonu **przed kliknięciem przycisku OK** do utworzenia klastra.</span><span class="sxs-lookup"><span data-stu-id="fe072-146">When you're creating a cluster by using the portal, we highly recommend that you download the template **before you click OK** to create the cluster.</span></span> <span data-ttu-id="fe072-147">Aby uzyskać więcej informacji, zapoznaj się [Konfigurowanie klastra sieci szkieletowej usług za pomocą szablonu usługi Azure Resource Manager](service-fabric-cluster-creation-via-arm.md).</span><span class="sxs-lookup"><span data-stu-id="fe072-147">For details, refer to [Set up a Service Fabric cluster by using an Azure Resource Manager template](service-fabric-cluster-creation-via-arm.md).</span></span> <span data-ttu-id="fe072-148">Musisz szablonu, aby wprowadzić zmiany później, ponieważ nie można wprowadzić kilka zmian za pomocą portalu.</span><span class="sxs-lookup"><span data-stu-id="fe072-148">You'll need the template to make changes later, because you can't make some changes by using the portal.</span></span>

<span data-ttu-id="fe072-149">Możesz wyeksportować szablony z portalu, za pomocą poniższych kroków.</span><span class="sxs-lookup"><span data-stu-id="fe072-149">You can export templates from the portal by using the following steps.</span></span> <span data-ttu-id="fe072-150">Jednak te szablony może być trudne do użycia, ponieważ mogą one mieć wartości null, których brakuje wymaganych informacji.</span><span class="sxs-lookup"><span data-stu-id="fe072-150">However, these templates can be more difficult to use because they might have null values that are missing required information.</span></span>

1. <span data-ttu-id="fe072-151">Otwórz grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="fe072-151">Open your resource group.</span></span>
2. <span data-ttu-id="fe072-152">Wybierz **ustawienia** Aby wyświetlić panel ustawień.</span><span class="sxs-lookup"><span data-stu-id="fe072-152">Select **Settings** to display the settings panel.</span></span>
3. <span data-ttu-id="fe072-153">Wybierz **wdrożeń** Aby wyświetlić panel historii wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="fe072-153">Select **Deployments** to display the deployment history panel.</span></span>
4. <span data-ttu-id="fe072-154">Wybierz wdrożenie, aby wyświetlić szczegóły wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="fe072-154">Select a deployment to display the details of the deployment.</span></span>
5. <span data-ttu-id="fe072-155">Wybierz **Eksportuj szablon** Aby wyświetlić panel szablonu.</span><span class="sxs-lookup"><span data-stu-id="fe072-155">Select **Export Template** to display the template panel.</span></span>
6. <span data-ttu-id="fe072-156">Wybierz **Zapisz do pliku** można wyeksportować plik zip zawierający szablonu, parametrów i pliki programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fe072-156">Select **Save to file** to export a .zip file that contains the template, parameter, and PowerShell files.</span></span>

<span data-ttu-id="fe072-157">Po wyeksportowaniu plików należy wprowadzić zmiany.</span><span class="sxs-lookup"><span data-stu-id="fe072-157">After you export the files, you need to make a modification.</span></span> <span data-ttu-id="fe072-158">Przeprowadź edycję pliku parameters.JSON następującym kodem, a następnie usuń **adminPassword** elementu.</span><span class="sxs-lookup"><span data-stu-id="fe072-158">Edit the parameters.json file and remove the **adminPassword** element.</span></span> <span data-ttu-id="fe072-159">To spowoduje, że monit o hasło po uruchomieniu skryptu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="fe072-159">This will cause a prompt for the password when the deployment script is run.</span></span> <span data-ttu-id="fe072-160">Po uruchomieniu skryptu wdrażania, trzeba będzie naprawić zerowe wartości parametrów.</span><span class="sxs-lookup"><span data-stu-id="fe072-160">When you're running the deployment script, you might have to fix null parameter values.</span></span>

<span data-ttu-id="fe072-161">Aby użyć pobranego szablonu, aby zaktualizować konfigurację:</span><span class="sxs-lookup"><span data-stu-id="fe072-161">To use the downloaded template to update a configuration:</span></span>

1. <span data-ttu-id="fe072-162">Wyodrębnij zawartość do folderu na komputerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="fe072-162">Extract the contents to a folder on your local computer.</span></span>
2. <span data-ttu-id="fe072-163">Zmodyfikuj zawartość w celu uwzględnienia nowej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="fe072-163">Modify the contents to reflect the new configuration.</span></span>
3. <span data-ttu-id="fe072-164">Uruchom program PowerShell i przejdź do folderu, w którym została rozpakowana zawartość.</span><span class="sxs-lookup"><span data-stu-id="fe072-164">Start PowerShell and change to the folder where you extracted the content.</span></span>
4. <span data-ttu-id="fe072-165">Uruchom **deploy.ps1** i podaj identyfikator subskrypcji, nazwa grupy zasobów (Użyj takie same nazwy, można zaktualizować konfiguracji) i nazwę unikatowego wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="fe072-165">Run **deploy.ps1** and fill in the subscription ID, the resource group name (use the same name to update the configuration), and a unique deployment name.</span></span>

### <a name="deploy-the-diagnostics-extension-as-part-of-cluster-creation-by-using-azure-resource-manager"></a><span data-ttu-id="fe072-166">Wdrażanie rozszerzenia diagnostyki w ramach tworzenia klastra przy użyciu usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="fe072-166">Deploy the Diagnostics extension as part of cluster creation by using Azure Resource Manager</span></span>
<span data-ttu-id="fe072-167">Aby utworzyć klaster przy użyciu usługi Resource Manager, należy dodać konfiguracji diagnostyki JSON do szablonu usługi Resource Manager pełne klastra przed utworzeniem klastra.</span><span class="sxs-lookup"><span data-stu-id="fe072-167">To create a cluster by using Resource Manager, you need to add the Diagnostics configuration JSON to the full cluster Resource Manager template before you create the cluster.</span></span> <span data-ttu-id="fe072-168">Udostępniamy przykładowy szablon Menedżera zasobów klastra maszyny Wirtualnej pięciu o konfiguracji diagnostyki dodana jako część nasze przykłady szablonu usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="fe072-168">We provide a sample five-VM cluster Resource Manager template with Diagnostics configuration added to it as part of our Resource Manager template samples.</span></span> <span data-ttu-id="fe072-169">Można to sprawdzić w tej lokalizacji w galerii Azure przykładów: [pięcioma węzłami klastra z przykładowy szablon Menedżera zasobów diagnostyki](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype).</span><span class="sxs-lookup"><span data-stu-id="fe072-169">You can see it at this location in the Azure Samples gallery: [Five-node cluster with Diagnostics Resource Manager template sample](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype).</span></span>

<span data-ttu-id="fe072-170">Aby wyświetlić ustawienia diagnostyki w szablonie usługi Resource Manager, otwórz plik azuredeploy.json i wyszukaj **IaaSDiagnostics**.</span><span class="sxs-lookup"><span data-stu-id="fe072-170">To see the Diagnostics setting in the Resource Manager template, open the azuredeploy.json file and search for **IaaSDiagnostics**.</span></span> <span data-ttu-id="fe072-171">Aby utworzyć klaster przy użyciu tego szablonu, wybierz **wdrażanie na platformie Azure** przycisk dostępny w poprzedniej konsolidacji.</span><span class="sxs-lookup"><span data-stu-id="fe072-171">To create a cluster by using this template, select the **Deploy to Azure** button available at the previous link.</span></span>

<span data-ttu-id="fe072-172">Alternatywnie można pobrać przykładowych Menedżera zasobów, wprowadzić zmiany i utworzyć klaster przy użyciu szablonu modyfikacji, przy użyciu `New-AzureRmResourceGroupDeployment` polecenie w oknie programu PowerShell systemu Azure.</span><span class="sxs-lookup"><span data-stu-id="fe072-172">Alternatively, you can download the Resource Manager sample, make changes to it, and create a cluster with the modified template by using the `New-AzureRmResourceGroupDeployment` command in an Azure PowerShell window.</span></span> <span data-ttu-id="fe072-173">Zobacz poniższy kod dla parametrów, które przekazujesz do polecenia.</span><span class="sxs-lookup"><span data-stu-id="fe072-173">See the following code for the parameters that you pass in to the command.</span></span> <span data-ttu-id="fe072-174">Aby uzyskać szczegółowe informacje na temat wdrażania grupy zasobów za pomocą programu PowerShell, zobacz artykuł [wdrażanie grupy zasobów przy użyciu szablonu usługi Azure Resource Manager](../azure-resource-manager/resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="fe072-174">For detailed information on how to deploy a resource group by using PowerShell, see the article [Deploy a resource group with the Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md).</span></span>

```powershell

New-AzureRmResourceGroupDeployment -ResourceGroupName $resourceGroupName -Name $deploymentName -TemplateFile $pathToARMConfigJsonFile -TemplateParameterFile $pathToParameterFile –Verbose
```

### <a name="deploy-the-diagnostics-extension-to-an-existing-cluster"></a><span data-ttu-id="fe072-175">Wdrażanie rozszerzenia diagnostyki do istniejącego klastra</span><span class="sxs-lookup"><span data-stu-id="fe072-175">Deploy the Diagnostics extension to an existing cluster</span></span>
<span data-ttu-id="fe072-176">Jeśli masz istniejący klaster nie ma wdrożonych diagnostyki lub jeśli chcesz zmodyfikować istniejącą konfigurację, można dodać lub zaktualizować.</span><span class="sxs-lookup"><span data-stu-id="fe072-176">If you have an existing cluster that doesn't have Diagnostics deployed, or if you want to modify an existing configuration, you can add or update it.</span></span> <span data-ttu-id="fe072-177">Zmodyfikuj szablonu usługi Resource Manager, który służy do tworzenia istniejącego klastra lub pobrać szablonu z portalu zgodnie z wcześniejszym opisem.</span><span class="sxs-lookup"><span data-stu-id="fe072-177">Modify the Resource Manager template that's used to create the existing cluster or download the template from the portal as described earlier.</span></span> <span data-ttu-id="fe072-178">Zmodyfikuj plik template.json, wykonując następujące zadania.</span><span class="sxs-lookup"><span data-stu-id="fe072-178">Modify the template.json file by performing the following tasks.</span></span>

<span data-ttu-id="fe072-179">Dodaj nowy zasób magazynu do szablonu przez dodanie do sekcji zasobów.</span><span class="sxs-lookup"><span data-stu-id="fe072-179">Add a new storage resource to the template by adding to the resources section.</span></span>

```json
{
  "apiVersion": "2015-05-01-preview",
  "type": "Microsoft.Storage/storageAccounts",
  "name": "[parameters('applicationDiagnosticsStorageAccountName')]",
  "location": "[parameters('computeLocation')]",
  "properties": {
    "accountType": "[parameters('applicationDiagnosticsStorageAccountType')]"
  },
  "tags": {
    "resourceType": "Service Fabric",
    "clusterName": "[parameters('clusterName')]"
  }
},
```

 <span data-ttu-id="fe072-180">Następnie dodaj do sekcji Parametry zaraz po definicji konta magazynu, między `supportLogStorageAccountName` i `vmNodeType0Name`.</span><span class="sxs-lookup"><span data-stu-id="fe072-180">Next, add to the parameters section just after the storage account definitions, between `supportLogStorageAccountName` and `vmNodeType0Name`.</span></span> <span data-ttu-id="fe072-181">Zastąp tekst zastępczy *nazwy konta magazynu tu* z nazwą konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="fe072-181">Replace the placeholder text *storage account name goes here* with the name of the storage account.</span></span>

```json
    "applicationDiagnosticsStorageAccountType": {
      "type": "string",
      "allowedValues": [
        "Standard_LRS",
        "Standard_GRS"
      ],
      "defaultValue": "Standard_LRS",
      "metadata": {
        "description": "Replication option for the application diagnostics storage account"
      }
    },
    "applicationDiagnosticsStorageAccountName": {
      "type": "string",
      "defaultValue": "storage account name goes here",
      "metadata": {
        "description": "Name for the storage account that contains application diagnostics data from the cluster"
      }
    },
```
<span data-ttu-id="fe072-182">Następnie zaktualizuj `VirtualMachineProfile` sekcji pliku template.json przez dodanie poniższego kodu w tablicy rozszerzeń.</span><span class="sxs-lookup"><span data-stu-id="fe072-182">Then, update the `VirtualMachineProfile` section of the template.json file by adding the following code within the extensions array.</span></span> <span data-ttu-id="fe072-183">Pamiętaj dodać przecinek na początku lub na końcu, w zależności od tego, gdzie jest wstawiana.</span><span class="sxs-lookup"><span data-stu-id="fe072-183">Be sure to add a comma at the beginning or the end, depending on where it's inserted.</span></span>

```json
{
    "name": "[concat(parameters('vmNodeType0Name'),'_Microsoft.Insights.VMDiagnosticsSettings')]",
    "properties": {
        "type": "IaaSDiagnostics",
        "autoUpgradeMinorVersion": true,
        "protectedSettings": {
        "storageAccountName": "[parameters('applicationDiagnosticsStorageAccountName')]",
        "storageAccountKey": "[listKeys(resourceId('Microsoft.Storage/storageAccounts', parameters('applicationDiagnosticsStorageAccountName')),'2015-05-01-preview').key1]",
        "storageAccountEndPoint": "https://core.windows.net/"
        },
        "publisher": "Microsoft.Azure.Diagnostics",
        "settings": {
        "WadCfg": {
            "DiagnosticMonitorConfiguration": {
            "overallQuotaInMB": "50000",
            "EtwProviders": {
                "EtwEventSourceProviderConfiguration": [
                {
                    "provider": "Microsoft-ServiceFabric-Actors",
                    "scheduledTransferKeywordFilter": "1",
                    "scheduledTransferPeriod": "PT5M",
                    "DefaultEvents": {
                    "eventDestination": "ServiceFabricReliableActorEventTable"
                    }
                },
                {
                    "provider": "Microsoft-ServiceFabric-Services",
                    "scheduledTransferPeriod": "PT5M",
                    "DefaultEvents": {
                    "eventDestination": "ServiceFabricReliableServiceEventTable"
                    }
                }
                ],
                "EtwManifestProviderConfiguration": [
                {
                    "provider": "cbd93bc2-71e5-4566-b3a7-595d8eeca6e8",
                    "scheduledTransferLogLevelFilter": "Information",
                    "scheduledTransferKeywordFilter": "4611686018427387904",
                    "scheduledTransferPeriod": "PT5M",
                    "DefaultEvents": {
                    "eventDestination": "ServiceFabricSystemEventTable"
                    }
                }
                ]
            }
            }
        },
        "StorageAccount": "[parameters('applicationDiagnosticsStorageAccountName')]"
        },
        "typeHandlerVersion": "1.5"
    }
}
```

<span data-ttu-id="fe072-184">Po zmodyfikowaniu pliku template.json zgodnie z opisem, ponownie opublikować szablonu usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="fe072-184">After you modify the template.json file as described, republish the Resource Manager template.</span></span> <span data-ttu-id="fe072-185">Jeśli szablon został wyeksportowany, uruchamiania pliku deploy.ps1 je opublikuje szablonu.</span><span class="sxs-lookup"><span data-stu-id="fe072-185">If the template was exported, running the deploy.ps1 file republishes the template.</span></span> <span data-ttu-id="fe072-186">Po wdrożeniu, upewnij się, że **ProvisioningState** jest **zakończyło się pomyślnie**.</span><span class="sxs-lookup"><span data-stu-id="fe072-186">After you deploy, ensure that **ProvisioningState** is **Succeeded**.</span></span>

## <a name="update-diagnostics-to-collect-health-and-load-events"></a><span data-ttu-id="fe072-187">Zaktualizuj diagnostyki do zbierania kondycji i załadować zdarzenia</span><span class="sxs-lookup"><span data-stu-id="fe072-187">Update diagnostics to collect health and load events</span></span>

<span data-ttu-id="fe072-188">Począwszy od wersji 5.4 sieci szkieletowej usług kondycji i obciążenia metryki zdarzenia są dostępne dla kolekcji.</span><span class="sxs-lookup"><span data-stu-id="fe072-188">Starting with the 5.4 release of Service Fabric, health and load metric events are available for collection.</span></span> <span data-ttu-id="fe072-189">Te zdarzenia odzwierciedlają zdarzeń generowanych przez system lub kodu za pomocą kondycji lub załadować API raportowania, takie jak [ReportPartitionHealth](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportpartitionhealth.aspx) lub [ReportLoad](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportload.aspx).</span><span class="sxs-lookup"><span data-stu-id="fe072-189">These events reflect events generated by the system or your code by using the health or load reporting APIs such as [ReportPartitionHealth](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportpartitionhealth.aspx) or [ReportLoad](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportload.aspx).</span></span> <span data-ttu-id="fe072-190">Dzięki temu agregowanie i wyświetlanie stanu systemu wraz z upływem czasu oraz alerty na podstawie kondycji lub obciążenia zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="fe072-190">This allows for aggregating and viewing system health over time and for alerting based on health or load events.</span></span> <span data-ttu-id="fe072-191">Aby wyświetlić te zdarzenia w Podglądzie zdarzeń diagnostycznych programu Visual Studio Dodaj "Microsoft-ServiceFabric:4:0x4000000000000008" do listy dostawców ETW.</span><span class="sxs-lookup"><span data-stu-id="fe072-191">To view these events in Visual Studio's Diagnostic Event Viewer add "Microsoft-ServiceFabric:4:0x4000000000000008" to the list of ETW providers.</span></span>

<span data-ttu-id="fe072-192">Aby zbierać zdarzenia, zmodyfikuj szablon usługi resource manager do uwzględnienia</span><span class="sxs-lookup"><span data-stu-id="fe072-192">To collect the events, modify the resource manager template to include</span></span>

```json
  "EtwManifestProviderConfiguration": [
    {
      "provider": "cbd93bc2-71e5-4566-b3a7-595d8eeca6e8",
      "scheduledTransferLogLevelFilter": "Information",
      "scheduledTransferKeywordFilter": "4611686018427387912",
      "scheduledTransferPeriod": "PT5M",
      "DefaultEvents": {
        "eventDestination": "ServiceFabricSystemEventTable"
      }
    }
```

## <a name="update-diagnostics-to-collect-and-upload-logs-from-new-eventsource-channels"></a><span data-ttu-id="fe072-193">Zaktualizuj diagnostyki do gromadzenia i przekazywania dzienników z nowych kanałów źródła zdarzeń</span><span class="sxs-lookup"><span data-stu-id="fe072-193">Update Diagnostics to collect and upload logs from new EventSource channels</span></span>
<span data-ttu-id="fe072-194">Aby zaktualizować diagnostykę, aby zbieranie dzienników z nowego kanałów źródła zdarzeń, które reprezentują nowej aplikacji, które zamierzasz wdrożyć, wykonaj te same czynności co w [poprzedniej sekcji](#deploywadarm) ustawień diagnostycznych dla istniejącego klastra.</span><span class="sxs-lookup"><span data-stu-id="fe072-194">To update Diagnostics to collect logs from new EventSource channels that represent a new application that you're about to deploy, perform the same steps as in the [previous section](#deploywadarm) for setup of Diagnostics for an existing cluster.</span></span>

<span data-ttu-id="fe072-195">Zaktualizuj `EtwEventSourceProviderConfiguration` sekcji w pliku template.json można dodawać nowych kanałów EventSource przed zastosowaniem konfiguracji aktualizacji przy użyciu `New-AzureRmResourceGroupDeployment` polecenia programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fe072-195">Update the `EtwEventSourceProviderConfiguration` section in the template.json file to add entries for the new EventSource channels before you apply the configuration update by using the `New-AzureRmResourceGroupDeployment` PowerShell command.</span></span> <span data-ttu-id="fe072-196">Nazwa źródła zdarzeń jest zdefiniowany jako części kodu w pliku ServiceEventSource.cs generowanych przez program Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="fe072-196">The name of the event source is defined as part of your code in the Visual Studio-generated ServiceEventSource.cs file.</span></span>

<span data-ttu-id="fe072-197">Na przykład jeśli źródło zdarzenia jest o nazwie Mój Eventsource, Dodaj następujący kod, aby umieścić zdarzenia Moje Eventsource w tabeli o nazwie MyDestinationTableName.</span><span class="sxs-lookup"><span data-stu-id="fe072-197">For example, if your event source is named My-Eventsource, add the following code to place the events from My-Eventsource into a table named MyDestinationTableName.</span></span>

```json
        {
            "provider": "My-Eventsource",
            "scheduledTransferPeriod": "PT5M",
            "DefaultEvents": {
            "eventDestination": "MyDestinationTableName"
            }
        }
```

<span data-ttu-id="fe072-198">Aby zebrać liczników wydajności lub dzienniki zdarzeń, należy modyfikować szablonu usługi Resource Manager za pomocą przykłady podane w [Utwórz maszynę wirtualną systemu Windows z monitorowania i diagnostyki za pomocą szablonu usługi Azure Resource Manager](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="fe072-198">To collect performance counters or event logs, modify the Resource Manager template by using the examples provided in [Create a Windows virtual machine with monitoring and diagnostics by using an Azure Resource Manager template](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="fe072-199">Następnie należy ponownie opublikować szablonu usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="fe072-199">Then, republish the Resource Manager template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fe072-200">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="fe072-200">Next steps</span></span>
<span data-ttu-id="fe072-201">Aby bardziej szczegółowo zrozumieć, jakie zdarzenia należy szukać podczas rozwiązywania problemów, zobacz zdarzeń diagnostycznych wysyłanego do [Reliable Actors](service-fabric-reliable-actors-diagnostics.md) i [niezawodne usługi](service-fabric-reliable-services-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="fe072-201">To understand in more detail what events you should look for while troubleshooting issues, see the diagnostic events emitted for [Reliable Actors](service-fabric-reliable-actors-diagnostics.md) and [Reliable Services](service-fabric-reliable-services-diagnostics.md).</span></span>

## <a name="related-articles"></a><span data-ttu-id="fe072-202">Pokrewne artykuły:</span><span class="sxs-lookup"><span data-stu-id="fe072-202">Related articles</span></span>
* [<span data-ttu-id="fe072-203">Dowiedz się, jak zbierania liczników wydajności lub dzienniki przy użyciu rozszerzenia diagnostyki</span><span class="sxs-lookup"><span data-stu-id="fe072-203">Learn how to collect performance counters or logs by using the Diagnostics extension</span></span>](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="fe072-204">Rozwiązania sieci szkieletowej usług analizy dzienników</span><span class="sxs-lookup"><span data-stu-id="fe072-204">Service Fabric solution in Log Analytics</span></span>](../log-analytics/log-analytics-service-fabric.md)

