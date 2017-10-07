---
title: "Dzienniki aaaCollect za pomocą diagnostyki Azure | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano sposób rejestrowania tooset się toocollect diagnostyki Azure z klastra usługi sieć szkieletowa usług działających na platformie Azure."
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
ms.openlocfilehash: afbcfbe972b1847ef33bf0539b4398794b1bd56b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="collect-logs-by-using-azure-diagnostics"></a><span data-ttu-id="7d7de-103">Zbieranie dzienników za pomocą Diagnostyki Azure</span><span class="sxs-lookup"><span data-stu-id="7d7de-103">Collect logs by using Azure Diagnostics</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7d7de-104">Windows</span><span class="sxs-lookup"><span data-stu-id="7d7de-104">Windows</span></span>](service-fabric-diagnostics-how-to-setup-wad.md)
> * [<span data-ttu-id="7d7de-105">Linux</span><span class="sxs-lookup"><span data-stu-id="7d7de-105">Linux</span></span>](service-fabric-diagnostics-how-to-setup-lad.md)
> 
> 

<span data-ttu-id="7d7de-106">Jeśli korzystasz z klastra usługi sieć szkieletowa usług Azure, jest dobrze toocollect hello dzienniki ze wszystkich węzłów hello w centralnej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="7d7de-106">When you're running an Azure Service Fabric cluster, it's a good idea toocollect hello logs from all hello nodes in a central location.</span></span> <span data-ttu-id="7d7de-107">O dzienniki hello w centralnej lokalizacji ułatwiają analizowanie i rozwiązywanie problemów w klastrze, lub problemy w hello aplikacje i usługi działające w klastrze.</span><span class="sxs-lookup"><span data-stu-id="7d7de-107">Having hello logs in a central location helps you analyze and troubleshoot issues in your cluster, or issues in hello applications and services running in that cluster.</span></span>

