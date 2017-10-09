---
title: aaaAzure SQL bazy danych, metryki i rejestrowanie danych diagnostycznych | Dokumentacja firmy Microsoft
description: "Informacje na temat konfigurowania użycia zasobów toostore zasobów bazy danych SQL Azure, łączności i statystyki wykonania zapytania."
services: sql-database
documentationcenter: 
author: vvasic
manager: jhubbard
editor: 
ms.assetid: 89c2a155-c2fb-4b67-bc19-9b4e03c6d3bc
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/24/2017
ms.author: vvasic
ms.openlocfilehash: e6f9e24992ca4f84f701e1ef858e98dc7b481e28
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-metrics-and-diagnostics-logging"></a><span data-ttu-id="91285-103">Metryki bazy danych SQL Azure i rejestrowanie danych diagnostycznych</span><span class="sxs-lookup"><span data-stu-id="91285-103">Azure SQL Database metrics and diagnostics logging</span></span> 
<span data-ttu-id="91285-104">Baza danych SQL Azure może emitować metryki i dzienników diagnostycznych do monitorowania łatwiejsze.</span><span class="sxs-lookup"><span data-stu-id="91285-104">Azure SQL Database can emit metrics and diagnostic logs for easier monitoring.</span></span> <span data-ttu-id="91285-105">Można skonfigurować użycie zasobów toostore bazy danych SQL Azure, pracowników i sesje i łączności do jednej z tych zasobów platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="91285-105">You can configure Azure SQL Database toostore resource usage, workers and sessions, and connectivity into one of these Azure resources:</span></span>
- <span data-ttu-id="91285-106">**Usługa Azure Storage**: w celu archiwizowania ogromnych ilości danych telemetrycznych za niewielką cenę</span><span class="sxs-lookup"><span data-stu-id="91285-106">**Azure Storage**: For archiving vast amounts of telemetry for a small price</span></span>
- <span data-ttu-id="91285-107">**Azure Centrum zdarzeń**: do integracji z niestandardowe rozwiązanie monitorowania lub potoki gorących telemetrii bazy danych SQL Azure</span><span class="sxs-lookup"><span data-stu-id="91285-107">**Azure Event Hub**: For integrating Azure SQL Database telemetry with your custom monitoring solution or hot pipelines</span></span>
- <span data-ttu-id="91285-108">**Analiza dzienników Azure**: dla fabrycznej hello rozwiązania z raportowania, alerty i zmniejszenia możliwości monitorowania</span><span class="sxs-lookup"><span data-stu-id="91285-108">**Azure Log Analytics**: For out of hello box monitoring solution with reporting, alerting, and mitigating capabilities</span></span> 

    ![architektura](./media/sql-database-metrics-diag-logging/architecture.png)

## <a name="enable-logging"></a><span data-ttu-id="91285-110">Włącz rejestrowanie</span><span class="sxs-lookup"><span data-stu-id="91285-110">Enable logging</span></span>

<span data-ttu-id="91285-111">Metryki i rejestrowania diagnostyki nie jest włączona domyślnie.</span><span class="sxs-lookup"><span data-stu-id="91285-111">Metrics and diagnostics logging is not enabled by default.</span></span> <span data-ttu-id="91285-112">Można włączyć i zarządzać metryki i rejestrowanie danych diagnostycznych przy użyciu jednej z następujących metod hello:</span><span class="sxs-lookup"><span data-stu-id="91285-112">You can enable and manage metrics and diagnostics logging using one of hello following methods:</span></span>
- <span data-ttu-id="91285-113">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="91285-113">Azure portal</span></span>
- <span data-ttu-id="91285-114">PowerShell</span><span class="sxs-lookup"><span data-stu-id="91285-114">PowerShell</span></span>
- <span data-ttu-id="91285-115">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="91285-115">Azure CLI</span></span>
- <span data-ttu-id="91285-116">Interfejs API REST</span><span class="sxs-lookup"><span data-stu-id="91285-116">REST API</span></span> 
- <span data-ttu-id="91285-117">Szablon usługi Resource Manager</span><span class="sxs-lookup"><span data-stu-id="91285-117">Resource Manager template</span></span>

<span data-ttu-id="91285-118">Po włączeniu metryki i rejestrowanie danych diagnostycznych należy hello toospecify zasobów platformy Azure, w którym są zbierane wybranych danych.</span><span class="sxs-lookup"><span data-stu-id="91285-118">When you enable metrics and diagnostics logging, you need toospecify hello Azure resource where selected data is collected.</span></span> <span data-ttu-id="91285-119">Dostępne opcje:</span><span class="sxs-lookup"><span data-stu-id="91285-119">Options available:</span></span>
- <span data-ttu-id="91285-120">Log Analytics</span><span class="sxs-lookup"><span data-stu-id="91285-120">Log analytics</span></span>
- <span data-ttu-id="91285-121">Centrum zdarzeń</span><span class="sxs-lookup"><span data-stu-id="91285-121">Event Hub</span></span>
- <span data-ttu-id="91285-122">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="91285-122">Azure Storage</span></span> 

