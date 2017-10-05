---
title: "Ocena aplikacji usługi Service Fabric z analizy dzienników przy użyciu portalu Azure | Dokumentacja firmy Microsoft"
description: "Rozwiązanie usługi sieć szkieletowa można użyć w analizy dzienników przy użyciu portalu Azure w celu oceny ryzyka i kondycji aplikacji usługi Service Fabric, micro-services, węzły i klastry."
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
ms.openlocfilehash: 8c564c0dcbb2f9be286917b2f4d8a40da5406fae
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="assess-service-fabric-applications-and-micro-services-with-the-azure-portal"></a><span data-ttu-id="43074-103">Oceń aplikacji usługi Service Fabric i micro-services przy użyciu portalu Azure</span><span class="sxs-lookup"><span data-stu-id="43074-103">Assess Service Fabric applications and micro-services with the Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="43074-104">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="43074-104">Resource Manager</span></span>](log-analytics-service-fabric-azure-resource-manager.md)
> * [<span data-ttu-id="43074-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="43074-105">PowerShell</span></span>](log-analytics-service-fabric.md)
>
>

![Symbol sieci szkieletowej usług](./media/log-analytics-service-fabric/service-fabric-assessment-symbol.png)

<span data-ttu-id="43074-107">W tym artykule opisano sposób użycia rozwiązania sieci szkieletowej usług w analizy dzienników do identyfikacji i rozwiązywania problemów w klastrze usługi sieć szkieletowa usług.</span><span class="sxs-lookup"><span data-stu-id="43074-107">This article describes how to use the Service Fabric solution in Log Analytics to help identify and troubleshoot issues across your Service Fabric cluster.</span></span>

<span data-ttu-id="43074-108">Rozwiązanie usługi Service Fabric korzysta z danych diagnostyki Azure z maszyn wirtualnych, sieci szkieletowej usług zbierać dane z tabel Azure WAD.</span><span class="sxs-lookup"><span data-stu-id="43074-108">The Service Fabric solution uses Azure Diagnostics data from your Service Fabric VMs, by collecting this data from your Azure WAD tables.</span></span> <span data-ttu-id="43074-109">Analizy dzienników następnie odczytuje zdarzenia framework sieci szkieletowej usług, w tym **niezawodnej zdarzeń usługi**, **zdarzenia aktora**, **zdarzenia operacyjne**, i **zdarzenia ETW niestandardowe**.</span><span class="sxs-lookup"><span data-stu-id="43074-109">Log Analytics then reads Service Fabric framework events, including **Reliable Service Events**, **Actor Events**, **Operational Events**, and **Custom ETW events**.</span></span> <span data-ttu-id="43074-110">Z pulpitu nawigacyjnego rozwiązania będą mogli wyświetlić godne uwagi problemy i istotne zdarzenia w środowisku sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="43074-110">With the solution dashboard, you are able to view notable issues and relevant events in your Service Fabric environment.</span></span>

<span data-ttu-id="43074-111">Aby rozpocząć pracę z rozwiązaniem, należy połączyć z klastra usługi sieć szkieletowa usług do obszaru roboczego analizy dzienników.</span><span class="sxs-lookup"><span data-stu-id="43074-111">To get started with the solution, you need to connect your Service Fabric cluster to a Log Analytics workspace.</span></span> <span data-ttu-id="43074-112">Poniżej przedstawiono trzy scenariusze, które należy uwzględnić:</span><span class="sxs-lookup"><span data-stu-id="43074-112">Here are three scenarios to consider:</span></span>

1. <span data-ttu-id="43074-113">Jeśli klaster sieci szkieletowej usług nie została wdrożona, wykonaj kroki w ***wdrażanie klastra sieci szkieletowej usług podłączony do obszaru roboczego analizy dzienników*** do wdrożenia nowego klastra i została ona skonfigurowana do raportu analizy dzienników.</span><span class="sxs-lookup"><span data-stu-id="43074-113">If you have not deployed your Service Fabric cluster, use the steps in ***Deploy a Service Fabric Cluster connected to a Log Analytics workspace*** to deploy a new cluster and have it configured to report to Log Analytics.</span></span>
2. <span data-ttu-id="43074-114">Jeśli potrzebujesz można zebrać liczników wydajności z hostów użycie innych rozwiązań pakietu OMS, takich jak zabezpieczeń klastra sieci szkieletowej usług, postępuj zgodnie z instrukcjami ***wdrażanie klastra sieci szkieletowej usług podłączony do obszaru roboczego analizy dzienników zainstalowane rozszerzenie maszyny Wirtualnej.***</span><span class="sxs-lookup"><span data-stu-id="43074-114">If you need to collect performance counters from your hosts to use other OMS solutions such as Security on your Service Fabric Cluster, follow the steps in ***Deploy a Service Fabric Cluster connected to a Log Analytics workspace with VM Extension installed.***</span></span>
3. <span data-ttu-id="43074-115">Jeśli zostały już wdrożone z klastra sieci szkieletowej usług i chcesz nawiązać analizy dzienników, postępuj zgodnie z instrukcjami ***Dodawanie istniejącego konta magazynu do analizy dzienników.***</span><span class="sxs-lookup"><span data-stu-id="43074-115">If you have already deployed your Service Fabric cluster and want to connect it to Log Analytics, follow the steps in ***Adding an existing storage account to Log Analytics.***</span></span>

## <a name="deploy-a-service-fabric-cluster-connected-to-a-log-analytics-workspace"></a><span data-ttu-id="43074-116">Wdrażanie klastra sieci szkieletowej usług podłączony do obszaru roboczego analizy dzienników.</span><span class="sxs-lookup"><span data-stu-id="43074-116">Deploy a Service Fabric Cluster connected to a Log Analytics workspace.</span></span>
<span data-ttu-id="43074-117">Ten szablon wykonuje następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="43074-117">This template does the following:</span></span>

1. <span data-ttu-id="43074-118">Wdraża klastra usługi sieć szkieletowa usług Azure już połączona z obszaru roboczego analizy dzienników.</span><span class="sxs-lookup"><span data-stu-id="43074-118">Deploys an Azure Service Fabric cluster already connected to a Log Analytics workspace.</span></span> <span data-ttu-id="43074-119">Istnieje możliwość utworzenia nowego obszaru roboczego podczas wdrażania szablonu lub wpisać nazwę już istniejący obszar roboczy analizy dzienników.</span><span class="sxs-lookup"><span data-stu-id="43074-119">You have the option to create a new workspace while deploying the template, or input the name of an already existing Log Analytics workspace.</span></span>
2. <span data-ttu-id="43074-120">Dodaje konto magazynu diagnostyki do obszaru roboczego analizy dzienników.</span><span class="sxs-lookup"><span data-stu-id="43074-120">Adds the diagnostic storage account to the Log Analytics workspace.</span></span>
3. <span data-ttu-id="43074-121">Umożliwia rozwiązanie sieci szkieletowej usług w obszarze roboczym analizy dzienników.</span><span class="sxs-lookup"><span data-stu-id="43074-121">Enables the Service Fabric solution in your Log Analytics workspace.</span></span>

<span data-ttu-id="43074-122">[![Wdrażanie na platformie Azure](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fazure%2Fazure-quickstart-templates%2Fmaster%2Fservice-fabric-oms%2F%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="43074-122">[![Deploy to Azure](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fazure%2Fazure-quickstart-templates%2Fmaster%2Fservice-fabric-oms%2F%2Fazuredeploy.json)</span></span>

<span data-ttu-id="43074-123">Po wybraniu przycisku Wdróż powyżej portalu Azure zostanie otwarty z parametrami do edycji.</span><span class="sxs-lookup"><span data-stu-id="43074-123">Once you select the deploy button above, the Azure portal opens with parameters for you to edit.</span></span> <span data-ttu-id="43074-124">Pamiętaj utworzyć nową grupę zasobów, jeśli możesz wpisać nazwę nowego obszaru roboczego analizy dzienników:</span><span class="sxs-lookup"><span data-stu-id="43074-124">Be sure to create a new resource group if you input a new Log Analytics workspace name:</span></span>

![Service Fabric](./media/log-analytics-service-fabric/2.png)

![Service Fabric](./media/log-analytics-service-fabric/3.png)

<span data-ttu-id="43074-127">Zaakceptuj postanowienia prawne, a następnie kliknij przycisk **Utwórz** do wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="43074-127">Accept the legal terms and click **Create** to start the deployment.</span></span> <span data-ttu-id="43074-128">Po zakończeniu wdrożenia powinien zostać wyświetlony nowy obszar roboczy i klastra utworzone i WADServiceFabric * zdarzeń, WADWindowsEventLogs i WADETWEvent tabele dodać:</span><span class="sxs-lookup"><span data-stu-id="43074-128">Once the deployment is completed, you should see the new workspace and cluster created, and the WADServiceFabric*Event, WADWindowsEventLogs and WADETWEvent tables added:</span></span>

![Service Fabric](./media/log-analytics-service-fabric/4.png)

## <a name="deploy-a-service-fabric-cluster-connected-to-a-log-analytics-workspace-with-vm-extension-installed"></a><span data-ttu-id="43074-130">Wdrażanie klastra sieci szkieletowej usług podłączony do obszaru roboczego analizy dzienników zainstalowane rozszerzenie maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="43074-130">Deploy a Service Fabric Cluster connected to a Log Analytics workspace with VM Extension installed.</span></span>

<span data-ttu-id="43074-131">Ten szablon wykonuje następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="43074-131">This template does the following:</span></span>

1. <span data-ttu-id="43074-132">Wdraża klastra usługi sieć szkieletowa usług Azure już połączona z obszaru roboczego analizy dzienników.</span><span class="sxs-lookup"><span data-stu-id="43074-132">Deploys an Azure Service Fabric cluster already connected to a Log Analytics workspace.</span></span> <span data-ttu-id="43074-133">Można utworzyć nowego obszaru roboczego lub użyć istniejącego.</span><span class="sxs-lookup"><span data-stu-id="43074-133">You can create a new workspace or use an existing one.</span></span>
2. <span data-ttu-id="43074-134">Dodaje do obszaru roboczego analizy dzienników konta magazynu diagnostyki.</span><span class="sxs-lookup"><span data-stu-id="43074-134">Adds the diagnostic storage accounts to the Log Analytics workspace.</span></span>
3. <span data-ttu-id="43074-135">Umożliwia rozwiązanie sieci szkieletowej usług w obszarze roboczym analizy dzienników.</span><span class="sxs-lookup"><span data-stu-id="43074-135">Enables the Service Fabric solution in the Log Analytics workspace.</span></span>
4. <span data-ttu-id="43074-136">Instaluje rozszerzenia agent MMA w każdym skalowania maszyny wirtualnej w klastrze usługi sieć szkieletowa usług.</span><span class="sxs-lookup"><span data-stu-id="43074-136">Installs the MMA agent extension in each virtual machine scale set in your Service Fabric cluster.</span></span> <span data-ttu-id="43074-137">Z zainstalowanym agentem MMA będą mogli wyświetlić metryki wydajności o węzły.</span><span class="sxs-lookup"><span data-stu-id="43074-137">With the MMA agent installed, you are able to view performance metrics about your nodes.</span></span>

<span data-ttu-id="43074-138">[![Wdrażanie na platformie Azure](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fazure%2Fazure-quickstart-templates%2Fmaster%2Fservice-fabric-vmss-oms%2F%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="43074-138">[![Deploy to Azure](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fazure%2Fazure-quickstart-templates%2Fmaster%2Fservice-fabric-vmss-oms%2F%2Fazuredeploy.json)</span></span>

<span data-ttu-id="43074-139">Po tej samej powyższe kroki niezbędne parametry wejściowe i rozpocząć poza wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="43074-139">Following the same steps above, input the necessary parameters, and kick off a deployment.</span></span> <span data-ttu-id="43074-140">Ponownie powinien zostać wyświetlony nowy obszar roboczy, klastra i tabele WAD wszystkie utworzone:</span><span class="sxs-lookup"><span data-stu-id="43074-140">Once again you should see the new workspace, cluster and WAD tables all created:</span></span>

![Service Fabric](./media/log-analytics-service-fabric/5.png)

### <a name="viewing-performance-data"></a><span data-ttu-id="43074-142">Wyświetlanie danych wydajności</span><span class="sxs-lookup"><span data-stu-id="43074-142">Viewing Performance Data</span></span>

<span data-ttu-id="43074-143">Aby wyświetlić dane wydajności z węzłów:</span><span class="sxs-lookup"><span data-stu-id="43074-143">To view Perf Data from your nodes:</span></span>


[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

- <span data-ttu-id="43074-144">Uruchom obszaru roboczego analizy dzienników z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="43074-144">Launch the Log Analytics workspace from the Azure portal.</span></span>
  <span data-ttu-id="43074-145">![Service Fabric](./media/log-analytics-service-fabric/6.png)</span><span class="sxs-lookup"><span data-stu-id="43074-145">![Service Fabric](./media/log-analytics-service-fabric/6.png)</span></span>
- <span data-ttu-id="43074-146">Przejdź do strony ustawień w okienku po lewej stronie, a następnie wybierz dane >> liczników wydajności systemu Windows >> "Dodaj wybrane liczniki wydajności": ![sieci szkieletowej usług](./media/log-analytics-service-fabric/7.png)</span><span class="sxs-lookup"><span data-stu-id="43074-146">Go to Settings on the left pane, and select Data >> Windows Performance Counters >> "Add the selected performance counters": ![Service Fabric](./media/log-analytics-service-fabric/7.png)</span></span>
- <span data-ttu-id="43074-147">W wyszukiwaniu dziennika należy użyć następujących zapytań do delve do kluczowych metryk dotyczących węzły:</span><span class="sxs-lookup"><span data-stu-id="43074-147">In Log Search, use the following queries to delve into key metrics about your nodes:</span></span>

    <span data-ttu-id="43074-148">a.</span><span class="sxs-lookup"><span data-stu-id="43074-148">a.</span></span> <span data-ttu-id="43074-149">Porównanie średnie wykorzystanie procesora CPU przez wszystkie węzły w ciągu ostatniej godziny jeden węzły, które mają problemy, a w odstępach czasu, jaki węzeł ma kolekcji:</span><span class="sxs-lookup"><span data-stu-id="43074-149">Compare the average CPU Utilization across all your nodes in the last one hour to see which nodes are having issues and at what time interval a node had a spike:</span></span>

    ```
    Type=Perf ObjectName=Processor CounterName="% Processor Time"|measure avg(CounterValue) by Computer Interval 1HOUR.
    ```

    ![Service Fabric](./media/log-analytics-service-fabric/10.png)

    <span data-ttu-id="43074-151">b.</span><span class="sxs-lookup"><span data-stu-id="43074-151">b.</span></span> <span data-ttu-id="43074-152">Widok podobne wykresy liniowe dla ilość pamięci dostępna na każdym węźle z tej kwerendy:</span><span class="sxs-lookup"><span data-stu-id="43074-152">View similar line charts for available memory on each node with this query:</span></span>

    ```
    Type=Perf ObjectName=Memory CounterName="Available MBytes Memory" | measure avg(CounterValue) by Computer Interval 1HOUR.
    ```

    <span data-ttu-id="43074-153">Aby wyświetlić listę wszystkich węzłów, przedstawiający dokładną wartość średnia dla dostępna pamięć (MB) dla każdego węzła, skorzystaj z tej kwerendy:</span><span class="sxs-lookup"><span data-stu-id="43074-153">To view a listing of all your nodes, showing the exact average value for Available MBytes for each node, use this query:</span></span>

    ```
    Type=Perf (ObjectName=Memory) (CounterName="Available MBytes") | measure avg(CounterValue) by Computer
    ```

    ![Service Fabric](./media/log-analytics-service-fabric/11.png)

    <span data-ttu-id="43074-155">c.</span><span class="sxs-lookup"><span data-stu-id="43074-155">c.</span></span> <span data-ttu-id="43074-156">W przypadku, gdy chcesz przejść do określonego węzła, sprawdzając średniej godzinowej, użycie procesora CPU minimalne, maksymalne i 75 percentyl możesz to zrobić przy użyciu tej kwerendy (Zastąp pole komputera):</span><span class="sxs-lookup"><span data-stu-id="43074-156">In the case that you want to drill down into a specific node by examining the hourly average, minimum, maximum and 75-percentile CPU usage, you're able to do this by using this query (replace Computer field):</span></span>

    ```
    Type=Perf CounterName="% Processor Time" InstanceName=_Total Computer="BaconDC01.BaconLand.com"| measure min(CounterValue), avg(CounterValue), percentile75(CounterValue), max(CounterValue) by Computer Interval 1HOUR
    ```

    ![Service Fabric](./media/log-analytics-service-fabric/12.png)

<span data-ttu-id="43074-158">Przeczytaj więcej informacji na temat metryki wydajności w usługi Analiza dzienników w [blogu Operations Management Suite](https://blogs.technet.microsoft.com/msoms/tag/metrics/).</span><span class="sxs-lookup"><span data-stu-id="43074-158">Read more information about performance metrics in Log Analytics at the [Operations Management Suite blog](https://blogs.technet.microsoft.com/msoms/tag/metrics/).</span></span>


## <a name="adding-an-existing-storage-account-to-log-analytics"></a><span data-ttu-id="43074-159">Dodawanie istniejącego konta magazynu do analizy dzienników</span><span class="sxs-lookup"><span data-stu-id="43074-159">Adding an existing storage account to Log Analytics</span></span>

<span data-ttu-id="43074-160">Ten szablon po prostu dodaje istniejących kont magazynu do nowego lub istniejącego obszaru roboczego analizy dzienników.</span><span class="sxs-lookup"><span data-stu-id="43074-160">This template simply adds your existing storage accounts to a new or existing Log Analytics workspace.</span></span>

<span data-ttu-id="43074-161">[![Wdrażanie na platformie Azure](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Foms-existing-storage-account%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="43074-161">[![Deploy to Azure](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Foms-existing-storage-account%2Fazuredeploy.json)</span></span>

> [!NOTE]
> <span data-ttu-id="43074-162">Wybór grupy zasobów, jeśli pracujesz już istniejący obszar roboczy analizy dzienników wybierz "Użyj istniejącego" i wyszukaj grupę zasobów, zawierającą obszaru roboczego analizy dzienników.</span><span class="sxs-lookup"><span data-stu-id="43074-162">In selecting a Resource Group, if you're working with an already existing Log Analytics workspace, select "Use Existing" and search for the resource group containing the Log Analytics workspace.</span></span> <span data-ttu-id="43074-163">Utwórz nowy Jeśli jeden inaczej.</span><span class="sxs-lookup"><span data-stu-id="43074-163">Create a new one if otherwise.</span></span>
> <span data-ttu-id="43074-164">![Service Fabric](./media/log-analytics-service-fabric/8.png)</span><span class="sxs-lookup"><span data-stu-id="43074-164">![Service Fabric](./media/log-analytics-service-fabric/8.png)</span></span>
>
>

<span data-ttu-id="43074-165">Po wdrożeniu tego szablonu można zobaczyć magazynu konto podłączone do obszaru roboczego analizy dzienników.</span><span class="sxs-lookup"><span data-stu-id="43074-165">After this template has been deployed, you will be able to see the storage account connected to your Log Analytics workspace.</span></span> <span data-ttu-id="43074-166">W tym wystąpieniu jedno konto magazynu więcej po dodaniu do obszaru roboczego programu Exchange, utworzone powyżej.</span><span class="sxs-lookup"><span data-stu-id="43074-166">In this instance, I added one more storage account to the Exchange workspace I created above.</span></span>
<span data-ttu-id="43074-167">![Service Fabric](./media/log-analytics-service-fabric/9.png)</span><span class="sxs-lookup"><span data-stu-id="43074-167">![Service Fabric](./media/log-analytics-service-fabric/9.png)</span></span>

## <a name="view-service-fabric-events"></a><span data-ttu-id="43074-168">Wyświetl zdarzenia dotyczące sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="43074-168">View Service Fabric events</span></span>

<span data-ttu-id="43074-169">Po zakończeniu wdrożenia i sieci szkieletowej usług rozwiązania została włączona w obszarze roboczym, wybierz **sieci szkieletowej usług** kafelka w portalu usługi Analiza dzienników do uruchomienia pulpitu nawigacyjnego sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="43074-169">Once the deployments are completed and the Service Fabric solution has been enabled in your workspace, select the **Service Fabric** tile in the Log Analytics portal to launch the Service Fabric dashboard.</span></span> <span data-ttu-id="43074-170">Na pulpicie nawigacyjnym znajdują się kolumny wymienione w poniższej tabeli.</span><span class="sxs-lookup"><span data-stu-id="43074-170">The dashboard includes the columns in the following table.</span></span> <span data-ttu-id="43074-171">Każda kolumna wymieniono top 10 zdarzenia według liczby spełniających kryteria tej kolumny. dla określonego przedziału czasu.</span><span class="sxs-lookup"><span data-stu-id="43074-171">Each column lists the top 10 events by count matching that column's criteria for the specified time range.</span></span> <span data-ttu-id="43074-172">Możesz uruchomić wyszukiwanie dziennika, które zawiera całą listę klikając **zobaczyć wszystkie** w prawej dolnej każdej kolumny lub przez kliknięcie nagłówka kolumny.</span><span class="sxs-lookup"><span data-stu-id="43074-172">You can run a log search that provides the entire list by clicking **See all** at the right bottom of each column, or by clicking the column header.</span></span>

| <span data-ttu-id="43074-173">**Zdarzenie sieci szkieletowej usług**</span><span class="sxs-lookup"><span data-stu-id="43074-173">**Service Fabric event**</span></span> | <span data-ttu-id="43074-174">**Opis elementu**</span><span class="sxs-lookup"><span data-stu-id="43074-174">**description**</span></span> |
| --- | --- |
| <span data-ttu-id="43074-175">Problemy godne uwagi</span><span class="sxs-lookup"><span data-stu-id="43074-175">Notable Issues</span></span> |<span data-ttu-id="43074-176">Wyświetlanie problemy, takie jak RunAsyncFailures RunAsynCancellations i rozwijane węzła.</span><span class="sxs-lookup"><span data-stu-id="43074-176">A Display of issues such as RunAsyncFailures RunAsynCancellations and Node Downs.</span></span> |
| <span data-ttu-id="43074-177">Zdarzenia operacyjne</span><span class="sxs-lookup"><span data-stu-id="43074-177">Operational Events</span></span> |<span data-ttu-id="43074-178">Godne zdarzenia operacyjne takich jak uaktualniania aplikacji i wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="43074-178">Notable operational events such as application upgrade and deployments.</span></span> |
| <span data-ttu-id="43074-179">Zdarzenia niezawodne usługi</span><span class="sxs-lookup"><span data-stu-id="43074-179">Reliable Service Events</span></span> |<span data-ttu-id="43074-180">Zdarzenia zauważalne niezawodnej usługi takie Runasyncinvocations.</span><span class="sxs-lookup"><span data-stu-id="43074-180">Notable reliable service events such a Runasyncinvocations.</span></span> |
| <span data-ttu-id="43074-181">Zdarzenia aktora</span><span class="sxs-lookup"><span data-stu-id="43074-181">Actor Events</span></span> |<span data-ttu-id="43074-182">Godne aktora zdarzenia generowane przez micro usług, takich jak wyjątki wyrzucane przez metodę aktora, aktora aktywacji i deactivations i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="43074-182">Notable actor events generated by your micro-services, such as exceptions thrown by an actor method, actor activations and deactivations, and so on.</span></span> |
| <span data-ttu-id="43074-183">Zdarzenia aplikacji</span><span class="sxs-lookup"><span data-stu-id="43074-183">Application Events</span></span> |<span data-ttu-id="43074-184">Wszystkie niestandardowe ETW zdarzenia generowane przez aplikacje.</span><span class="sxs-lookup"><span data-stu-id="43074-184">All custom ETW events generated by your applications.</span></span> |

![Pulpit nawigacyjny sieci szkieletowej usług](./media/log-analytics-service-fabric/sf3.png)

![Pulpit nawigacyjny sieci szkieletowej usług](./media/log-analytics-service-fabric/sf4.png)

<span data-ttu-id="43074-187">W poniższej tabeli przedstawiono metody zbierania danych i inne szczegółowe informacje o jak dane są zbierane dla sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="43074-187">The following table shows data collection methods and other details about how data is collected for Service Fabric.</span></span>

| <span data-ttu-id="43074-188">Platformy</span><span class="sxs-lookup"><span data-stu-id="43074-188">platform</span></span> | <span data-ttu-id="43074-189">Bezpośrednie agenta</span><span class="sxs-lookup"><span data-stu-id="43074-189">Direct Agent</span></span> | <span data-ttu-id="43074-190">Agent programu Operations Manager</span><span class="sxs-lookup"><span data-stu-id="43074-190">Operations Manager agent</span></span> | <span data-ttu-id="43074-191">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="43074-191">Azure Storage</span></span> | <span data-ttu-id="43074-192">Wymagane programu Operations Manager?</span><span class="sxs-lookup"><span data-stu-id="43074-192">Operations Manager required?</span></span> | <span data-ttu-id="43074-193">Danych agenta programu Operations Manager są wysyłane za pośrednictwem grupy zarządzania</span><span class="sxs-lookup"><span data-stu-id="43074-193">Operations Manager agent data sent via management group</span></span> | <span data-ttu-id="43074-194">Częstotliwość kolekcji</span><span class="sxs-lookup"><span data-stu-id="43074-194">collection frequency</span></span> |
| --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="43074-195">Windows</span><span class="sxs-lookup"><span data-stu-id="43074-195">Windows</span></span> |  |  | <span data-ttu-id="43074-196">&#8226;</span><span class="sxs-lookup"><span data-stu-id="43074-196">&#8226;</span></span> |  |  |<span data-ttu-id="43074-197">10 minut</span><span class="sxs-lookup"><span data-stu-id="43074-197">10 minutes</span></span> |

> [!NOTE]
> <span data-ttu-id="43074-198">Zakres tych zdarzeń w rozwiązaniu sieci szkieletowej usług można zmienić, klikając **dane oparte na ostatnich 7 dni** w górnej części pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="43074-198">You can change the scope of these events in the Service Fabric solution by clicking **Data based on last 7 days** at the top of the dashboard.</span></span> <span data-ttu-id="43074-199">Można również wyświetlać zdarzenia generowane w ciągu ostatnich siedmiu dni, jeden dzień lub sześciu godzin.</span><span class="sxs-lookup"><span data-stu-id="43074-199">You can also show events generated within the last seven days, one day, or six hours.</span></span> <span data-ttu-id="43074-200">Umożliwia wybranie **niestandardowych** Aby określić zakres niestandardowy.</span><span class="sxs-lookup"><span data-stu-id="43074-200">Or, you can select **Custom** to specify a custom date range.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="43074-201">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="43074-201">Next steps</span></span>

* <span data-ttu-id="43074-202">Użyj [wyszukiwania dziennika analizy dzienników](log-analytics-log-searches.md) Aby wyświetlić szczegółowe dane zdarzeń usługi sieć szkieletowa usług.</span><span class="sxs-lookup"><span data-stu-id="43074-202">Use [Log Searches in Log Analytics](log-analytics-log-searches.md) to view detailed Service Fabric event data.</span></span>
