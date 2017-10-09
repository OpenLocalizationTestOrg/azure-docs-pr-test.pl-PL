---
title: "aaaAssess aplikacji sieci szkieletowej usług za pomocą analizy dzienników przy użyciu hello portalu Azure | Dokumentacja firmy Microsoft"
description: "Za pomocą rozwiązania sieci szkieletowej usług hello w analizy dzienników przy użyciu hello Azure tooassess portalu hello ryzyka i kondycji sieci szkieletowej usług aplikacji, a także micro-services, węzły i klastry."
services: log-analytics
documentationcenter: 
author: niniikhena
manager: jochan
editor: 
ms.assetid: 9c91aacb-c48e-466c-b792-261f25940c0c
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: nini
ms.openlocfilehash: 891c7f6e5ed511ac18599bdc280ab3dc09700fbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="assess-service-fabric-applications-and-micro-services-with-hello-azure-portal"></a><span data-ttu-id="b3da9-103">Oceń aplikacji usługi Service Fabric i micro-services z hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="b3da9-103">Assess Service Fabric applications and micro-services with hello Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="b3da9-104">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="b3da9-104">Resource Manager</span></span>](log-analytics-service-fabric-azure-resource-manager.md)
> * [<span data-ttu-id="b3da9-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b3da9-105">PowerShell</span></span>](log-analytics-service-fabric.md)
>
>

![Symbol sieci szkieletowej usług](./media/log-analytics-service-fabric/service-fabric-assessment-symbol.png)

<span data-ttu-id="b3da9-107">W tym artykule opisano sposób hello toouse rozwiązania sieci szkieletowej usług w toohelp analizy dzienników identyfikowanie i rozwiązywanie problemów w klastrze usługi sieć szkieletowa usług.</span><span class="sxs-lookup"><span data-stu-id="b3da9-107">This article describes how toouse hello Service Fabric solution in Log Analytics toohelp identify and troubleshoot issues across your Service Fabric cluster.</span></span>

<span data-ttu-id="b3da9-108">Hello rozwiązania usługi Service Fabric korzysta z danych diagnostyki Azure z maszyn wirtualnych, sieci szkieletowej usług zbierać dane z tabel Azure WAD.</span><span class="sxs-lookup"><span data-stu-id="b3da9-108">hello Service Fabric solution uses Azure Diagnostics data from your Service Fabric VMs, by collecting this data from your Azure WAD tables.</span></span> <span data-ttu-id="b3da9-109">Analizy dzienników następnie odczytuje zdarzenia framework sieci szkieletowej usług, w tym **niezawodnej zdarzeń usługi**, **zdarzenia aktora**, **zdarzenia operacyjne**, i **zdarzenia ETW niestandardowe**.</span><span class="sxs-lookup"><span data-stu-id="b3da9-109">Log Analytics then reads Service Fabric framework events, including **Reliable Service Events**, **Actor Events**, **Operational Events**, and **Custom ETW events**.</span></span> <span data-ttu-id="b3da9-110">Z pulpitu nawigacyjnego rozwiązania hello jesteś tooview stanie godne uwagi problemy i istotne zdarzenia w środowisku sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="b3da9-110">With hello solution dashboard, you are able tooview notable issues and relevant events in your Service Fabric environment.</span></span>

<span data-ttu-id="b3da9-111">wprowadzenie do rozwiązania hello tooget, należy tooconnect obszaru roboczego analizy dzienników tooa klastra sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="b3da9-111">tooget started with hello solution, you need tooconnect your Service Fabric cluster tooa Log Analytics workspace.</span></span> <span data-ttu-id="b3da9-112">Poniżej przedstawiono trzy tooconsider scenariusze:</span><span class="sxs-lookup"><span data-stu-id="b3da9-112">Here are three scenarios tooconsider:</span></span>