<span data-ttu-id="7d7de-108">Jednym ze sposobów tooupload i zbieranie dzienników jest toouse hello Azure Diagnostics rozszerzenia, które przekazywania dzienników tooAzure magazynu Azure Application Insights i usługi Azure Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="7d7de-108">One way tooupload and collect logs is toouse hello Azure Diagnostics extension, which uploads logs tooAzure Storage, Azure Application Insights, or Azure Event Hubs.</span></span> <span data-ttu-id="7d7de-109">Witaj dzienniki nie są to przydatne, bezpośrednio w magazynie lub w usłudze Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="7d7de-109">hello logs are not that useful directly in storage or in Event Hubs.</span></span> <span data-ttu-id="7d7de-110">Można jednak użyć procesu zewnętrznego tooread hello zdarzenia z magazynu i umieszczenie ich w produkcie takich jak [analizy dzienników](../log-analytics/log-analytics-service-fabric.md) lub innego rozwiązania do analizowania dziennika.</span><span class="sxs-lookup"><span data-stu-id="7d7de-110">But you can use an external process tooread hello events from storage and place them in a product such as [Log Analytics](../log-analytics/log-analytics-service-fabric.md) or another log-parsing solution.</span></span> <span data-ttu-id="7d7de-111">[Azure Application Insights](https://azure.microsoft.com/services/application-insights/) zawiera kompleksowe dziennik wyszukiwania i analiza usługi wbudowanych.</span><span class="sxs-lookup"><span data-stu-id="7d7de-111">[Azure Application Insights](https://azure.microsoft.com/services/application-insights/) comes with a comprehensive log search and analytics service built-in.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7d7de-112">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="7d7de-112">Prerequisites</span></span>
<span data-ttu-id="7d7de-113">Użyj tych narzędzi tooperform niektóre operacje hello w tym dokumencie:</span><span class="sxs-lookup"><span data-stu-id="7d7de-113">You use these tools tooperform some of hello operations in this document:</span></span>

* <span data-ttu-id="7d7de-114">[Diagnostyka Azure](../cloud-services/cloud-services-dotnet-diagnostics.md) (dotyczących tooAzure usługi w chmurze, lecz jest dobrym informacje i przykłady)</span><span class="sxs-lookup"><span data-stu-id="7d7de-114">[Azure Diagnostics](../cloud-services/cloud-services-dotnet-diagnostics.md) (related tooAzure Cloud Services but has good information and examples)</span></span>
* [<span data-ttu-id="7d7de-115">Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="7d7de-115">Azure Resource Manager</span></span>](../azure-resource-manager/resource-group-overview.md)
* [<span data-ttu-id="7d7de-116">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="7d7de-116">Azure PowerShell</span></span>](/powershell/azure/overview)
* [<span data-ttu-id="7d7de-117">Klient usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="7d7de-117">Azure Resource Manager client</span></span>](https://github.com/projectkudu/ARMClient)
* [<span data-ttu-id="7d7de-118">Szablon usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="7d7de-118">Azure Resource Manager template</span></span>](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="log-sources-that-you-might-want-toocollect"></a><span data-ttu-id="7d7de-119">Dziennik źródeł rozważ toocollect</span><span class="sxs-lookup"><span data-stu-id="7d7de-119">Log sources that you might want toocollect</span></span>
* <span data-ttu-id="7d7de-120">**Dzienniki usługi sieć szkieletowa**: wysyłanego z hello platformy toostandard funkcji Śledzenie zdarzeń systemu Windows () i EventSource kanałów.</span><span class="sxs-lookup"><span data-stu-id="7d7de-120">**Service Fabric logs**: Emitted from hello platform toostandard Event Tracing for Windows (ETW) and EventSource channels.</span></span> <span data-ttu-id="7d7de-121">Dzienniki może być jednym z kilku typów:</span><span class="sxs-lookup"><span data-stu-id="7d7de-121">Logs can be one of several types:</span></span>
  * <span data-ttu-id="7d7de-122">Zdarzenia operacyjne: dzienniki dla operacji, które hello wykonuje platformy sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="7d7de-122">Operational events: Logs for operations that hello Service Fabric platform performs.</span></span> <span data-ttu-id="7d7de-123">Tworzenie aplikacji i usług, zmian stanu węzła i informacje o uaktualnianiu przykładami.</span><span class="sxs-lookup"><span data-stu-id="7d7de-123">Examples include creation of applications and services, node state changes, and upgrade information.</span></span>
  * [<span data-ttu-id="7d7de-124">Reliable Actors zdarzeń modelu programowania</span><span class="sxs-lookup"><span data-stu-id="7d7de-124">Reliable Actors programming model events</span></span>](service-fabric-reliable-actors-diagnostics.md)
  * [<span data-ttu-id="7d7de-125">Niezawodne usługi zdarzeń modelu programowania</span><span class="sxs-lookup"><span data-stu-id="7d7de-125">Reliable Services programming model events</span></span>](service-fabric-reliable-services-diagnostics.md)
* <span data-ttu-id="7d7de-126">**Zdarzenia aplikacji**: zdarzenia wysyłanego z kodu z usługą i zapisany przy użyciu klasy pomocy EventSource hello w hello szablony programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7d7de-126">**Application events**: Events emitted from your service's code and written out by using hello EventSource helper class provided in hello Visual Studio templates.</span></span> <span data-ttu-id="7d7de-127">Aby uzyskać więcej informacji dotyczących sposobu toowrite logowania z aplikacji, zobacz [monitora i diagnozowania usług w Instalatorze programowanie komputera lokalnego](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).</span><span class="sxs-lookup"><span data-stu-id="7d7de-127">For more information on how toowrite logs from your application, see [Monitor and diagnose services in a local machine development setup](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).</span></span>

## <a name="deploy-hello-diagnostics-extension"></a><span data-ttu-id="7d7de-128">Wdrażanie rozszerzenia diagnostyki hello</span><span class="sxs-lookup"><span data-stu-id="7d7de-128">Deploy hello Diagnostics extension</span></span>
<span data-ttu-id="7d7de-129">pierwszym krokiem Hello zbierania dzienników jest rozszerzeniem diagnostyki hello toodeploy na poszczególnych maszyn wirtualnych hello w klastrze usługi sieć szkieletowa hello.</span><span class="sxs-lookup"><span data-stu-id="7d7de-129">hello first step in collecting logs is toodeploy hello Diagnostics extension on each of hello VMs in hello Service Fabric cluster.</span></span> <span data-ttu-id="7d7de-130">Hello rozszerzenia diagnostyki zbiera dzienniki na każdej maszynie Wirtualnej i przekazuje je toohello konta magazynu, który określisz.</span><span class="sxs-lookup"><span data-stu-id="7d7de-130">hello Diagnostics extension collects logs on each VM and uploads them toohello storage account that you specify.</span></span> <span data-ttu-id="7d7de-131">kroki Hello zależą od nieco przy użyciu hello portalu Azure lub usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="7d7de-131">hello steps vary a little based on whether you use hello Azure portal or Azure Resource Manager.</span></span> <span data-ttu-id="7d7de-132">kroki Hello również różnić w zależności od czy wdrożenia hello jest częścią tworzenia klastra lub dla klastra, który już istnieje.</span><span class="sxs-lookup"><span data-stu-id="7d7de-132">hello steps also vary based on whether hello deployment is part of cluster creation or is for a cluster that already exists.</span></span> <span data-ttu-id="7d7de-133">Przyjrzyjmy się hello kroki dla każdego scenariusza.</span><span class="sxs-lookup"><span data-stu-id="7d7de-133">Let's look at hello steps for each scenario.</span></span>

### <a name="deploy-hello-diagnostics-extension-as-part-of-cluster-creation-through-hello-portal"></a><span data-ttu-id="7d7de-134">Wdrażanie rozszerzenia diagnostyki hello w ramach tworzenia klastra za pośrednictwem portalu hello</span><span class="sxs-lookup"><span data-stu-id="7d7de-134">Deploy hello Diagnostics extension as part of cluster creation through hello portal</span></span>
<span data-ttu-id="7d7de-135">toodeploy hello diagnostyki rozszerzenia toohello maszyn wirtualnych w klastrze hello w ramach tworzenia klastra, możesz użyć panel ustawień diagnostyki hello pokazano powitania po obrazu.</span><span class="sxs-lookup"><span data-stu-id="7d7de-135">toodeploy hello Diagnostics extension toohello VMs in hello cluster as part of cluster creation, you use hello Diagnostics settings panel shown in hello following image.</span></span> <span data-ttu-id="7d7de-136">tooenable Reliable Actors lub niezawodne usługi zbierania zdarzeń, sprawdź, czy diagnostyki jest ustawiony za**na** (hello ustawienie domyślne).</span><span class="sxs-lookup"><span data-stu-id="7d7de-136">tooenable Reliable Actors or Reliable Services event collection, ensure that Diagnostics is set too**On** (hello default setting).</span></span> <span data-ttu-id="7d7de-137">Po utworzeniu klastra hello, nie możesz zmienić te ustawienia przy użyciu portalu hello.</span><span class="sxs-lookup"><span data-stu-id="7d7de-137">After you create hello cluster, you can't change these settings by using hello portal.</span></span>

![Azure ustawień diagnostyki w portalu hello tworzenia klastra](./media/service-fabric-diagnostics-how-to-setup-wad/portal-cluster-creation-diagnostics-setting.png)

<span data-ttu-id="7d7de-139">Witaj zespołu pomocy technicznej platformy Azure *wymaga* Obsługa dzienniki toohelp Rozwiąż wszelkie tworzenia żądania obsługi.</span><span class="sxs-lookup"><span data-stu-id="7d7de-139">hello Azure support team *requires* support logs toohelp resolve any support requests that you create.</span></span> <span data-ttu-id="7d7de-140">Te dzienniki są zbierane w czasie rzeczywistym i są przechowywane w jednym z kont magazynu hello utworzonych w grupie zasobów hello.</span><span class="sxs-lookup"><span data-stu-id="7d7de-140">These logs are collected in real time and are stored in one of hello storage accounts created in hello resource group.</span></span> <span data-ttu-id="7d7de-141">ustawienia diagnostyki Hello skonfigurować zdarzenia na poziomie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7d7de-141">hello Diagnostics settings configure application-level events.</span></span> <span data-ttu-id="7d7de-142">Te zdarzenia zawierają [Reliable Actors](service-fabric-reliable-actors-diagnostics.md) zdarzenia, [niezawodne usługi](service-fabric-reliable-services-diagnostics.md) zdarzenia, a niektóre zdarzenia toobe sieci szkieletowej usług poziom systemu przechowywane w usłudze Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="7d7de-142">These events include [Reliable Actors](service-fabric-reliable-actors-diagnostics.md) events, [Reliable Services](service-fabric-reliable-services-diagnostics.md) events, and some system-level Service Fabric events toobe stored in Azure Storage.</span></span>

<span data-ttu-id="7d7de-143">Produkty, takie jak [Elasticsearch](https://www.elastic.co/guide/index.html) lub własnego procesu można uzyskać hello zdarzenia z hello konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="7d7de-143">Products such as [Elasticsearch](https://www.elastic.co/guide/index.html) or your own process can get hello events from hello storage account.</span></span> <span data-ttu-id="7d7de-144">Nie ma żadnych sposób toofilter lub Oczyść hello zdarzenia, które są wysyłane toohello tabeli.</span><span class="sxs-lookup"><span data-stu-id="7d7de-144">There is currently no way toofilter or groom hello events that are sent toohello table.</span></span> <span data-ttu-id="7d7de-145">Jeśli nie implementują zdarzenia tooremove procesu z tabeli hello, hello tabeli będzie toogrow.</span><span class="sxs-lookup"><span data-stu-id="7d7de-145">If you don't implement a process tooremove events from hello table, hello table will continue toogrow.</span></span>

<span data-ttu-id="7d7de-146">Podczas tworzenia klastra przy użyciu portalu hello, zalecamy pobranie szablonu hello **przed kliknięciem przycisku OK** toocreate hello klastra.</span><span class="sxs-lookup"><span data-stu-id="7d7de-146">When you're creating a cluster by using hello portal, we highly recommend that you download hello template **before you click OK** toocreate hello cluster.</span></span> <span data-ttu-id="7d7de-147">Aby uzyskać więcej informacji, zobacz zbyt[Konfigurowanie klastra sieci szkieletowej usług za pomocą szablonu usługi Azure Resource Manager](service-fabric-cluster-creation-via-arm.md).</span><span class="sxs-lookup"><span data-stu-id="7d7de-147">For details, refer too[Set up a Service Fabric cluster by using an Azure Resource Manager template](service-fabric-cluster-creation-via-arm.md).</span></span> <span data-ttu-id="7d7de-148">Zmiany toomake szablonu hello będą potrzebne później, ponieważ nie można wprowadzić kilka zmian przy użyciu portalu hello.</span><span class="sxs-lookup"><span data-stu-id="7d7de-148">You'll need hello template toomake changes later, because you can't make some changes by using hello portal.</span></span>

<span data-ttu-id="7d7de-149">Możesz wyeksportować szablony z portalu hello przy użyciu hello następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="7d7de-149">You can export templates from hello portal by using hello following steps.</span></span> <span data-ttu-id="7d7de-150">Jednak te szablony może być trudniejsze toouse, ponieważ mogą one mieć wartości null, których brakuje wymaganych informacji.</span><span class="sxs-lookup"><span data-stu-id="7d7de-150">However, these templates can be more difficult toouse because they might have null values that are missing required information.</span></span>

1. <span data-ttu-id="7d7de-151">Otwórz grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="7d7de-151">Open your resource group.</span></span>
2. <span data-ttu-id="7d7de-152">Wybierz **ustawienia** toodisplay hello ustawienia panelu.</span><span class="sxs-lookup"><span data-stu-id="7d7de-152">Select **Settings** toodisplay hello settings panel.</span></span>
3. <span data-ttu-id="7d7de-153">Wybierz **wdrożeń** toodisplay hello wdrożenia historii panelu.</span><span class="sxs-lookup"><span data-stu-id="7d7de-153">Select **Deployments** toodisplay hello deployment history panel.</span></span>
4. <span data-ttu-id="7d7de-154">Wybierz szczegóły hello toodisplay wdrożenia hello wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="7d7de-154">Select a deployment toodisplay hello details of hello deployment.</span></span>
5. <span data-ttu-id="7d7de-155">Wybierz **Eksportuj szablon** toodisplay hello szablonu panelu.</span><span class="sxs-lookup"><span data-stu-id="7d7de-155">Select **Export Template** toodisplay hello template panel.</span></span>
6. <span data-ttu-id="7d7de-156">Wybierz **zapisać toofile** tooexport plik zip zawierający hello szablonu, parametrów i pliki programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7d7de-156">Select **Save toofile** tooexport a .zip file that contains hello template, parameter, and PowerShell files.</span></span>

<span data-ttu-id="7d7de-157">Po wyeksportowaniu hello plików należy toomake modyfikację.</span><span class="sxs-lookup"><span data-stu-id="7d7de-157">After you export hello files, you need toomake a modification.</span></span> <span data-ttu-id="7d7de-158">Edytuj plik parameters.JSON następującym kodem hello i Usuń hello **adminPassword** elementu.</span><span class="sxs-lookup"><span data-stu-id="7d7de-158">Edit hello parameters.json file and remove hello **adminPassword** element.</span></span> <span data-ttu-id="7d7de-159">Spowoduje to monit o hasło powitania po uruchomieniu skryptu wdrażania hello.</span><span class="sxs-lookup"><span data-stu-id="7d7de-159">This will cause a prompt for hello password when hello deployment script is run.</span></span> <span data-ttu-id="7d7de-160">Po uruchomieniu skryptu wdrażania hello może mieć wartości null parametrów toofix.</span><span class="sxs-lookup"><span data-stu-id="7d7de-160">When you're running hello deployment script, you might have toofix null parameter values.</span></span>

<span data-ttu-id="7d7de-161">Witaj toouse pobrać tooupdate szablonu konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="7d7de-161">toouse hello downloaded template tooupdate a configuration:</span></span>

1. <span data-ttu-id="7d7de-162">Wyodrębnij hello zawartość tooa folderu na komputerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="7d7de-162">Extract hello contents tooa folder on your local computer.</span></span>
2. <span data-ttu-id="7d7de-163">Zmodyfikuj hello zawartość tooreflect hello nowej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="7d7de-163">Modify hello contents tooreflect hello new configuration.</span></span>
3. <span data-ttu-id="7d7de-164">Uruchom program PowerShell i zmień toohello folder, w którym wyodrębniono zawartość hello.</span><span class="sxs-lookup"><span data-stu-id="7d7de-164">Start PowerShell and change toohello folder where you extracted hello content.</span></span>
4. <span data-ttu-id="7d7de-165">Uruchom **deploy.ps1** i podaj identyfikator subskrypcji hello, nazwa grupy zasobów hello (Użyj hello sama konfiguracja hello tooupdate nazwy) oraz nazwę unikatowego wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="7d7de-165">Run **deploy.ps1** and fill in hello subscription ID, hello resource group name (use hello same name tooupdate hello configuration), and a unique deployment name.</span></span>

### <a name="deploy-hello-diagnostics-extension-as-part-of-cluster-creation-by-using-azure-resource-manager"></a><span data-ttu-id="7d7de-166">Wdrażanie rozszerzenia diagnostyki hello w ramach tworzenia klastra przy użyciu usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="7d7de-166">Deploy hello Diagnostics extension as part of cluster creation by using Azure Resource Manager</span></span>
<span data-ttu-id="7d7de-167">toocreate klastra za pomocą Menedżera zasobów, należy tooadd hello diagnostyki konfiguracji szablonu JSON w toohello pełne klastra Menedżera zasobów przed utworzeniem klastra hello.</span><span class="sxs-lookup"><span data-stu-id="7d7de-167">toocreate a cluster by using Resource Manager, you need tooadd hello Diagnostics configuration JSON toohello full cluster Resource Manager template before you create hello cluster.</span></span> <span data-ttu-id="7d7de-168">Udostępniamy przykładowy szablon Menedżera zasobów klastra maszyny Wirtualnej pięciu o konfiguracji diagnostyki dodane tooit jako część nasze przykłady szablonu usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="7d7de-168">We provide a sample five-VM cluster Resource Manager template with Diagnostics configuration added tooit as part of our Resource Manager template samples.</span></span> <span data-ttu-id="7d7de-169">Można to sprawdzić w tej lokalizacji w galerii Azure przykładów hello: [pięcioma węzłami klastra z przykładowy szablon Menedżera zasobów diagnostyki](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype).</span><span class="sxs-lookup"><span data-stu-id="7d7de-169">You can see it at this location in hello Azure Samples gallery: [Five-node cluster with Diagnostics Resource Manager template sample](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype).</span></span>

<span data-ttu-id="7d7de-170">ustawienia diagnostyki hello toosee hello szablonu usługi Resource Manager, hello Otwórz plik azuredeploy.json i wyszukaj **IaaSDiagnostics**.</span><span class="sxs-lookup"><span data-stu-id="7d7de-170">toosee hello Diagnostics setting in hello Resource Manager template, open hello azuredeploy.json file and search for **IaaSDiagnostics**.</span></span> <span data-ttu-id="7d7de-171">toocreate klastra przy użyciu tego szablonu, wybierz opcję hello **wdrażanie tooAzure** przycisk dostępne pod adresem hello poprzedniej konsolidacji.</span><span class="sxs-lookup"><span data-stu-id="7d7de-171">toocreate a cluster by using this template, select hello **Deploy tooAzure** button available at hello previous link.</span></span>

<span data-ttu-id="7d7de-172">Alternatywnie można pobrać hello próbki Menedżera zasobów, wprowadzić zmiany tooit i utworzyć klaster przy użyciu szablonu modyfikacji hello przy użyciu hello `New-AzureRmResourceGroupDeployment` polecenie w oknie programu PowerShell systemu Azure.</span><span class="sxs-lookup"><span data-stu-id="7d7de-172">Alternatively, you can download hello Resource Manager sample, make changes tooit, and create a cluster with hello modified template by using hello `New-AzureRmResourceGroupDeployment` command in an Azure PowerShell window.</span></span> <span data-ttu-id="7d7de-173">Zobacz hello następującego kodu dla parametrów hello, które przekazujesz w poleceniu toohello.</span><span class="sxs-lookup"><span data-stu-id="7d7de-173">See hello following code for hello parameters that you pass in toohello command.</span></span> <span data-ttu-id="7d7de-174">Aby uzyskać szczegółowe informacje dotyczące sposobu toodeploy zasób grupy przy użyciu programu PowerShell, zobacz artykuł hello [wdrażanie grupy zasobów z szablonem usługi Azure Resource Manager hello](../azure-resource-manager/resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="7d7de-174">For detailed information on how toodeploy a resource group by using PowerShell, see hello article [Deploy a resource group with hello Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md).</span></span>

```powershell

New-AzureRmResourceGroupDeployment -ResourceGroupName $resourceGroupName -Name $deploymentName -TemplateFile $pathToARMConfigJsonFile -TemplateParameterFile $pathToParameterFile –Verbose
```

### <a name="deploy-hello-diagnostics-extension-tooan-existing-cluster"></a><span data-ttu-id="7d7de-175">Wdrażanie hello diagnostyki rozszerzenia tooan istniejącego klastra</span><span class="sxs-lookup"><span data-stu-id="7d7de-175">Deploy hello Diagnostics extension tooan existing cluster</span></span>
<span data-ttu-id="7d7de-176">Jeśli masz istniejący klaster nie ma wdrożonych diagnostyki lub jeśli chcesz toomodify istniejącej konfiguracji, można dodać lub zaktualizować.</span><span class="sxs-lookup"><span data-stu-id="7d7de-176">If you have an existing cluster that doesn't have Diagnostics deployed, or if you want toomodify an existing configuration, you can add or update it.</span></span> <span data-ttu-id="7d7de-177">Zmodyfikuj szablon Menedżera zasobów hello, która jest używana toocreate hello istniejącego klastra lub pobrać hello szablonu z portalu hello zgodnie z wcześniejszym opisem.</span><span class="sxs-lookup"><span data-stu-id="7d7de-177">Modify hello Resource Manager template that's used toocreate hello existing cluster or download hello template from hello portal as described earlier.</span></span> <span data-ttu-id="7d7de-178">Zmodyfikuj plik template.json hello, wykonując następujące zadania hello.</span><span class="sxs-lookup"><span data-stu-id="7d7de-178">Modify hello template.json file by performing hello following tasks.</span></span>

<span data-ttu-id="7d7de-179">Dodaj nowy szablon toohello zasobów magazynu przez dodanie toohello sekcja zasobów.</span><span class="sxs-lookup"><span data-stu-id="7d7de-179">Add a new storage resource toohello template by adding toohello resources section.</span></span>

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

 <span data-ttu-id="7d7de-180">Następnie dodaj parametry toohello sekcji zaraz po definicji konta magazynu hello, między `supportLogStorageAccountName` i `vmNodeType0Name`.</span><span class="sxs-lookup"><span data-stu-id="7d7de-180">Next, add toohello parameters section just after hello storage account definitions, between `supportLogStorageAccountName` and `vmNodeType0Name`.</span></span> <span data-ttu-id="7d7de-181">Zastąp tekst zastępczy hello *nazwy konta magazynu tu* o nazwie hello hello konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="7d7de-181">Replace hello placeholder text *storage account name goes here* with hello name of hello storage account.</span></span>

```json
    "applicationDiagnosticsStorageAccountType": {
      "type": "string",
      "allowedValues": [
        "Standard_LRS",
        "Standard_GRS"
      ],
      "defaultValue": "Standard_LRS",
      "metadata": {
        "description": "Replication option for hello application diagnostics storage account"
      }
    },
    "applicationDiagnosticsStorageAccountName": {
      "type": "string",
      "defaultValue": "storage account name goes here",
      "metadata": {
        "description": "Name for hello storage account that contains application diagnostics data from hello cluster"
      }
    },
```
<span data-ttu-id="7d7de-182">Następnie zaktualizuj hello `VirtualMachineProfile` sekcji pliku template.json hello przez dodanie hello następującego kodu w ramach hello tablica rozszerzeń.</span><span class="sxs-lookup"><span data-stu-id="7d7de-182">Then, update hello `VirtualMachineProfile` section of hello template.json file by adding hello following code within hello extensions array.</span></span> <span data-ttu-id="7d7de-183">Należy się tooadd przecinkami hello początek lub koniec hello, w zależności od tego, gdzie jest wstawiana.</span><span class="sxs-lookup"><span data-stu-id="7d7de-183">Be sure tooadd a comma at hello beginning or hello end, depending on where it's inserted.</span></span>

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

<span data-ttu-id="7d7de-184">Po zmodyfikowaniu pliku template.json hello zgodnie z opisem ponownie opublikować hello szablonu usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="7d7de-184">After you modify hello template.json file as described, republish hello Resource Manager template.</span></span> <span data-ttu-id="7d7de-185">Jeśli został wyeksportowany szablon hello, uruchamianie pliku deploy.ps1 hello je opublikuje hello szablonu.</span><span class="sxs-lookup"><span data-stu-id="7d7de-185">If hello template was exported, running hello deploy.ps1 file republishes hello template.</span></span> <span data-ttu-id="7d7de-186">Po wdrożeniu, upewnij się, że **ProvisioningState** jest **zakończyło się pomyślnie**.</span><span class="sxs-lookup"><span data-stu-id="7d7de-186">After you deploy, ensure that **ProvisioningState** is **Succeeded**.</span></span>

## <a name="update-diagnostics-toocollect-health-and-load-events"></a><span data-ttu-id="7d7de-187">Aktualizowanie zdarzenia kondycji i obciążenia toocollect diagnostyki</span><span class="sxs-lookup"><span data-stu-id="7d7de-187">Update diagnostics toocollect health and load events</span></span>

<span data-ttu-id="7d7de-188">Począwszy od wersji platformy Service Fabric hello 5.4 metryki zdarzenia kondycji i obciążenia są dostępne dla kolekcji.</span><span class="sxs-lookup"><span data-stu-id="7d7de-188">Starting with hello 5.4 release of Service Fabric, health and load metric events are available for collection.</span></span> <span data-ttu-id="7d7de-189">Te zdarzenia odzwierciedlają zdarzeń generowanych przez hello system lub kodu za pomocą kondycji hello lub załadować API raportowania, takie jak [ReportPartitionHealth](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportpartitionhealth.aspx) lub [ReportLoad](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportload.aspx).</span><span class="sxs-lookup"><span data-stu-id="7d7de-189">These events reflect events generated by hello system or your code by using hello health or load reporting APIs such as [ReportPartitionHealth](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportpartitionhealth.aspx) or [ReportLoad](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportload.aspx).</span></span> <span data-ttu-id="7d7de-190">Dzięki temu agregowanie i wyświetlanie stanu systemu wraz z upływem czasu oraz alerty na podstawie kondycji lub obciążenia zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="7d7de-190">This allows for aggregating and viewing system health over time and for alerting based on health or load events.</span></span> <span data-ttu-id="7d7de-191">tooview dodać tych zdarzeń w Podglądzie zdarzeń diagnostycznych programu Visual Studio "Microsoft-ServiceFabric:4:0x4000000000000008" toohello listy dostawców ETW.</span><span class="sxs-lookup"><span data-stu-id="7d7de-191">tooview these events in Visual Studio's Diagnostic Event Viewer add "Microsoft-ServiceFabric:4:0x4000000000000008" toohello list of ETW providers.</span></span>

<span data-ttu-id="7d7de-192">zdarzenia hello toocollect, zmodyfikuj tooinclude szablon Menedżera zasobów hello</span><span class="sxs-lookup"><span data-stu-id="7d7de-192">toocollect hello events, modify hello resource manager template tooinclude</span></span>

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

## <a name="update-diagnostics-toocollect-and-upload-logs-from-new-eventsource-channels"></a><span data-ttu-id="7d7de-193">Zaktualizuj toocollect diagnostyki i przekazywania dzienników z nowych kanałów źródła zdarzeń</span><span class="sxs-lookup"><span data-stu-id="7d7de-193">Update Diagnostics toocollect and upload logs from new EventSource channels</span></span>
<span data-ttu-id="7d7de-194">Dzienniki toocollect diagnostyki tooupdate nowych kanałów EventSource reprezentujących nowej aplikacji, który zajmie około toodeploy, wykonaj kroki takie same jak hello hello [poprzedniej sekcji](#deploywadarm) ustawień diagnostycznych dla istniejącej klaster.</span><span class="sxs-lookup"><span data-stu-id="7d7de-194">tooupdate Diagnostics toocollect logs from new EventSource channels that represent a new application that you're about toodeploy, perform hello same steps as in hello [previous section](#deploywadarm) for setup of Diagnostics for an existing cluster.</span></span>

<span data-ttu-id="7d7de-195">Zaktualizuj hello `EtwEventSourceProviderConfiguration` sekcji hello template.json wpisy tooadd hello nowych kanałów EventSource przed zastosowaniem konfiguracji hello aktualizacji przy użyciu hello `New-AzureRmResourceGroupDeployment` polecenia programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7d7de-195">Update hello `EtwEventSourceProviderConfiguration` section in hello template.json file tooadd entries for hello new EventSource channels before you apply hello configuration update by using hello `New-AzureRmResourceGroupDeployment` PowerShell command.</span></span> <span data-ttu-id="7d7de-196">Nazwa Hello źródła zdarzeń hello jest zdefiniowany jako części kodu w pliku generowanych przez program Visual Studio ServiceEventSource.cs hello.</span><span class="sxs-lookup"><span data-stu-id="7d7de-196">hello name of hello event source is defined as part of your code in hello Visual Studio-generated ServiceEventSource.cs file.</span></span>

<span data-ttu-id="7d7de-197">Na przykład źródło zdarzenia jest o nazwie Mój Eventsource, dodać hello następujące zdarzenia hello tooplace kodu z Moje Eventsource do tabeli o nazwie MyDestinationTableName.</span><span class="sxs-lookup"><span data-stu-id="7d7de-197">For example, if your event source is named My-Eventsource, add hello following code tooplace hello events from My-Eventsource into a table named MyDestinationTableName.</span></span>

```json
        {
            "provider": "My-Eventsource",
            "scheduledTransferPeriod": "PT5M",
            "DefaultEvents": {
            "eventDestination": "MyDestinationTableName"
            }
        }
```

<span data-ttu-id="7d7de-198">liczniki wydajności toocollect lub dzienniki zdarzeń, modyfikować szablonu usługi Resource Manager hello za pomocą hello przykłady podane w [Utwórz maszynę wirtualną systemu Windows z monitorowania i diagnostyki za pomocą szablonu usługi Azure Resource Manager](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7d7de-198">toocollect performance counters or event logs, modify hello Resource Manager template by using hello examples provided in [Create a Windows virtual machine with monitoring and diagnostics by using an Azure Resource Manager template](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="7d7de-199">Następnie należy ponownie opublikować hello szablonu usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="7d7de-199">Then, republish hello Resource Manager template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7d7de-200">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="7d7de-200">Next steps</span></span>
<span data-ttu-id="7d7de-201">toounderstand bardziej szczegółowo jakie zdarzenia należy szukać podczas rozwiązywania problemów, zobacz hello zdarzeń diagnostycznych wysyłanego do [Reliable Actors](service-fabric-reliable-actors-diagnostics.md) i [niezawodne usługi](service-fabric-reliable-services-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="7d7de-201">toounderstand in more detail what events you should look for while troubleshooting issues, see hello diagnostic events emitted for [Reliable Actors](service-fabric-reliable-actors-diagnostics.md) and [Reliable Services](service-fabric-reliable-services-diagnostics.md).</span></span>

## <a name="related-articles"></a><span data-ttu-id="7d7de-202">Pokrewne artykuły:</span><span class="sxs-lookup"><span data-stu-id="7d7de-202">Related articles</span></span>
* [<span data-ttu-id="7d7de-203">Dowiedz się, jak toocollect liczników wydajności lub dzienniki przy użyciu hello rozszerzenia diagnostyki</span><span class="sxs-lookup"><span data-stu-id="7d7de-203">Learn how toocollect performance counters or logs by using hello Diagnostics extension</span></span>](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="7d7de-204">Rozwiązania sieci szkieletowej usług analizy dzienników</span><span class="sxs-lookup"><span data-stu-id="7d7de-204">Service Fabric solution in Log Analytics</span></span>](../log-analytics/log-analytics-service-fabric.md)