<span data-ttu-id="91285-123">Można udostępnić nowych zasobów platformy Azure lub wybierz istniejący zasób.</span><span class="sxs-lookup"><span data-stu-id="91285-123">You can provision a new Azure resource or select an existing resource.</span></span> <span data-ttu-id="91285-124">Po wybraniu hello zasobów magazynu, należy toospecify które toocollect danych.</span><span class="sxs-lookup"><span data-stu-id="91285-124">After selecting hello storage resource, you need toospecify which data toocollect.</span></span> <span data-ttu-id="91285-125">Dostępne opcje to:</span><span class="sxs-lookup"><span data-stu-id="91285-125">Options available include:</span></span>

- <span data-ttu-id="91285-126">**[metryki 1 minutę](sql-database-metrics-diag-logging.md#1-minute-metrics)**  — zawiera procent użycia jednostek DTU, limit jednostek dtu w warstwie, procent użycia procesora CPU danych fizycznych odczytu procent, dziennika zapisu procent, Powodzenie/nie powiodło się/zablokowane przez połączeń zapory, wartość procentowa sesji, procent pracowników Magazyn, procent użycia magazynu, XTP procent użycia magazynu</span><span class="sxs-lookup"><span data-stu-id="91285-126">**[1-minute metrics](sql-database-metrics-diag-logging.md#1-minute-metrics)** - contains DTU percentage, DTU limit, CPU percentage, Physical data read percentage, Log write percentage, Successful/Failed/Blocked by firewall connections, sessions percentage, workers percentage, storage, storage percentage, XTP storage percentage</span></span>

<span data-ttu-id="91285-127">Jeśli określisz konto AzureStorage lub Centrum zdarzeń można określić toospecify zasad przechowywania tych danych, która jest starsza niż wybrany okres jest usuwany.</span><span class="sxs-lookup"><span data-stu-id="91285-127">If you specify Event Hub or an AzureStorage account, you can specify a retention policy toospecify that data that is older than a selected time period is deleted.</span></span> <span data-ttu-id="91285-128">Jeśli określisz analizy dzienników zasady przechowywania hello zależy od wybranej warstwy cenowej hello.</span><span class="sxs-lookup"><span data-stu-id="91285-128">If you specify Log Analytics, hello retention policy depends on hello selected pricing tier.</span></span> <span data-ttu-id="91285-129">Przeczytaj więcej na temat [cennik analizy dzienników](https://azure.microsoft.com/pricing/details/log-analytics/).</span><span class="sxs-lookup"><span data-stu-id="91285-129">Read more about [Log Analytics pricing](https://azure.microsoft.com/pricing/details/log-analytics/).</span></span> 

<span data-ttu-id="91285-130">Zalecamy przeczytanie zarówno hello [omówienie metryk w Microsoft Azure](../monitoring-and-diagnostics/monitoring-overview-metrics.md) i [Omówienie programu Azure dzienników diagnostycznych](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) artykuły toogain zrozumienia nie tylko sposób rejestrowania tooenable, ale hello kategorie metryki i dziennika obsługiwane przez hello różne usługi platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="91285-130">We recommend that you read both hello [Overview of metrics in Microsoft Azure](../monitoring-and-diagnostics/monitoring-overview-metrics.md) and [Overview of Azure Diagnostic Logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) articles toogain an understanding of not only how tooenable logging, but hello metrics and log categories supported by hello various Azure services.</span></span>

### <a name="azure-portal"></a><span data-ttu-id="91285-131">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="91285-131">Azure portal</span></span>

<span data-ttu-id="91285-132">metryki tooenable i zbierania dzienników diagnostycznych w hello portalu Azure, przejdź do bazy danych Azure SQL tooyour lub puli elastycznej strony, a następnie kliknij **ustawień diagnostycznych**.</span><span class="sxs-lookup"><span data-stu-id="91285-132">tooenable metrics and diagnostic logs collection in hello Azure portal, navigate tooyour Azure SQL database or elastic pool page, and then click **Diagnostic settings**.</span></span>

   ![Włącz w hello portalu Azure](./media/sql-database-metrics-diag-logging/enable-portal.png)

### <a name="powershell"></a><span data-ttu-id="91285-134">PowerShell</span><span class="sxs-lookup"><span data-stu-id="91285-134">PowerShell</span></span>

<span data-ttu-id="91285-135">metryki tooenable i informacji diagnostycznych rejestrowanie przy użyciu programu PowerShell, użyj hello następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="91285-135">tooenable metrics and diagnostics logging using PowerShell, use hello following commands:</span></span>

- <span data-ttu-id="91285-136">Magazyn tooenable dzienników diagnostycznych na koncie magazynu, użyj tego polecenia:</span><span class="sxs-lookup"><span data-stu-id="91285-136">tooenable storage of Diagnostic Logs in a Storage Account, use this command:</span></span>

   ```powershell
   Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -StorageAccountId [your storage account id] -Enabled $true
   ```

   <span data-ttu-id="91285-137">Hello Identyfikatora konta magazynu jest identyfikator zasobu hello toowhich konta magazynu hello ma toosend hello dzienniki.</span><span class="sxs-lookup"><span data-stu-id="91285-137">hello Storage Account ID is hello resource id for hello storage account toowhich you want toosend hello logs.</span></span>

- <span data-ttu-id="91285-138">tooenable przesyłania strumieniowego dzienników diagnostycznych tooan Centrum zdarzeń, użyj tego polecenia:</span><span class="sxs-lookup"><span data-stu-id="91285-138">tooenable streaming of Diagnostic Logs tooan Event Hub, use this command:</span></span>

   ```powershell
   Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -ServiceBusRuleId [your service bus rule id] -Enabled $true
   ```

   <span data-ttu-id="91285-139">Hello identyfikator reguły magistrali usług to ciąg w formacie:</span><span class="sxs-lookup"><span data-stu-id="91285-139">hello Service Bus Rule ID is a string with this format:</span></span>

   ```powershell
   {service bus resource ID}/authorizationrules/{key name}
   ``` 

- <span data-ttu-id="91285-140">tooenable wysyłania dzienników diagnostycznych obszaru roboczego analizy dzienników tooa, użyj tego polecenia:</span><span class="sxs-lookup"><span data-stu-id="91285-140">tooenable sending of Diagnostic Logs tooa Log Analytics workspace, use this command:</span></span>

   ```powershell
   Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -WorkspaceId [resource id of hello log analytics workspace] -Enabled $true
   ```

- <span data-ttu-id="91285-141">Można uzyskać identyfikatora zasobu hello obszaru roboczego analizy dzienników przy użyciu hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="91285-141">You can obtain hello resource id of your Log Analytics workspace using hello following command:</span></span>

   ```powershell
   (Get-AzureRmOperationalInsightsWorkspace).ResourceId
   ```

<span data-ttu-id="91285-142">Tooenable te parametry można łączyć wiele opcji danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="91285-142">You can combine these parameters tooenable multiple output options.</span></span>

### <a name="cli"></a><span data-ttu-id="91285-143">Interfejs wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="91285-143">CLI</span></span>

<span data-ttu-id="91285-144">metryki tooenable i diagnostyki rejestrowania przy użyciu hello Azure CLI hello Użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="91285-144">tooenable metrics and diagnostics logging using hello Azure CLI, use hello following commands:</span></span>

- <span data-ttu-id="91285-145">Magazyn tooenable dzienników diagnostycznych na koncie magazynu, użyj tego polecenia:</span><span class="sxs-lookup"><span data-stu-id="91285-145">tooenable storage of Diagnostic Logs in a Storage Account, use this command:</span></span>

   ```azurecli-interactive
   azure insights diagnostic set --resourceId <resourceId> --storageId <storageAccountId> --enabled true
   ```

   <span data-ttu-id="91285-146">Hello Identyfikatora konta magazynu jest identyfikator zasobu hello toowhich konta magazynu hello ma toosend hello dzienniki.</span><span class="sxs-lookup"><span data-stu-id="91285-146">hello Storage Account ID is hello resource id for hello storage account toowhich you want toosend hello logs.</span></span>

- <span data-ttu-id="91285-147">tooenable przesyłania strumieniowego dzienników diagnostycznych tooan Centrum zdarzeń, użyj tego polecenia:</span><span class="sxs-lookup"><span data-stu-id="91285-147">tooenable streaming of Diagnostic Logs tooan Event Hub, use this command:</span></span>

   ```azurecli-interactive
   azure insights diagnostic set --resourceId <resourceId> --serviceBusRuleId <serviceBusRuleId> --enabled true
   ```

   <span data-ttu-id="91285-148">Hello identyfikator reguły magistrali usług to ciąg w formacie:</span><span class="sxs-lookup"><span data-stu-id="91285-148">hello Service Bus Rule ID is a string with this format:</span></span>

   ```azurecli-interactive
   {service bus resource ID}/authorizationrules/{key name}
   ```

- <span data-ttu-id="91285-149">tooenable wysyłania dzienników diagnostycznych obszaru roboczego analizy dzienników tooa, użyj tego polecenia:</span><span class="sxs-lookup"><span data-stu-id="91285-149">tooenable sending of Diagnostic Logs tooa Log Analytics workspace, use this command:</span></span>

   ```azurecli-interactive
   azure insights diagnostic set --resourceId <resourceId> --workspaceId <resource id of hello log analytics workspace> --enabled true
   ```

<span data-ttu-id="91285-150">Tooenable te parametry można łączyć wiele opcji danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="91285-150">You can combine these parameters tooenable multiple output options.</span></span>

### <a name="rest-api"></a><span data-ttu-id="91285-151">Interfejs API REST</span><span class="sxs-lookup"><span data-stu-id="91285-151">REST API</span></span>

<span data-ttu-id="91285-152">Przeczytaj temat zbyt[zmiany ustawień diagnostycznych przy użyciu interfejsu API REST Monitor Azure hello](https://msdn.microsoft.com/library/azure/dn931931.aspx).</span><span class="sxs-lookup"><span data-stu-id="91285-152">Read about how too[change Diagnostic settings using hello Azure Monitor REST API](https://msdn.microsoft.com/library/azure/dn931931.aspx).</span></span> 

### <a name="resource-manager-template"></a><span data-ttu-id="91285-153">Szablon usługi Resource Manager</span><span class="sxs-lookup"><span data-stu-id="91285-153">Resource Manager template</span></span>

<span data-ttu-id="91285-154">Przeczytaj temat zbyt[Włącz ustawienia diagnostyki na tworzenie zasobów przy użyciu szablonu usługi Resource Manager](../monitoring-and-diagnostics/monitoring-enable-diagnostic-logs-using-template.md).</span><span class="sxs-lookup"><span data-stu-id="91285-154">Read about how too[enable Diagnostic settings at resource creation using Resource Manager template](../monitoring-and-diagnostics/monitoring-enable-diagnostic-logs-using-template.md).</span></span> 

## <a name="stream-into-log-analytics"></a><span data-ttu-id="91285-155">Strumień do analizy dzienników</span><span class="sxs-lookup"><span data-stu-id="91285-155">Stream into Log Analytics</span></span> 
<span data-ttu-id="91285-156">Metryki bazy danych SQL Azure i dzienników diagnostycznych mogła być przesłana strumieniowo do analizy dzienników przy użyciu opcji wbudowanych "Wyślij tooLog Analytics" hello, w portalu hello lub przez włączenie analizy dzienników diagnostycznych ustawienia za pomocą poleceń cmdlet programu Azure PowerShell, Azure CLI lub Azure Monitor REST INTERFEJS API.</span><span class="sxs-lookup"><span data-stu-id="91285-156">Azure SQL Database metrics and diagnostic logs can be streamed into Log Analytics using hello built-in “Send tooLog Analytics” option in hello portal, or by enabling Log Analytics in a diagnostic setting via Azure PowerShell cmdlets, Azure CLI, or Azure Monitor REST API.</span></span>

### <a name="installation-overview"></a><span data-ttu-id="91285-157">Omówienie instalacji</span><span class="sxs-lookup"><span data-stu-id="91285-157">Installation overview</span></span>

<span data-ttu-id="91285-158">Monitorowanie floty bazy danych SQL Azure jest proste — analizy dzienników.</span><span class="sxs-lookup"><span data-stu-id="91285-158">Monitoring Azure SQL Database fleet is simple with Log Analytics.</span></span> <span data-ttu-id="91285-159">Wymagane są trzy kroki:</span><span class="sxs-lookup"><span data-stu-id="91285-159">Three steps are required:</span></span>

1.  <span data-ttu-id="91285-160">Utwórz zasób analizy dzienników</span><span class="sxs-lookup"><span data-stu-id="91285-160">Create Log Analytics resource</span></span>
2.  <span data-ttu-id="91285-161">Konfigurowanie metryki toorecord baz danych i dzienników diagnostycznych do hello utworzone analizy dzienników</span><span class="sxs-lookup"><span data-stu-id="91285-161">Configure databases toorecord metrics and diagnostic logs into hello created Log Analytics</span></span>
3.  <span data-ttu-id="91285-162">Zainstaluj **analiza SQL Azure** rozwiązania z galerii w analizy dzienników</span><span class="sxs-lookup"><span data-stu-id="91285-162">Install **Azure SQL Analytics** solution from gallery in Log Analytics</span></span>

### <a name="create-log-analytics-resource"></a><span data-ttu-id="91285-163">Utwórz zasób analizy dzienników</span><span class="sxs-lookup"><span data-stu-id="91285-163">Create Log Analytics resource</span></span>

1. <span data-ttu-id="91285-164">Kliknij przycisk **nowy** w menu po lewej stronie powitania.</span><span class="sxs-lookup"><span data-stu-id="91285-164">Click **New** in hello left-hand menu.</span></span>
2. <span data-ttu-id="91285-165">Kliknij przycisk **monitorowanie i zarządzanie**</span><span class="sxs-lookup"><span data-stu-id="91285-165">Click **Monitoring + Management**</span></span>
3. <span data-ttu-id="91285-166">Kliknij przycisk **dziennika analityka**</span><span class="sxs-lookup"><span data-stu-id="91285-166">Click **Log Analytics**</span></span>
4. <span data-ttu-id="91285-167">Wypełnienie w postaci analizy dzienników hello hello wymagane informacje dodatkowe: Nazwa obszaru roboczego, subskrypcji, grupy zasobów, lokalizacji i warstwę cenową.</span><span class="sxs-lookup"><span data-stu-id="91285-167">Fill in hello Log Analytics form with hello additional information required: workspace name, subscription, resource group, location, and pricing tier.</span></span>

   ![analizy dzienników](./media/sql-database-metrics-diag-logging/log-analytics.png)

### <a name="configure-databases-toorecord-metrics-and-diagnostic-logs"></a><span data-ttu-id="91285-169">Konfigurowanie metryki toorecord baz danych i dzienników diagnostycznych</span><span class="sxs-lookup"><span data-stu-id="91285-169">Configure databases toorecord metrics and diagnostic logs</span></span>

<span data-ttu-id="91285-170">Hello Najprostszym sposobem tooconfigure gdzie baz danych rejestrowania ich metryki odbywa się za pośrednictwem hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="91285-170">hello easiest way tooconfigure where databases record their metrics is through hello Azure portal.</span></span> <span data-ttu-id="91285-171">W portalu Azure Witaj, przejdź tooyour zasobów bazy danych SQL Azure i kliknij **ustawień diagnostycznych**.</span><span class="sxs-lookup"><span data-stu-id="91285-171">In hello Azure portal, navigate tooyour Azure SQL Database resource and click **Diagnostics settings**.</span></span> 

### <a name="install-hello-azure-sql-analytics-solution-from-gallery"></a><span data-ttu-id="91285-172">Zainstaluj hello rozwiązania analizy SQL Azure z galerii</span><span class="sxs-lookup"><span data-stu-id="91285-172">Install hello Azure SQL Analytics solution from gallery</span></span>  

1. <span data-ttu-id="91285-173">Po utworzeniu hello zasobów analizy dzienników i danych jest przepływać do niego, należy zainstalować rozwiązania analizy SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="91285-173">Once hello Log Analytics resource is created and your data is flowing into it, install Azure SQL Analytics solution.</span></span> <span data-ttu-id="91285-174">Można to zrobić za pomocą hello **galerii rozwiązań** który można znaleźć na powitania OMS głównej i w menu po stronie powitania.</span><span class="sxs-lookup"><span data-stu-id="91285-174">This can be done through hello **Solutions Gallery** that you can find on hello OMS homepage and in hello side menu.</span></span> <span data-ttu-id="91285-175">W galerii hello, Znajdź i kliknij **analiza SQL Azure** rozwiązanie i kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="91285-175">In hello gallery, find and click **Azure SQL Analytics** solution and click **Add**.</span></span>

   ![rozwiązanie monitorowania](./media/sql-database-metrics-diag-logging/monitoring-solution.png)

2. <span data-ttu-id="91285-177">Na stronie głównej OMS nowy Kafelek o nazwie **analiza SQL Azure** pojawi się.</span><span class="sxs-lookup"><span data-stu-id="91285-177">On your OMS homepage, a new tile called **Azure SQL Analytics** appears.</span></span> <span data-ttu-id="91285-178">Wybranie tego kafelka otwiera pulpitu nawigacyjnego Azure SQL Analytics hello.</span><span class="sxs-lookup"><span data-stu-id="91285-178">Selecting this tile opens hello Azure SQL Analytics dashboard.</span></span>

### <a name="using-azure-sql-analytics-solution"></a><span data-ttu-id="91285-179">Przy użyciu rozwiązania analizy Azure SQL</span><span class="sxs-lookup"><span data-stu-id="91285-179">Using Azure SQL Analytics Solution</span></span>

<span data-ttu-id="91285-180">Analiza SQL Azure jest hierarchiczne pulpit nawigacyjny, który pozwala toonavigate przez hierarchię hello zasobów bazy danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="91285-180">Azure SQL Analytics is a hierarchical dashboard that allows you toonavigate through hello hierarchy of Azure SQL Database resources.</span></span> <span data-ttu-id="91285-181">Ta umożliwia możliwości możesz toodo wysokiego poziomu, monitorowania może również umożliwia tooscope Twojego monitorowania hello toojust prawo zestawu zasobów.</span><span class="sxs-lookup"><span data-stu-id="91285-181">This capability enables you toodo high-level monitoring but it also enables you tooscope your monitoring toojust hello right set of resources.</span></span>
<span data-ttu-id="91285-182">Pulpit nawigacyjny zawiera listy hello różnych zasobów w ramach zasobu hello wybrane.</span><span class="sxs-lookup"><span data-stu-id="91285-182">Dashboard contains hello lists of different resources under hello selected resource.</span></span> <span data-ttu-id="91285-183">Na przykład dla wybranej subskrypcji można wyświetlić hello wszystkich serwerów, pule elastyczne i baz danych, które należy toohello wybrane subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="91285-183">For example, for a selected subscription you can see hello all servers, elastic pools and databases that belong toohello selected subscription.</span></span> <span data-ttu-id="91285-184">Ponadto baz danych i pul elastycznych widać hello metryki użycia zasobów tego zasobu.</span><span class="sxs-lookup"><span data-stu-id="91285-184">Additionally, for Elastic Pools and databases, you can see hello resource usage metrics of that resource.</span></span> <span data-ttu-id="91285-185">Obejmuje wykresy jednostek dtu w warstwie, procesor CPU we/wy, dziennika, sesje, pracowników, połączeń i magazynu w GB.</span><span class="sxs-lookup"><span data-stu-id="91285-185">This includes charts for DTU, CPU, IO, LOG, sessions, workers, connections, and storage in GB.</span></span>

## <a name="stream-into-azure-event-hub"></a><span data-ttu-id="91285-186">Strumień do Centrum zdarzeń platformy Azure</span><span class="sxs-lookup"><span data-stu-id="91285-186">Stream into Azure Event Hub</span></span>

<span data-ttu-id="91285-187">Metryki bazy danych SQL Azure i dzienników diagnostycznych mogła być przesłana strumieniowo do Centrum zdarzeń przy użyciu opcji wbudowanych "strumienia tooan Centrum zdarzeń" hello, w portalu hello, lub włączenie identyfikator reguły magistrali usług w ustawienie diagnostyczne za pomocą polecenia cmdlet programu PowerShell usługi Azure, Azure CLI lub Azure Monitor REST INTERFEJS API.</span><span class="sxs-lookup"><span data-stu-id="91285-187">Azure SQL Database metrics and diagnostic logs can be streamed into Event Hub using hello built-in “Stream tooan event hub” option in hello portal, or by enabling Service Bus Rule Id in a diagnostic setting via Azure PowerShell Cmdlets, Azure CLI, or Azure Monitor REST API.</span></span> 

### <a name="what-toodo-with-metrics-and-diagnostic-logs-in-event-hub"></a><span data-ttu-id="91285-188">Jakie toodo dzienników diagnostycznych w Centrum zdarzeń i metryk?</span><span class="sxs-lookup"><span data-stu-id="91285-188">What toodo with metrics and diagnostic logs in Event Hub?</span></span>
<span data-ttu-id="91285-189">Po hello wybrane dane są przesyłane strumieniowo do Centrum zdarzeń, jesteś jedną tooenabling bliżej krok zaawansowanych scenariuszy monitorowania.</span><span class="sxs-lookup"><span data-stu-id="91285-189">Once hello selected data is streamed into Event Hub, you are one step closer tooenabling advanced monitoring scenarios.</span></span> <span data-ttu-id="91285-190">Usługa Event Hubs działa jako "drzwi wejściowe" dla potoku zdarzeń hello, a po pobraniu danych do Centrum zdarzeń, można je przekształcać i przechowywane za pomocą dowolnego dostawcy analiz w czasie rzeczywistym lub kart przetwarzania wsadowego i magazynowania.</span><span class="sxs-lookup"><span data-stu-id="91285-190">Event Hubs acts as hello "front door" for an event pipeline, and once data is collected into an Event Hub, it can be transformed and stored using any real-time analytics provider or batching/storage adapters.</span></span> <span data-ttu-id="91285-191">Usługa Event Hubs oddziela hello Wytwarzanie strumienia zdarzeń od użycia hello tych zdarzeń, dzięki czemu odbiorcy zdarzeń mogą uzyskiwać dostęp do zdarzeń hello w swoim własnym harmonogramem.</span><span class="sxs-lookup"><span data-stu-id="91285-191">Event Hubs decouples hello production of a stream of events from hello consumption of those events, so that event consumers can access hello events on their own schedule.</span></span> <span data-ttu-id="91285-192">Aby uzyskać więcej informacji o Centrum zdarzeń Zobacz:</span><span class="sxs-lookup"><span data-stu-id="91285-192">For more information on Event Hub, see:</span></span>

- <span data-ttu-id="91285-193">[Co to jest usługa Azure Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md)?</span><span class="sxs-lookup"><span data-stu-id="91285-193">[What are Azure Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md)?</span></span>
- [<span data-ttu-id="91285-194">Rozpoczynanie pracy z usługą Event Hubs</span><span class="sxs-lookup"><span data-stu-id="91285-194">Get started with Event Hubs</span></span>](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)


<span data-ttu-id="91285-195">Poniżej przedstawiono kilka sposobów może używać hello przesyłania strumieniowego możliwości:</span><span class="sxs-lookup"><span data-stu-id="91285-195">Here are just a few ways you might use hello streaming capability:</span></span>

-   <span data-ttu-id="91285-196">Wyświetl kondycję usługi przez przesyłania strumieniowego "aktywnej ścieżki" danych tooPowerBI — za pomocą usługi Event Hubs, Stream Analytics i usługi Power BI, metryki i diagnostyki danych w pobliżu wgląd w czasie rzeczywistym mogą łatwo przekształcić na usługami Azure.</span><span class="sxs-lookup"><span data-stu-id="91285-196">View service health by streaming “hot path” data tooPowerBI - Using Event Hubs, Stream Analytics, and PowerBI, you can easily transform your metrics and diagnostics data into near real-time insights on your Azure services.</span></span> <span data-ttu-id="91285-197">Omówienie sposobu przetwarzania danych za pomocą usługi Stream Analytics tooset się usługi Event Hubs i używać usługi Power BI jako dane wyjściowe, zobacz [Stream Analytics i usługi Power BI](../stream-analytics/stream-analytics-power-bi-dashboard.md).</span><span class="sxs-lookup"><span data-stu-id="91285-197">For an overview of how tooset up an Event Hubs, process data with Stream Analytics, and use PowerBI as an output, see [Stream Analytics and Power BI](../stream-analytics/stream-analytics-power-bi-dashboard.md).</span></span>
-   <span data-ttu-id="91285-198">Strumień dzienniki firm toothird rejestrowania i dane telemetryczne strumieni — centra zdarzeń przy użyciu przesyłania strumieniowego można można uzyskać Twoje metryki i dzienniki diagnostyczne w toodifferent rozwiązań analitycznych innych firm monitorowania i dziennika.</span><span class="sxs-lookup"><span data-stu-id="91285-198">Stream logs toothird-party logging and telemetry streams – Using Event Hubs streaming you can get your metrics and diagnostic logs in toodifferent third-party monitoring and log analytics solutions.</span></span> 
-   <span data-ttu-id="91285-199">Jeśli masz już platformy telemetrii niestandardowej lub są tylko pomyśleć o budynku jedną hello skalowalnej publikowania / subskrypcji, rodzaj usługi Event Hubs umożliwia tooflexibly pozyskiwania dzienników diagnostycznych kompilacji telemetria niestandardowa i platforma rejestrowania.</span><span class="sxs-lookup"><span data-stu-id="91285-199">Build a custom telemetry and logging platform – If you already have a custom-built telemetry platform or are just thinking about building one, hello highly scalable publish-subscribe nature of Event Hubs allows you tooflexibly ingest diagnostic logs.</span></span> <span data-ttu-id="91285-200">Zobacz [Dan Rosanova przewodnik toousing centra zdarzeń w skali globalnej platformę telemetrii](https://azure.microsoft.com/documentation/videos/build-2015-designing-and-sizing-a-global-scale-telemetry-platform-on-azure-event-Hubs/).</span><span class="sxs-lookup"><span data-stu-id="91285-200">See [Dan Rosanova’s guide toousing Event Hubs in a global scale telemetry platform](https://azure.microsoft.com/documentation/videos/build-2015-designing-and-sizing-a-global-scale-telemetry-platform-on-azure-event-Hubs/).</span></span>

## <a name="stream-into-azure-storage"></a><span data-ttu-id="91285-201">Strumień do magazynu Azure</span><span class="sxs-lookup"><span data-stu-id="91285-201">Stream into Azure Storage</span></span>

<span data-ttu-id="91285-202">Metryki bazy danych SQL Azure i dzienniki diagnostyczne mogą być przechowywane w magazynie Azure przy użyciu wbudowanych opcji "Archiwum tooa konta magazynu" hello, w portalu Azure hello, lub włączenie usługi Azure Storage w ustawienie diagnostyczne za pomocą polecenia cmdlet programu PowerShell usługi Azure, Azure CLI lub Azure Monitor interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="91285-202">Azure SQL Database metrics and diagnostic logs can be stored into Azure Storage using hello built-in "Archive tooa storage account” option in hello Azure portal, or by enabling Azure Storage in a diagnostic setting via Azure PowerShell Cmdlets, Azure CLI, or Azure Monitor REST API.</span></span>

### <a name="schema-of-metrics-and-diagnostic-logs-in-hello-storage-account"></a><span data-ttu-id="91285-203">Schemat metryki i dzienników diagnostycznych na koncie magazynu hello</span><span class="sxs-lookup"><span data-stu-id="91285-203">Schema of metrics and diagnostic logs in hello storage account</span></span>

<span data-ttu-id="91285-204">Po skonfigurowaniu metryki i zbierania dzienników diagnostycznych kontenera magazynu jest tworzony na koncie magazynu hello wybranych podczas hello pierwsze wiersze danych są dostępne.</span><span class="sxs-lookup"><span data-stu-id="91285-204">Once you have set up metrics and diagnostic logs collection, a storage container is created in hello storage account you selected when hello first rows of data are available.</span></span> <span data-ttu-id="91285-205">Struktura Hello tych obiektów blob jest:</span><span class="sxs-lookup"><span data-stu-id="91285-205">hello structure of these blobs is:</span></span>

```powershell
insights-{metrics|logs}-{category name}/resourceId=/SUBSCRIPTIONS/{subscription ID}/ RESOURCEGROUPS/{resource group name}/PROVIDERS/Microsoft.SQL/servers/{resource_server}/ databases/{database_name}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json
```
    
<span data-ttu-id="91285-206">Lub po prostu:</span><span class="sxs-lookup"><span data-stu-id="91285-206">Or, more simply:</span></span>

```powershell
insights-{metrics|logs}-{category name}/resourceId=/{resource Id}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json
```

<span data-ttu-id="91285-207">Na przykład może być nazwa obiektu blob dla 1-minutowych metryki:</span><span class="sxs-lookup"><span data-stu-id="91285-207">For example, a blob name for 1-minute metrics might be:</span></span>

```powershell
insights-metrics-minute/resourceId=/SUBSCRIPTIONS/s1id1234-5679-0123-4567-890123456789/RESOURCEGROUPS/TESTRESOURCEGROUP/PROVIDERS/MICROSOFT.SQL/ servers/Server1/databases/database1/y=2016/m=08/d=22/h=18/m=00/PT1H.json
```

<span data-ttu-id="91285-208">W przypadku, gdy chcesz toorecord hello dane z hello puli elastycznej, nazwa obiektu blob różni się nieco:</span><span class="sxs-lookup"><span data-stu-id="91285-208">In case you want toorecord hello data from hello Elastic Pool, blob name is a bit different:</span></span>

```powershell
insights-{metrics|logs}-{category name}/resourceId=/SUBSCRIPTIONS/{subscription ID}/ RESOURCEGROUPS/{resource group name}/PROVIDERS/Microsoft.SQL/servers/{resource_server}/ elasticPools/{elastic_pool_name}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json
```

### <a name="download-metrics-and-logs-from-azure-storage"></a><span data-ttu-id="91285-209">Pobierz dzienniki i metryki z usługi Azure storage</span><span class="sxs-lookup"><span data-stu-id="91285-209">Download metrics and logs from Azure storage</span></span>

<span data-ttu-id="91285-210">Zobacz [pobrać metryki i dzienników diagnostycznych z usługi Azure Storage](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs)</span><span class="sxs-lookup"><span data-stu-id="91285-210">See [Download metrics and diagnostic logs from Azure Storage](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs)</span></span>

## <a name="1-minute-metrics"></a><span data-ttu-id="91285-211">metryki 1 minuta</span><span class="sxs-lookup"><span data-stu-id="91285-211">1-minute metrics</span></span>

| |  |
|---|---|
|<span data-ttu-id="91285-212">**Zasób**</span><span class="sxs-lookup"><span data-stu-id="91285-212">**Resource**</span></span>|<span data-ttu-id="91285-213">**Metryki**</span><span class="sxs-lookup"><span data-stu-id="91285-213">**Metrics**</span></span>|
|<span data-ttu-id="91285-214">Database (Baza danych)</span><span class="sxs-lookup"><span data-stu-id="91285-214">Database</span></span>|<span data-ttu-id="91285-215">Procent użycia jednostek DTU, używane jednostek dtu w warstwie, limit jednostek dtu w warstwie, procent użycia procesora CPU i procent odczytu danych fizycznych, dziennika zapisu procent, Powodzenie/nie powiodło się/zablokowane przez połączeń zapory, wartość procentowa sesji, procent pracowników, magazynu, procent użycia magazynu, XTP procent użycia magazynu, Zakleszczenie</span><span class="sxs-lookup"><span data-stu-id="91285-215">DTU percentage, DTU used, DTU limit, CPU percentage, Physical data read percentage, Log write percentage, Successful/Failed/Blocked by firewall connections, sessions percentage, workers percentage, storage, storage percentage, XTP storage percentage, deadlocks</span></span> |
|<span data-ttu-id="91285-216">Puli elastycznej</span><span class="sxs-lookup"><span data-stu-id="91285-216">Elastic pool</span></span>|<span data-ttu-id="91285-217">procent liczby jednostek eDTU używany eDTU, limit liczby jednostek eDTU, procent użycia procesora CPU i procent odczytu danych fizycznych, dziennika zapisu procent, procent sesji, procent pracowników, magazynu, procent użycia magazynu, limit magazynu, XTP procent użycia magazynu</span><span class="sxs-lookup"><span data-stu-id="91285-217">eDTU percentage, eDTU used, eDTU limit, CPU percentage, Physical data read percentage, Log write percentage, sessions percentage, workers percentage, storage, storage percentage, storage limit, XTP storage percentage</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="91285-218">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="91285-218">Next steps</span></span>

- <span data-ttu-id="91285-219">Przeczytaj zarówno hello [omówienie metryk w Microsoft Azure](../monitoring-and-diagnostics/monitoring-overview-metrics.md) i [Omówienie programu Azure dzienników diagnostycznych](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) artykuły toogain zrozumienia nie tylko jak tooenable rejestrowania, ale hello metryki i dziennika kategorii obsługiwane przez hello różne usługi platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="91285-219">Read both hello [Overview of metrics in Microsoft Azure](../monitoring-and-diagnostics/monitoring-overview-metrics.md) and [Overview of Azure Diagnostic Logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) articles toogain an understanding of not only how tooenable logging, but hello metrics and log categories supported by hello various Azure services.</span></span>
- <span data-ttu-id="91285-220">Przeczytaj te toolearn artykuły dotyczące centra zdarzeń:</span><span class="sxs-lookup"><span data-stu-id="91285-220">Read these articles toolearn about event hubs:</span></span>
   - <span data-ttu-id="91285-221">[Co to jest usługa Azure Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md)?</span><span class="sxs-lookup"><span data-stu-id="91285-221">[What are Azure Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md)?</span></span>
   - [<span data-ttu-id="91285-222">Rozpoczynanie pracy z usługą Event Hubs</span><span class="sxs-lookup"><span data-stu-id="91285-222">Get started with Event Hubs</span></span>](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)
- <span data-ttu-id="91285-223">Zobacz [pobrać metryki i dzienników diagnostycznych z usługi Azure Storage](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs)</span><span class="sxs-lookup"><span data-stu-id="91285-223">See [Download metrics and diagnostic logs from Azure Storage](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs)</span></span>