1. <span data-ttu-id="b3da9-113">Jeśli klaster sieci szkieletowej usług nie została wdrożona, wykonaj kroki hello w ***wdrażanie obszaru roboczego analizy dzienników tooa klastra sieci szkieletowej usług podłączony*** toodeploy nowego klastra i skonfigurowano tooreport tooLog Analytics.</span><span class="sxs-lookup"><span data-stu-id="b3da9-113">If you have not deployed your Service Fabric cluster, use hello steps in ***Deploy a Service Fabric Cluster connected tooa Log Analytics workspace*** toodeploy a new cluster and have it configured tooreport tooLog Analytics.</span></span>
2. <span data-ttu-id="b3da9-114">Jeśli należy toocollect liczniki wydajności z toouse Twojego hostów innych rozwiązań pakietu OMS, takich jak zabezpieczeń w klastrze usługi sieć szkieletowa, wykonaj kroki hello w ***wdrażanie obszar roboczy analizy dzienników tooa klastra sieci szkieletowej usług połączone z rozszerzenia maszyny Wirtualnej zainstalowana.***</span><span class="sxs-lookup"><span data-stu-id="b3da9-114">If you need toocollect performance counters from your hosts toouse other OMS solutions such as Security on your Service Fabric Cluster, follow hello steps in ***Deploy a Service Fabric Cluster connected tooa Log Analytics workspace with VM Extension installed.***</span></span>
3. <span data-ttu-id="b3da9-115">Jeśli została już wdrożona klastra sieci szkieletowej usług i chcesz tooconnect go tooLog Analytics, wykonaj kroki hello ***Dodawanie istniejącego konta magazynu tooLog Analytics.***</span><span class="sxs-lookup"><span data-stu-id="b3da9-115">If you have already deployed your Service Fabric cluster and want tooconnect it tooLog Analytics, follow hello steps in ***Adding an existing storage account tooLog Analytics.***</span></span>

## <a name="deploy-a-service-fabric-cluster-connected-tooa-log-analytics-workspace"></a><span data-ttu-id="b3da9-116">Wdróż obszaru roboczego analizy dzienników tooa połączenia klastra sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="b3da9-116">Deploy a Service Fabric Cluster connected tooa Log Analytics workspace.</span></span>
<span data-ttu-id="b3da9-117">Ten szablon hello następujące:</span><span class="sxs-lookup"><span data-stu-id="b3da9-117">This template does hello following:</span></span>

1. <span data-ttu-id="b3da9-118">Wdraża obszar roboczy analizy dzienników tooa klastra już połączona sieć szkieletowa usług Azure.</span><span class="sxs-lookup"><span data-stu-id="b3da9-118">Deploys an Azure Service Fabric cluster already connected tooa Log Analytics workspace.</span></span> <span data-ttu-id="b3da9-119">Masz toocreate opcji hello nowy obszar roboczy podczas wdrażania szablonu hello lub nazwę wejściowej hello już istniejący obszar roboczy analizy dzienników.</span><span class="sxs-lookup"><span data-stu-id="b3da9-119">You have hello option toocreate a new workspace while deploying hello template, or input hello name of an already existing Log Analytics workspace.</span></span>
2. <span data-ttu-id="b3da9-120">Dodaje obszaru roboczego analizy dzienników toohello konto magazynu diagnostyki hello.</span><span class="sxs-lookup"><span data-stu-id="b3da9-120">Adds hello diagnostic storage account toohello Log Analytics workspace.</span></span>
3. <span data-ttu-id="b3da9-121">Umożliwia rozwiązanie sieci szkieletowej usług hello w obszarze roboczym analizy dzienników.</span><span class="sxs-lookup"><span data-stu-id="b3da9-121">Enables hello Service Fabric solution in your Log Analytics workspace.</span></span>

<span data-ttu-id="b3da9-122">[![Wdrażanie tooAzure](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fazure%2Fazure-quickstart-templates%2Fmaster%2Fservice-fabric-oms%2F%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="b3da9-122">[![Deploy tooAzure](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fazure%2Fazure-quickstart-templates%2Fmaster%2Fservice-fabric-oms%2F%2Fazuredeploy.json)</span></span>

<span data-ttu-id="b3da9-123">Po wybraniu hello wdrażanie przycisk powyżej, hello Azure otwarciu portalu wraz z parametrami, należy tooedit.</span><span class="sxs-lookup"><span data-stu-id="b3da9-123">Once you select hello deploy button above, hello Azure portal opens with parameters for you tooedit.</span></span> <span data-ttu-id="b3da9-124">Być toocreate się nową grupę zasobów możesz wpisać nazwę nowego obszaru roboczego analizy dzienników:</span><span class="sxs-lookup"><span data-stu-id="b3da9-124">Be sure toocreate a new resource group if you input a new Log Analytics workspace name:</span></span>

![Service Fabric](./media/log-analytics-service-fabric/2.png)

![Service Fabric](./media/log-analytics-service-fabric/3.png)

<span data-ttu-id="b3da9-127">Zaakceptuj postanowienia prawne hello i kliknij przycisk **Utwórz** toostart hello wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="b3da9-127">Accept hello legal terms and click **Create** toostart hello deployment.</span></span> <span data-ttu-id="b3da9-128">Po zakończeniu wdrażania hello powinni widzieć nowy obszar roboczy hello i utworzyć klaster i hello WADServiceFabric * zdarzeń, WADWindowsEventLogs i WADETWEvent tabele dodać:</span><span class="sxs-lookup"><span data-stu-id="b3da9-128">Once hello deployment is completed, you should see hello new workspace and cluster created, and hello WADServiceFabric*Event, WADWindowsEventLogs and WADETWEvent tables added:</span></span>

![Service Fabric](./media/log-analytics-service-fabric/4.png)

## <a name="deploy-a-service-fabric-cluster-connected-tooa-log-analytics-workspace-with-vm-extension-installed"></a><span data-ttu-id="b3da9-130">Zainstalowane rozszerzenie maszyny Wirtualnej, należy wdrożyć obszaru roboczego analizy dzienników tooa połączenia klastra sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="b3da9-130">Deploy a Service Fabric Cluster connected tooa Log Analytics workspace with VM Extension installed.</span></span>

<span data-ttu-id="b3da9-131">Ten szablon hello następujące:</span><span class="sxs-lookup"><span data-stu-id="b3da9-131">This template does hello following:</span></span>

1. <span data-ttu-id="b3da9-132">Wdraża obszar roboczy analizy dzienników tooa klastra już połączona sieć szkieletowa usług Azure.</span><span class="sxs-lookup"><span data-stu-id="b3da9-132">Deploys an Azure Service Fabric cluster already connected tooa Log Analytics workspace.</span></span> <span data-ttu-id="b3da9-133">Można utworzyć nowego obszaru roboczego lub użyć istniejącego.</span><span class="sxs-lookup"><span data-stu-id="b3da9-133">You can create a new workspace or use an existing one.</span></span>
2. <span data-ttu-id="b3da9-134">Dodaje obszaru roboczego analizy dzienników toohello hello diagnostycznych magazynu kont.</span><span class="sxs-lookup"><span data-stu-id="b3da9-134">Adds hello diagnostic storage accounts toohello Log Analytics workspace.</span></span>
3. <span data-ttu-id="b3da9-135">Umożliwia rozwiązanie sieci szkieletowej usług hello w obszarze roboczym analizy dzienników hello.</span><span class="sxs-lookup"><span data-stu-id="b3da9-135">Enables hello Service Fabric solution in hello Log Analytics workspace.</span></span>
4. <span data-ttu-id="b3da9-136">Instaluje rozszerzenia agent MMA hello w każdym skalowania maszyny wirtualnej w klastrze usługi sieć szkieletowa usług.</span><span class="sxs-lookup"><span data-stu-id="b3da9-136">Installs hello MMA agent extension in each virtual machine scale set in your Service Fabric cluster.</span></span> <span data-ttu-id="b3da9-137">Z zainstalowanym agentem MMA hello metryki wydajności mogą tooview nastąpi węzły.</span><span class="sxs-lookup"><span data-stu-id="b3da9-137">With hello MMA agent installed, you are able tooview performance metrics about your nodes.</span></span>

<span data-ttu-id="b3da9-138">[![Wdrażanie tooAzure](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fazure%2Fazure-quickstart-templates%2Fmaster%2Fservice-fabric-vmss-oms%2F%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="b3da9-138">[![Deploy tooAzure](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fazure%2Fazure-quickstart-templates%2Fmaster%2Fservice-fabric-vmss-oms%2F%2Fazuredeploy.json)</span></span>

<span data-ttu-id="b3da9-139">Poniżej hello tego samego powyższe kroki, niezbędne parametry wejściowe hello i rozpocząć poza wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="b3da9-139">Following hello same steps above, input hello necessary parameters, and kick off a deployment.</span></span> <span data-ttu-id="b3da9-140">Ponownie powinien zostać wyświetlony nowy obszar roboczy hello, klastra i tabele WAD wszystkie utworzone:</span><span class="sxs-lookup"><span data-stu-id="b3da9-140">Once again you should see hello new workspace, cluster and WAD tables all created:</span></span>

![Service Fabric](./media/log-analytics-service-fabric/5.png)

### <a name="viewing-performance-data"></a><span data-ttu-id="b3da9-142">Wyświetlanie danych wydajności</span><span class="sxs-lookup"><span data-stu-id="b3da9-142">Viewing Performance Data</span></span>

<span data-ttu-id="b3da9-143">tooview danych o wydajności z węzłów:</span><span class="sxs-lookup"><span data-stu-id="b3da9-143">tooview Perf Data from your nodes:</span></span>


[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

- <span data-ttu-id="b3da9-144">Uruchom program hello obszaru roboczego analizy dzienników z hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="b3da9-144">Launch hello Log Analytics workspace from hello Azure portal.</span></span>
  <span data-ttu-id="b3da9-145">![Service Fabric](./media/log-analytics-service-fabric/6.png)</span><span class="sxs-lookup"><span data-stu-id="b3da9-145">![Service Fabric](./media/log-analytics-service-fabric/6.png)</span></span>
- <span data-ttu-id="b3da9-146">Przejdź tooSettings w okienku po lewej stronie powitania i wybierz dane >> liczników wydajności systemu Windows >> "hello Dodaj wybrane liczniki wydajności": ![sieci szkieletowej usług](./media/log-analytics-service-fabric/7.png)</span><span class="sxs-lookup"><span data-stu-id="b3da9-146">Go tooSettings on hello left pane, and select Data >> Windows Performance Counters >> "Add hello selected performance counters": ![Service Fabric](./media/log-analytics-service-fabric/7.png)</span></span>
- <span data-ttu-id="b3da9-147">W wyszukiwaniu dziennika należy użyć powitania po toodelve zapytania do kluczowych metryk dotyczących węzły:</span><span class="sxs-lookup"><span data-stu-id="b3da9-147">In Log Search, use hello following queries toodelve into key metrics about your nodes:</span></span>

    <span data-ttu-id="b3da9-148">a.</span><span class="sxs-lookup"><span data-stu-id="b3da9-148">a.</span></span> <span data-ttu-id="b3da9-149">Porównaj hello średnie wykorzystanie procesora CPU przez wszystkie węzły w hello węzły, które występują problemy dotyczące ostatniego toosee godzinę i w odstępach czasu, jaki węzeł ma kolekcji:</span><span class="sxs-lookup"><span data-stu-id="b3da9-149">Compare hello average CPU Utilization across all your nodes in hello last one hour toosee which nodes are having issues and at what time interval a node had a spike:</span></span>

    ```
    Type=Perf ObjectName=Processor CounterName="% Processor Time"|measure avg(CounterValue) by Computer Interval 1HOUR.
    ```

    ![Service Fabric](./media/log-analytics-service-fabric/10.png)

    <span data-ttu-id="b3da9-151">b.</span><span class="sxs-lookup"><span data-stu-id="b3da9-151">b.</span></span> <span data-ttu-id="b3da9-152">Widok podobne wykresy liniowe dla ilość pamięci dostępna na każdym węźle z tej kwerendy:</span><span class="sxs-lookup"><span data-stu-id="b3da9-152">View similar line charts for available memory on each node with this query:</span></span>

    ```
    Type=Perf ObjectName=Memory CounterName="Available MBytes Memory" | measure avg(CounterValue) by Computer Interval 1HOUR.
    ```

    <span data-ttu-id="b3da9-153">tooview lista wszystkich węzłów, przedstawiający hello dokładną wartość średnia dla dostępna pamięć (MB) dla każdego węzła, skorzystaj z tej kwerendy:</span><span class="sxs-lookup"><span data-stu-id="b3da9-153">tooview a listing of all your nodes, showing hello exact average value for Available MBytes for each node, use this query:</span></span>

    ```
    Type=Perf (ObjectName=Memory) (CounterName="Available MBytes") | measure avg(CounterValue) by Computer
    ```

    ![Service Fabric](./media/log-analytics-service-fabric/11.png)

    <span data-ttu-id="b3da9-155">c.</span><span class="sxs-lookup"><span data-stu-id="b3da9-155">c.</span></span> <span data-ttu-id="b3da9-156">W przypadku hello mają toodrill w dół w określonym węźle, sprawdzając średniej godzinowej hello minimalne, maksymalne i percentyl 75 użycia procesora CPU, możesz teraz możliwe toodo to przez przy użyciu tej kwerendy (Zastąp pole komputera):</span><span class="sxs-lookup"><span data-stu-id="b3da9-156">In hello case that you want toodrill down into a specific node by examining hello hourly average, minimum, maximum and 75-percentile CPU usage, you're able toodo this by using this query (replace Computer field):</span></span>

    ```
    Type=Perf CounterName="% Processor Time" InstanceName=_Total Computer="BaconDC01.BaconLand.com"| measure min(CounterValue), avg(CounterValue), percentile75(CounterValue), max(CounterValue) by Computer Interval 1HOUR
    ```

    ![Service Fabric](./media/log-analytics-service-fabric/12.png)

<span data-ttu-id="b3da9-158">Przeczytaj więcej informacji na temat metryk wydajności w analizy dzienników hello [blogu Operations Management Suite](https://blogs.technet.microsoft.com/msoms/tag/metrics/).</span><span class="sxs-lookup"><span data-stu-id="b3da9-158">Read more information about performance metrics in Log Analytics at hello [Operations Management Suite blog](https://blogs.technet.microsoft.com/msoms/tag/metrics/).</span></span>


## <a name="adding-an-existing-storage-account-toolog-analytics"></a><span data-ttu-id="b3da9-159">Dodawanie istniejącego konta magazynu tooLog analityka</span><span class="sxs-lookup"><span data-stu-id="b3da9-159">Adding an existing storage account tooLog Analytics</span></span>

<span data-ttu-id="b3da9-160">Ten szablon jest po prostu dodaje z istniejącego magazynu kont tooa nowy lub istniejący obszar roboczy analizy dzienników.</span><span class="sxs-lookup"><span data-stu-id="b3da9-160">This template simply adds your existing storage accounts tooa new or existing Log Analytics workspace.</span></span>

<span data-ttu-id="b3da9-161">[![Wdrażanie tooAzure](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Foms-existing-storage-account%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="b3da9-161">[![Deploy tooAzure](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Foms-existing-storage-account%2Fazuredeploy.json)</span></span>

> [!NOTE]
> <span data-ttu-id="b3da9-162">Wybór grupy zasobów, jeśli pracujesz już istniejący obszar roboczy analizy dzienników wybierz "Użyj istniejącego" i wyszukaj hello grupę zasobów, zawierającą hello obszaru roboczego analizy dzienników.</span><span class="sxs-lookup"><span data-stu-id="b3da9-162">In selecting a Resource Group, if you're working with an already existing Log Analytics workspace, select "Use Existing" and search for hello resource group containing hello Log Analytics workspace.</span></span> <span data-ttu-id="b3da9-163">Utwórz nowy Jeśli jeden inaczej.</span><span class="sxs-lookup"><span data-stu-id="b3da9-163">Create a new one if otherwise.</span></span>
> <span data-ttu-id="b3da9-164">![Service Fabric](./media/log-analytics-service-fabric/8.png)</span><span class="sxs-lookup"><span data-stu-id="b3da9-164">![Service Fabric](./media/log-analytics-service-fabric/8.png)</span></span>
>
>

<span data-ttu-id="b3da9-165">Po wdrożeniu tego szablonu można obszaru roboczego może toosee hello magazynu konto podłączone tooyour analizy dzienników.</span><span class="sxs-lookup"><span data-stu-id="b3da9-165">After this template has been deployed, you will be able toosee hello storage account connected tooyour Log Analytics workspace.</span></span> <span data-ttu-id="b3da9-166">W tym wystąpieniu po dodaniu jednego więcej pamięci masowej konta toohello Exchange obszaru roboczego utworzone powyżej.</span><span class="sxs-lookup"><span data-stu-id="b3da9-166">In this instance, I added one more storage account toohello Exchange workspace I created above.</span></span>
<span data-ttu-id="b3da9-167">![Service Fabric](./media/log-analytics-service-fabric/9.png)</span><span class="sxs-lookup"><span data-stu-id="b3da9-167">![Service Fabric](./media/log-analytics-service-fabric/9.png)</span></span>

## <a name="view-service-fabric-events"></a><span data-ttu-id="b3da9-168">Wyświetl zdarzenia dotyczące sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="b3da9-168">View Service Fabric events</span></span>

<span data-ttu-id="b3da9-169">Po zakończeniu wdrożenia hello i hello rozwiązania sieci szkieletowej usług została włączona w obszarze roboczym, wybierz hello **sieci szkieletowej usług** kafelka na pulpicie nawigacyjnym hello analizy dzienników portalu toolaunch hello sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="b3da9-169">Once hello deployments are completed and hello Service Fabric solution has been enabled in your workspace, select hello **Service Fabric** tile in hello Log Analytics portal toolaunch hello Service Fabric dashboard.</span></span> <span data-ttu-id="b3da9-170">pulpit nawigacyjny Hello zawiera kolumny hello w hello w poniższej tabeli.</span><span class="sxs-lookup"><span data-stu-id="b3da9-170">hello dashboard includes hello columns in hello following table.</span></span> <span data-ttu-id="b3da9-171">Każda kolumna wymieniono top zdarzenia 10 hello przez liczbę dopasowanie, że kryteria kolumny hello określony przedział czasu.</span><span class="sxs-lookup"><span data-stu-id="b3da9-171">Each column lists hello top 10 events by count matching that column's criteria for hello specified time range.</span></span> <span data-ttu-id="b3da9-172">Możesz uruchomić wyszukiwanie dziennika, które zawiera listę całego hello klikając **zobaczyć wszystkie** u dołu prawo hello każdej kolumny lub przez kliknięcie nagłówka kolumny hello.</span><span class="sxs-lookup"><span data-stu-id="b3da9-172">You can run a log search that provides hello entire list by clicking **See all** at hello right bottom of each column, or by clicking hello column header.</span></span>

| <span data-ttu-id="b3da9-173">**Zdarzenie sieci szkieletowej usług**</span><span class="sxs-lookup"><span data-stu-id="b3da9-173">**Service Fabric event**</span></span> | <span data-ttu-id="b3da9-174">**Opis elementu**</span><span class="sxs-lookup"><span data-stu-id="b3da9-174">**description**</span></span> |
| --- | --- |
| <span data-ttu-id="b3da9-175">Problemy godne uwagi</span><span class="sxs-lookup"><span data-stu-id="b3da9-175">Notable Issues</span></span> |<span data-ttu-id="b3da9-176">Wyświetlanie problemy, takie jak RunAsyncFailures RunAsynCancellations i rozwijane węzła.</span><span class="sxs-lookup"><span data-stu-id="b3da9-176">A Display of issues such as RunAsyncFailures RunAsynCancellations and Node Downs.</span></span> |
| <span data-ttu-id="b3da9-177">Zdarzenia operacyjne</span><span class="sxs-lookup"><span data-stu-id="b3da9-177">Operational Events</span></span> |<span data-ttu-id="b3da9-178">Godne zdarzenia operacyjne takich jak uaktualniania aplikacji i wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="b3da9-178">Notable operational events such as application upgrade and deployments.</span></span> |
| <span data-ttu-id="b3da9-179">Zdarzenia niezawodne usługi</span><span class="sxs-lookup"><span data-stu-id="b3da9-179">Reliable Service Events</span></span> |<span data-ttu-id="b3da9-180">Zdarzenia zauważalne niezawodnej usługi takie Runasyncinvocations.</span><span class="sxs-lookup"><span data-stu-id="b3da9-180">Notable reliable service events such a Runasyncinvocations.</span></span> |
| <span data-ttu-id="b3da9-181">Zdarzenia aktora</span><span class="sxs-lookup"><span data-stu-id="b3da9-181">Actor Events</span></span> |<span data-ttu-id="b3da9-182">Godne aktora zdarzenia generowane przez micro usług, takich jak wyjątki wyrzucane przez metodę aktora, aktora aktywacji i deactivations i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="b3da9-182">Notable actor events generated by your micro-services, such as exceptions thrown by an actor method, actor activations and deactivations, and so on.</span></span> |
| <span data-ttu-id="b3da9-183">Zdarzenia aplikacji</span><span class="sxs-lookup"><span data-stu-id="b3da9-183">Application Events</span></span> |<span data-ttu-id="b3da9-184">Wszystkie niestandardowe ETW zdarzenia generowane przez aplikacje.</span><span class="sxs-lookup"><span data-stu-id="b3da9-184">All custom ETW events generated by your applications.</span></span> |

![Pulpit nawigacyjny sieci szkieletowej usług](./media/log-analytics-service-fabric/sf3.png)

![Pulpit nawigacyjny sieci szkieletowej usług](./media/log-analytics-service-fabric/sf4.png)

<span data-ttu-id="b3da9-187">Witaj poniższej tabeli przedstawiono metody zbierania danych i inne szczegółowe informacje o jak dane są zbierane dla sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="b3da9-187">hello following table shows data collection methods and other details about how data is collected for Service Fabric.</span></span>

| <span data-ttu-id="b3da9-188">Platformy</span><span class="sxs-lookup"><span data-stu-id="b3da9-188">platform</span></span> | <span data-ttu-id="b3da9-189">Bezpośrednie agenta</span><span class="sxs-lookup"><span data-stu-id="b3da9-189">Direct Agent</span></span> | <span data-ttu-id="b3da9-190">Agent programu Operations Manager</span><span class="sxs-lookup"><span data-stu-id="b3da9-190">Operations Manager agent</span></span> | <span data-ttu-id="b3da9-191">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="b3da9-191">Azure Storage</span></span> | <span data-ttu-id="b3da9-192">Wymagane programu Operations Manager?</span><span class="sxs-lookup"><span data-stu-id="b3da9-192">Operations Manager required?</span></span> | <span data-ttu-id="b3da9-193">Danych agenta programu Operations Manager są wysyłane za pośrednictwem grupy zarządzania</span><span class="sxs-lookup"><span data-stu-id="b3da9-193">Operations Manager agent data sent via management group</span></span> | <span data-ttu-id="b3da9-194">Częstotliwość kolekcji</span><span class="sxs-lookup"><span data-stu-id="b3da9-194">collection frequency</span></span> |
| --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="b3da9-195">Windows</span><span class="sxs-lookup"><span data-stu-id="b3da9-195">Windows</span></span> |  |  | <span data-ttu-id="b3da9-196">&#8226;</span><span class="sxs-lookup"><span data-stu-id="b3da9-196">&#8226;</span></span> |  |  |<span data-ttu-id="b3da9-197">10 minut</span><span class="sxs-lookup"><span data-stu-id="b3da9-197">10 minutes</span></span> |

> [!NOTE]
> <span data-ttu-id="b3da9-198">Zakres hello tych zdarzeń w hello rozwiązania sieci szkieletowej usług można zmienić, klikając **dane oparte na ostatnich 7 dni** u góry hello hello pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="b3da9-198">You can change hello scope of these events in hello Service Fabric solution by clicking **Data based on last 7 days** at hello top of hello dashboard.</span></span> <span data-ttu-id="b3da9-199">Można również wyświetlać zdarzenia generowane w hello ostatnich siedmiu dni, w ciągu jednego dnia lub sześciu godzin.</span><span class="sxs-lookup"><span data-stu-id="b3da9-199">You can also show events generated within hello last seven days, one day, or six hours.</span></span> <span data-ttu-id="b3da9-200">Umożliwia wybranie **niestandardowych** toospecify niestandardowy zakres dat.</span><span class="sxs-lookup"><span data-stu-id="b3da9-200">Or, you can select **Custom** toospecify a custom date range.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="b3da9-201">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b3da9-201">Next steps</span></span>

* <span data-ttu-id="b3da9-202">Użyj [wyszukiwania dziennika analizy dzienników](log-analytics-log-searches.md) tooview szczegółowe dane zdarzeń usługi sieć szkieletowa usług.</span><span class="sxs-lookup"><span data-stu-id="b3da9-202">Use [Log Searches in Log Analytics](log-analytics-log-searches.md) tooview detailed Service Fabric event data.</span></span>
