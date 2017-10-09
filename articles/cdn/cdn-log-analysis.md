---
title: "Analiza aaaLog dla usługi Azure CDN | Dokumentacja firmy Microsoft"
description: "Klienta można włączyć analizy dziennika dla usługi Azure CDN."
services: cdn
documentationcenter: 
author: smcevoy
manager: erikre
editor: 
ms.assetid: 95e18b3c-b987-46c2-baa8-a27a029e3076
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/03/2017
ms.author: v-semcev
ms.openlocfilehash: 56e5a4fec46fd156cf38252732afb4522741d009
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="diagnostics-logs-for-azure-cdn"></a><span data-ttu-id="9a5e4-103">Dzienniki diagnostyczne dla usługi Azure CDN</span><span class="sxs-lookup"><span data-stu-id="9a5e4-103">Diagnostics Logs for Azure CDN</span></span>

<span data-ttu-id="9a5e4-104">Po włączeniu sieci CDN w warstwie aplikacji będzie prawdopodobnie mają toomonitor hello CDN użycia, Sprawdź kondycję hello firmy i rozwiązywania potencjalnych problemów.</span><span class="sxs-lookup"><span data-stu-id="9a5e4-104">After enabling CDN for your application, you will likely want toomonitor hello CDN usage, check hello health of your delivery, and troubleshoot potential issues.</span></span> <span data-ttu-id="9a5e4-105">Usługi Azure CDN zapewnia dodatkowe możliwości z [sieci CDN w warstwie podstawowa analiza](cdn-analyze-usage-patterns.md) i [dzienników diagnostycznych](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs)</span><span class="sxs-lookup"><span data-stu-id="9a5e4-105">Azure CDN provides these capabilities with [CDN Core Analytics](cdn-analyze-usage-patterns.md) and [Diagnostic Logs](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs)</span></span>

## <a name="cdn-core-analytics"></a><span data-ttu-id="9a5e4-106">Sieci CDN w warstwie podstawowa analiza</span><span class="sxs-lookup"><span data-stu-id="9a5e4-106">CDN Core Analytics</span></span>
<span data-ttu-id="9a5e4-107">Bieżący użytkownik usługi Azure CDN z Verizon standardowa lub premium profilu masz już możliwe tooview podstawowa analiza w portalu dodatkowym hello dostępny przy użyciu opcji "Manage" hello z hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="9a5e4-107">As a current Azure CDN user with Verizon standard or premium profile, you are already able tooview core analytics in hello supplemental portal accessible via hello "Manage" option from hello Azure portal.</span></span> 

## <a name="azure-diagnostic-logs"></a><span data-ttu-id="9a5e4-108">Dzienniki diagnostyczne platformy Azure</span><span class="sxs-lookup"><span data-stu-id="9a5e4-108">Azure Diagnostic Logs</span></span>

<span data-ttu-id="9a5e4-109">Azure przy użyciu tej nowej funkcji, można teraz wyświetlić podstawowa analiza i zapisać je w co najmniej jednego miejsca docelowe, w tym:</span><span class="sxs-lookup"><span data-stu-id="9a5e4-109">Azure With this new feature, you can now view core analytics and save them into one or more destinations including:</span></span>

 - <span data-ttu-id="9a5e4-110">Konto usługi Azure Storage</span><span class="sxs-lookup"><span data-stu-id="9a5e4-110">Azure Storage account</span></span>
 - <span data-ttu-id="9a5e4-111">Azure Event Hubs</span><span class="sxs-lookup"><span data-stu-id="9a5e4-111">Azure Event Hubs</span></span>
 - [<span data-ttu-id="9a5e4-112">Repozytorium OMS analizy dzienników</span><span class="sxs-lookup"><span data-stu-id="9a5e4-112">OMS Log Analytics repository</span></span>](https://docs.microsoft.com/azure/log-analytics/log-analytics-get-started)
 
 <span data-ttu-id="9a5e4-113">Ta funkcja jest dostępna dla wszystkich punktów końcowych usługi CDN należące tooVerizon (Standard i Premium) oraz profilów usługi CDN Akamai (Standard).</span><span class="sxs-lookup"><span data-stu-id="9a5e4-113">This feature is available for all CDN endpoints belonging tooVerizon (Standard & Premium) and Akamai (Standard) CDN Profiles.</span></span>

<span data-ttu-id="9a5e4-114">Dzienniki diagnostyczne Zezwalaj metryki użycia podstawowe tooexport z sieci CDN punktu końcowego tooa różnych źródeł, dzięki czemu będzie można korzystać dostosowany sposób.</span><span class="sxs-lookup"><span data-stu-id="9a5e4-114">Diagnostics logs allow you tooexport basic usage metrics from your CDN endpoint tooa variety of sources so that you can consume them in a customized way.</span></span> <span data-ttu-id="9a5e4-115">Na przykład można wykonać hello następujące typy eksportu danych:</span><span class="sxs-lookup"><span data-stu-id="9a5e4-115">For example, you can do hello following types of data export:</span></span>

- <span data-ttu-id="9a5e4-116">Eksportuj tooblob pamięci masowej, Eksportuj tooCSV i Generuj wykresy w programie excel.</span><span class="sxs-lookup"><span data-stu-id="9a5e4-116">Export data tooblob storage, export tooCSV, and generate graphs in excel.</span></span>
- <span data-ttu-id="9a5e4-117">Eksportowanie danych tooevent koncentratorów i skorelowania danych z innych usług azure.</span><span class="sxs-lookup"><span data-stu-id="9a5e4-117">Export data tooevent hubs and correlate with data from other azure services.</span></span>
- <span data-ttu-id="9a5e4-118">Eksportowanie danych toolog analytics i dane widoku w własne obszar roboczy OMS</span><span class="sxs-lookup"><span data-stu-id="9a5e4-118">Export data toolog analytics and view data in your own OMS work space</span></span>

<span data-ttu-id="9a5e4-119">Witaj rysunku poniżej przedstawiono typowe przeglądanie sieci CDN w warstwie podstawowa analiza danych.</span><span class="sxs-lookup"><span data-stu-id="9a5e4-119">hello following figure shows a typical CDN Core Analytics view into data.</span></span>

![Portal — dzienniki diagnostyczne](./media/cdn-diagnostics-log/01_OMS-workspace.png)

<span data-ttu-id="9a5e4-121">*Rysunek 1 — widok sieci CDN w warstwie podstawowa analiza*</span><span class="sxs-lookup"><span data-stu-id="9a5e4-121">*Figure 1 - CDN Core Analytics view*</span></span>

<span data-ttu-id="9a5e4-122">następujące wskazówki Hello przechodzi przez schemat hello hello core analizy danych, etapy włączenie funkcji hello dostarczania ich toovarious miejsc docelowych i korzystanie z tych miejsc docelowych.</span><span class="sxs-lookup"><span data-stu-id="9a5e4-122">hello following walkthrough goes through hello schema of hello core analytics data, steps involved in enabling hello feature and delivering them toovarious destinations, and consuming from these destinations.</span></span>

## <a name="enable-logging-with-azure-portal"></a><span data-ttu-id="9a5e4-123">Włącz rejestrowanie z portalu Azure</span><span class="sxs-lookup"><span data-stu-id="9a5e4-123">Enable logging with Azure portal</span></span>

> [!NOTE]
> <span data-ttu-id="9a5e4-124">Witaj dzienników diagnostycznych są włączone **poza** domyślnie.</span><span class="sxs-lookup"><span data-stu-id="9a5e4-124">hello diagnostics logs are turned **off** by default.</span></span> 

<span data-ttu-id="9a5e4-125">Wykonaj kroki hello poniżej rejestrowanie tooenable z sieci CDN w warstwie podstawowa analiza:</span><span class="sxs-lookup"><span data-stu-id="9a5e4-125">Follow hello steps below tooenable logging with CDN Core Analytics:</span></span>

<span data-ttu-id="9a5e4-126">Zaloguj się toohello [portalu Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9a5e4-126">Sign in toohello [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="9a5e4-127">Jeśli nie masz już włączone dla przepływu pracy, w sieci CDN [włączyć usługi Azure CDN](cdn-create-new-endpoint.md) przed kontynuowaniem.</span><span class="sxs-lookup"><span data-stu-id="9a5e4-127">If you don't already have CDN enabled for your workflow, [Enable Azure CDN](cdn-create-new-endpoint.md) before you continue.</span></span>

1. <span data-ttu-id="9a5e4-128">W portalu hello Przejdź zbyt**profilu CDN**.</span><span class="sxs-lookup"><span data-stu-id="9a5e4-128">In hello portal, navigate too**CDN profile**.</span></span>
2. <span data-ttu-id="9a5e4-129">Wybierz profil CDN, a następnie wybierz punkt końcowy CDN hello, które mają tooenable **dzienników diagnostycznych**.</span><span class="sxs-lookup"><span data-stu-id="9a5e4-129">Select a CDN profile, then select hello CDN endpoint that you want tooenable **Diagnostics Logs**.</span></span>

    ![Portal — dzienniki diagnostyczne](./media/cdn-diagnostics-log/02_Browse-to-Diagnostics-logs.png)

3. <span data-ttu-id="9a5e4-131">Przejdź za**dzienników diagnostycznych** bloku w obszarze **monitorowanie** sekcji, a następnie zmień stan hello zbyt**na**.</span><span class="sxs-lookup"><span data-stu-id="9a5e4-131">Go too**Diagnostics Logs** blade Under **Monitoring** section, then change hello status too**On**.</span></span>

    ![Portal — dzienniki diagnostyczne](./media/cdn-diagnostics-log/03_Diagnostics-logs-options.png)

### <a name="enable-logging-with-azure-storage"></a><span data-ttu-id="9a5e4-133">Włącz rejestrowanie z usługą Azure Storage</span><span class="sxs-lookup"><span data-stu-id="9a5e4-133">Enable logging with Azure Storage</span></span>
    
<span data-ttu-id="9a5e4-134">toouse dzienniki hello toostore magazynu Azure, wybierz **archiwum konta magazynu tooa**, wybierz dni przechowywania i kliknij przycisk **CoreAnalytics** w obszarze **dziennika**.</span><span class="sxs-lookup"><span data-stu-id="9a5e4-134">toouse Azure Storage toostore hello logs, select **Archive tooa storage account**, select retention days, and click **CoreAnalytics** under **Log**.</span></span>

![Portal — dzienniki diagnostyczne](./media/cdn-diagnostics-log/04_Diagnostics-logs-storage.png)

<span data-ttu-id="9a5e4-136">*Rysunek 2 — rejestrowanie z usługą Azure Storage*</span><span class="sxs-lookup"><span data-stu-id="9a5e4-136">*Figure 2 - Logging with Azure Storage*</span></span>

### <a name="logging-with-oms-log-analytics"></a><span data-ttu-id="9a5e4-137">Rejestrowanie z OMS analizy dzienników</span><span class="sxs-lookup"><span data-stu-id="9a5e4-137">Logging with OMS Log Analytics</span></span>

<span data-ttu-id="9a5e4-138">toouse analizy dzienników OMS toostore hello dzienniki, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="9a5e4-138">toouse OMS Log Analytics toostore hello logs, follow these steps:</span></span>

1. <span data-ttu-id="9a5e4-139">Z hello **dzienników diagnostycznych** bloku w obszarze **monitorowanie**, wybierz pozycję **wysyłania tooLog Analytics** z</span><span class="sxs-lookup"><span data-stu-id="9a5e4-139">From hello **Diagnostics Logs** blade Under **Monitoring**, select **Send tooLog Analytics** from</span></span> 

    ![Portal — dzienniki diagnostyczne](./media/cdn-diagnostics-log/05_Ready-to-Configure.png)    

2. <span data-ttu-id="9a5e4-141">Konfiguruj rejestrowanie analizy dzienników hello, klikając polecenie Konfiguruj.</span><span class="sxs-lookup"><span data-stu-id="9a5e4-141">Configure hello Log Analytics logging by clicking on Configure.</span></span> <span data-ttu-id="9a5e4-142">Zostanie wyświetlone okno dialogowe tooa, gdzie poprzedniej obszaru roboczego wybierz lub Utwórz nową.</span><span class="sxs-lookup"><span data-stu-id="9a5e4-142">This takes you tooa dialog where you can select a previous workspace or create a new one.</span></span>

    ![Portal — dzienniki diagnostyczne](./media/cdn-diagnostics-log/06_Choose-workspace.png)

3. <span data-ttu-id="9a5e4-144">Kliknij przycisk **Utwórz nowy obszar roboczy**.</span><span class="sxs-lookup"><span data-stu-id="9a5e4-144">Click **Create New Workspace**.</span></span>

    ![Portal — dzienniki diagnostyczne](./media/cdn-diagnostics-log/07_Create-new.png)

4. <span data-ttu-id="9a5e4-146">Następnie musisz wybrać nową nazwę obszaru roboczego, istniejącej subskrypcji, grupy zasobów (Nowa lub istniejąca), lokalizacji i warstwę cenową.</span><span class="sxs-lookup"><span data-stu-id="9a5e4-146">Next you must select a new workspace name, existing subscription, resource group (new or existing), location, and pricing tier.</span></span> <span data-ttu-id="9a5e4-147">Dostępna jest opcja hello przypinanie ten pulpit nawigacyjny tooyour konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="9a5e4-147">You have hello option of pinning this configuration tooyour dashboard.</span></span> <span data-ttu-id="9a5e4-148">Kliknij przycisk OK toocomplete hello konfigurację.</span><span class="sxs-lookup"><span data-stu-id="9a5e4-148">Click OK toocomplete hello configuration.</span></span>

    <span data-ttu-id="9a5e4-149">Obok obszaru roboczego powinna zostać wyświetlona z nazwami grup obszarem roboczym pakietu OMS i zasobów.</span><span class="sxs-lookup"><span data-stu-id="9a5e4-149">Next you should see your workspace with your OMS Workspace and Resource group names.</span></span> <span data-ttu-id="9a5e4-150">Nazwy musi być unikatowa i można używać tylko litery, cyfry i łączniki.</span><span class="sxs-lookup"><span data-stu-id="9a5e4-150">Names must be unique and can only use letters, numbers, and hyphens.</span></span> <span data-ttu-id="9a5e4-151">Spacje i znaki podkreślenia są niedozwolone.</span><span class="sxs-lookup"><span data-stu-id="9a5e4-151">Spaces and underscores are not allowed.</span></span> 

    ![Portal — dzienniki diagnostyczne](./media/cdn-diagnostics-log/08_Workspace-resource.png)

5. <span data-ttu-id="9a5e4-153">Następnie Pobierz krótki komunikat informujący, że obszar roboczy użytkownika został utworzony i są zwracane tooyour rejestrowania ekranu konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="9a5e4-153">You next get a short message saying that your workspace has been created and you are returned tooyour logging configuration screen.</span></span> <span data-ttu-id="9a5e4-154">Można potwierdzić hello nazwę obszaru roboczego analizy dzienników.</span><span class="sxs-lookup"><span data-stu-id="9a5e4-154">You can confirm hello name of your Log Analytics workspace.</span></span>

    ![Portal — dzienniki diagnostyczne](./media/cdn-diagnostics-log/09_Return-to-logging.png)

    <span data-ttu-id="9a5e4-156">Po skonfigurowaniu hello konfiguracji analizy dzienników upewnij się, że zaznaczysz pola CoreAnalytics hello rejestrowania w sieci CDN.</span><span class="sxs-lookup"><span data-stu-id="9a5e4-156">Once you have set up hello Log Analytics configuration, make sure you also check hello CoreAnalytics box for CDN logging.</span></span>

6. <span data-ttu-id="9a5e4-157">Jeśli wszystko jest preferencjom tooyour, kliknij hello **zapisać** u góry okna dialogowego konfiguracji hello hello.</span><span class="sxs-lookup"><span data-stu-id="9a5e4-157">If everything is tooyour liking, click hello **Save** button at hello top of hello configuration dialog.</span></span>

    ![Portal — dzienniki diagnostyczne](./media/cdn-diagnostics-log/10_Save-me.png)

    <span data-ttu-id="9a5e4-159">Witaj **zapisać** przycisk nie jest już aktywne i że hello na/wyłączanie przycisku jest teraz ON, ale blue zamiast purpurowy.</span><span class="sxs-lookup"><span data-stu-id="9a5e4-159">hello **Save** button is no longer active and that hello ON/OFF button is now ON, but blue instead of purple.</span></span>

7. <span data-ttu-id="9a5e4-160">Toosee nowy obszar roboczy OMS, przejdź tooyour portalu Azure pulpitu nawigacyjnego, kliknij nazwę hello obszaru roboczego analizy dzienników.</span><span class="sxs-lookup"><span data-stu-id="9a5e4-160">If you want toosee your new OMS workspace, go tooyour Azure portal Dashboard, click hello name of your Log Analytics workspace.</span></span> <span data-ttu-id="9a5e4-161">Następnie zostanie wyświetlony obszar roboczy (Upewnij się, że obszar roboczy OMS jest wyróżnione po lewej stronie powitania).</span><span class="sxs-lookup"><span data-stu-id="9a5e4-161">Next you will see your workspace (make sure that OMS Workspace is highlighted on hello left).</span></span> <span data-ttu-id="9a5e4-162">Polecenie hello portalu OMS kafelka toosee obszaru roboczego w repozytorium OMS hello.</span><span class="sxs-lookup"><span data-stu-id="9a5e4-162">Click on hello OMS Portal tile toosee your workspace in hello OMS repository.</span></span> 

    ![Portal — dzienniki diagnostyczne](./media/cdn-diagnostics-log/11_OMS-dashboard.png) 

    <span data-ttu-id="9a5e4-164">Repozytorium OMS jest teraz gotowy toolog danych.</span><span class="sxs-lookup"><span data-stu-id="9a5e4-164">Your OMS repository is now ready toolog data.</span></span> <span data-ttu-id="9a5e4-165">W celu tooconsume danych, należy użyć [rozwiązania OMS](#consuming-oms-log-analytics-data), wymienionych w dalszej części tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="9a5e4-165">In order tooconsume that data, you must use an [OMS Solution](#consuming-oms-log-analytics-data), covered later in this article.</span></span>

<span data-ttu-id="9a5e4-166">Więcej informacji na temat opóźnienia danych dziennika [tutaj](#log-data-delays).</span><span class="sxs-lookup"><span data-stu-id="9a5e4-166">For more information about log data delays, go [here](#log-data-delays).</span></span>

## <a name="enable-logging-with-powershell"></a><span data-ttu-id="9a5e4-167">Włącz rejestrowanie przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="9a5e4-167">Enable logging with PowerShell</span></span>

<span data-ttu-id="9a5e4-168">Poniżej znajduje się przykład w sposób tooenable i Pobierz dzienniki diagnostyczne za pośrednictwem hello polecenia cmdlet programu PowerShell usługi Azure.</span><span class="sxs-lookup"><span data-stu-id="9a5e4-168">Below is an example on how tooenable and get Diagnostic Logs via hello Azure PowerShell Cmdlets.</span></span>

###<a name="enabling-diagnostic-logs-in-a-storage-account"></a><span data-ttu-id="9a5e4-169">Włączanie diagnostyki logowania na koncie magazynu</span><span class="sxs-lookup"><span data-stu-id="9a5e4-169">Enabling Diagnostic Logs in a Storage Account</span></span>

<span data-ttu-id="9a5e4-170">Zaloguj się najpierw, a następnie wybierz subskrypcję:</span><span class="sxs-lookup"><span data-stu-id="9a5e4-170">First log in and select a subscription:</span></span>

    Login-AzureRmAccount 

    Select-AzureSubscription -SubscriptionId 


<span data-ttu-id="9a5e4-171">tooEnable dzienników diagnostycznych na koncie magazynu, użyj tego polecenia:</span><span class="sxs-lookup"><span data-stu-id="9a5e4-171">tooEnable Diagnostic Logs in a Storage Account, use this command:</span></span>

```powershell
    Set-AzureRmDiagnosticSetting -ResourceId "/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Cdn/profiles/{profileName}/endpoints/{endpointName}" -StorageAccountId "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ClassicStorage/storageAccounts/{storageAccountName}" -Enabled $true -Categories CoreAnalytics
```
<span data-ttu-id="9a5e4-172">tooEnable dzienników diagnostyki w obszarze roboczym pakietu OMS, użyj tego polecenia:</span><span class="sxs-lookup"><span data-stu-id="9a5e4-172">tooEnable Diagnostics Logs in an OMS workspace, use this command:</span></span>

```powershell
    Set-AzureRmDiagnosticSetting -ResourceId "/subscriptions/`{subscriptionId}<subscriptionId>
    .<subscriptionName>" -WorkspaceId "/subscriptions/<workspaceId>.<workspaceName>" -Enabled $true -Categories CoreAnalytics 
```



## <a name="consuming-diagnostics-logs-from-azure-storage"></a><span data-ttu-id="9a5e4-173">Korzystanie z dzienników diagnostycznych z usługi Azure Storage</span><span class="sxs-lookup"><span data-stu-id="9a5e4-173">Consuming diagnostics logs from Azure Storage</span></span>
<span data-ttu-id="9a5e4-174">W tej sekcji opisano schemat hello hello sieci CDN w warstwie podstawowa analiza, w jaki sposób te są zorganizowane w ramach konta magazynu platformy Azure i zawiera przykładowy kod toodownload hello rejestruje się w pliku CSV tooa.</span><span class="sxs-lookup"><span data-stu-id="9a5e4-174">This section describes hello schema of hello CDN core analytics, how these are organized inside of an Azure Storage Account and provides sample code toodownload hello logs in tooa CSV file.</span></span>

### <a name="using-microsoft-azure-storage-explorer"></a><span data-ttu-id="9a5e4-175">Za pomocą Eksploratora usługi Storage platformy Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="9a5e4-175">Using Microsoft Azure Storage Explorer</span></span>
<span data-ttu-id="9a5e4-176">Przed są dostępne dane analityczne core hello hello konta magazynu Azure, musisz najpierw narzędzie tooaccess hello zawartość na koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="9a5e4-176">Before you can access hello core analytics data from hello Azure Storage Account, you first need a tool tooaccess hello contents in a storage account.</span></span> <span data-ttu-id="9a5e4-177">Mimo że rynku hello dostępnych jest kilka narzędzi, hello, który firma Microsoft zaleca jest hello Eksploratora magazynu Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="9a5e4-177">While there are several tools available in hello market, hello one that we recommend is hello Microsoft Azure Storage Explorer.</span></span> <span data-ttu-id="9a5e4-178">Możesz pobrać narzędzie hello [tutaj](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="9a5e4-178">You can download hello tool from [here](http://storageexplorer.com/).</span></span> <span data-ttu-id="9a5e4-179">Po pobieranie i instalowanie oprogramowania hello, skonfiguruj ją toouse hello tego samego konta magazynu Azure, które zostały skonfigurowane jako docelowy toohello dzienników Diagnostyka sieci CDN.</span><span class="sxs-lookup"><span data-stu-id="9a5e4-179">After downloading and installing hello software, configure it toouse hello same Azure Storage Account that was configured as a destination toohello CDN Diagnostics Logs.</span></span>

1.  <span data-ttu-id="9a5e4-180">Otwórz **Eksploratora usługi Storage platformy Microsoft Azure**</span><span class="sxs-lookup"><span data-stu-id="9a5e4-180">Open **Microsoft Azure Storage Explorer**</span></span>
2.  <span data-ttu-id="9a5e4-181">Zlokalizuj konto magazynu hello</span><span class="sxs-lookup"><span data-stu-id="9a5e4-181">Locate hello storage account</span></span>
3.  <span data-ttu-id="9a5e4-182">Przejdź toohello **"Kontenerów obiektów Blob"** węźle tego magazynu konta, a następnie rozwiń węzeł hello</span><span class="sxs-lookup"><span data-stu-id="9a5e4-182">Go toohello **“Blob Containers”** node under this storage account and expand hello node</span></span>
4.  <span data-ttu-id="9a5e4-183">Wybierz hello kontener o nazwie **"insights dzienniki coreanalytics"** i kliknij ją dwukrotnie</span><span class="sxs-lookup"><span data-stu-id="9a5e4-183">Select hello container named **“insights-logs-coreanalytics”** and double-click it</span></span>
5.  <span data-ttu-id="9a5e4-184">Wyniki Pokaż się na powitania prawym okienku począwszy hello najpierw poziomu, który wygląda podobnie **"resourceId ="**.</span><span class="sxs-lookup"><span data-stu-id="9a5e4-184">Results show up on hello right-hand pane starting with hello first level, which looks like **“resourceId=”**.</span></span> <span data-ttu-id="9a5e4-185">Klikaj końca hello aż zostanie wyświetlony plik hello **PT1H.json**.</span><span class="sxs-lookup"><span data-stu-id="9a5e4-185">Continue clicking all hello way until you see hello file **PT1H.json**.</span></span> <span data-ttu-id="9a5e4-186">Zobacz powitania po Uwaga wyjaśnienie hello ścieżki.</span><span class="sxs-lookup"><span data-stu-id="9a5e4-186">See hello following note for explanation of hello path.</span></span>
6.  <span data-ttu-id="9a5e4-187">Każdy obiekt blob **PT1H.json** reprezentuje hello analizy dzienników dla jednej godziny dla określonego punktu końcowego CDN lub jego domeny niestandardowej.</span><span class="sxs-lookup"><span data-stu-id="9a5e4-187">Each blob **PT1H.json** represents hello analytics logs for one hour for a specific CDN endpoint or its custom domain.</span></span>
7.  <span data-ttu-id="9a5e4-188">Schemat Hello hello zawartość tego pliku JSON zostało opisane w sekcji hello schematu z hello Core analizy dzienników</span><span class="sxs-lookup"><span data-stu-id="9a5e4-188">hello schema of hello contents of this JSON file is described in hello section Schema of hello Core Analytics Logs</span></span>


> [!NOTE]
> <span data-ttu-id="9a5e4-189">**Format ścieżki obiektu blob**</span><span class="sxs-lookup"><span data-stu-id="9a5e4-189">**Blob path format**</span></span>
> 
> <span data-ttu-id="9a5e4-190">Dzienniki Analytics Core są generowane co godzinę.</span><span class="sxs-lookup"><span data-stu-id="9a5e4-190">Core Analytics logs are generated every hour.</span></span> <span data-ttu-id="9a5e4-191">Wszystkie dane przez godzinę są zbierane i przechowywane wewnątrz pojedynczego obiektu Blob Azure jako ładunek JSON.</span><span class="sxs-lookup"><span data-stu-id="9a5e4-191">All data for an hour are collected and stored inside a single Azure Blob as a JSON payload.</span></span> <span data-ttu-id="9a5e4-192">toothis ścieżka Hello obiektów Blob platformy Azure pojawi się tak, jakby to hierarchiczna struktura.</span><span class="sxs-lookup"><span data-stu-id="9a5e4-192">hello path toothis Azure Blob appears as if there is a hierarchical structure.</span></span> <span data-ttu-id="9a5e4-193">Jest ponieważ interpretuje narzędzia Eksplorator magazynu hello "/" jako separatora katalogu, pokazuje hello hierarchii dla wygody.</span><span class="sxs-lookup"><span data-stu-id="9a5e4-193">This is because hello Storage explorer tool interprets '/' as a directory separator and shows hello hierarchy for convenience.</span></span> <span data-ttu-id="9a5e4-194">W rzeczywistości hello pełną ścieżkę reprezentuje tylko hello nazwa obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="9a5e4-194">Actually, hello whole path just represents hello blob name.</span></span> <span data-ttu-id="9a5e4-195">Następuje to nazwa obiektu blob hello hello następującą konwencją</span><span class="sxs-lookup"><span data-stu-id="9a5e4-195">This name of hello blob follows hello following naming convention</span></span> 
    
    resourceId=/SUBSCRIPTIONS/{Subscription Id}/RESOURCEGROUPS/{Resource Group Name}/PROVIDERS/MICROSOFT.CDN/PROFILES/{Profile Name}/ENDPOINTS/{Endpoint Name}/ y={Year}/m={Month}/d={Day}/h={Hour}/m={Minutes}/PT1H.json

<span data-ttu-id="9a5e4-196">**Opis pola:**</span><span class="sxs-lookup"><span data-stu-id="9a5e4-196">**Description of fields:**</span></span>

|<span data-ttu-id="9a5e4-197">wartość</span><span class="sxs-lookup"><span data-stu-id="9a5e4-197">value</span></span>|<span data-ttu-id="9a5e4-198">description</span><span class="sxs-lookup"><span data-stu-id="9a5e4-198">description</span></span>|
|-------|---------|
|<span data-ttu-id="9a5e4-199">Identyfikator subskrypcji</span><span class="sxs-lookup"><span data-stu-id="9a5e4-199">Subscription ID</span></span>    |<span data-ttu-id="9a5e4-200">Identyfikator hello subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="9a5e4-200">ID of hello Azure Subscription.</span></span> <span data-ttu-id="9a5e4-201">To jest w formacie Guid hello.</span><span class="sxs-lookup"><span data-stu-id="9a5e4-201">This is in hello Guid format.</span></span>|
|<span data-ttu-id="9a5e4-202">Zasób</span><span class="sxs-lookup"><span data-stu-id="9a5e4-202">Resource</span></span> |<span data-ttu-id="9a5e4-203">Nazwa grupy zasobów CDN hello toowhich, grupy zasobów hello należą.</span><span class="sxs-lookup"><span data-stu-id="9a5e4-203">Group Name   Name of hello resource group toowhich hello CDN resources belong.</span></span>|
|<span data-ttu-id="9a5e4-204">Nazwa profilu</span><span class="sxs-lookup"><span data-stu-id="9a5e4-204">Profile Name</span></span> |<span data-ttu-id="9a5e4-205">Nazwa hello profilu CDN</span><span class="sxs-lookup"><span data-stu-id="9a5e4-205">Name of hello CDN Profile</span></span>|
|<span data-ttu-id="9a5e4-206">Nazwa punktu końcowego</span><span class="sxs-lookup"><span data-stu-id="9a5e4-206">Endpoint Name</span></span> |<span data-ttu-id="9a5e4-207">Nazwa hello punktu końcowego CDN</span><span class="sxs-lookup"><span data-stu-id="9a5e4-207">Name of hello CDN Endpoint</span></span>|
|<span data-ttu-id="9a5e4-208">Roku</span><span class="sxs-lookup"><span data-stu-id="9a5e4-208">Year</span></span>|  <span data-ttu-id="9a5e4-209">Reprezentacja 4-cyfrowego roku hello na przykład 2017 r.</span><span class="sxs-lookup"><span data-stu-id="9a5e4-209">4-digit representation of hello year for example, 2017</span></span>|
|<span data-ttu-id="9a5e4-210">Miesiąc</span><span class="sxs-lookup"><span data-stu-id="9a5e4-210">Month</span></span>| <span data-ttu-id="9a5e4-211">Reprezentacja 2-cyfrowy numer miesiąca hello.</span><span class="sxs-lookup"><span data-stu-id="9a5e4-211">2-digit representation of hello month number.</span></span> <span data-ttu-id="9a5e4-212">01 stycznia =... 12 grudnia =</span><span class="sxs-lookup"><span data-stu-id="9a5e4-212">01=January ... 12=December</span></span>|
|<span data-ttu-id="9a5e4-213">Dzień</span><span class="sxs-lookup"><span data-stu-id="9a5e4-213">Day</span></span>|   <span data-ttu-id="9a5e4-214">Reprezentacja 2 cyfry hello dzień miesiąca hello</span><span class="sxs-lookup"><span data-stu-id="9a5e4-214">2 digit representation of hello day of hello month</span></span>|
|<span data-ttu-id="9a5e4-215">PT1H.JSON</span><span class="sxs-lookup"><span data-stu-id="9a5e4-215">PT1H.json</span></span>| <span data-ttu-id="9a5e4-216">Rzeczywisty plik JSON, których są przechowywane dane analizy hello</span><span class="sxs-lookup"><span data-stu-id="9a5e4-216">Actual JSON file where hello analytics data is stored</span></span>|

### <a name="exporting-hello-core-analytics-data-tooa-csv-file"></a><span data-ttu-id="9a5e4-217">Eksportowanie hello podstawowe dane analityczne tooa pliku CSV</span><span class="sxs-lookup"><span data-stu-id="9a5e4-217">Exporting hello Core Analytics Data tooa CSV File</span></span>

<span data-ttu-id="9a5e4-218">toomake it łatwe tooaccess hello podstawowa analiza, firma Microsoft udostępnia przykładowy kod dla narzędzia, która umożliwia pobieranie hello pliki w formacie JSON na format pliku płaskim oddzielone przecinkami, które mogą być używane tooeasily Tworzenie wykresów lub innych agregacji.</span><span class="sxs-lookup"><span data-stu-id="9a5e4-218">toomake it easy tooaccess hello Core Analytics, we provide a sample code for a tool, which allows downloading hello JSON files into a flat comma-separated file format, which can be used tooeasily create charts or other aggregations.</span></span>

<span data-ttu-id="9a5e4-219">Oto, jak można użyć narzędzia hello:</span><span class="sxs-lookup"><span data-stu-id="9a5e4-219">Here is how you can use hello tool:</span></span>

1.  <span data-ttu-id="9a5e4-220">Odwiedź hello github łącza: [https://github.com/Azure-Samples/azure-cdn-samples/tree/master/CoreAnalytics-ExportToCsv](https://github.com/Azure-Samples/azure-cdn-samples/tree/master/CoreAnalytics-ExportToCsv )</span><span class="sxs-lookup"><span data-stu-id="9a5e4-220">Visit hello github link: [https://github.com/Azure-Samples/azure-cdn-samples/tree/master/CoreAnalytics-ExportToCsv ](https://github.com/Azure-Samples/azure-cdn-samples/tree/master/CoreAnalytics-ExportToCsv )</span></span>
2.  <span data-ttu-id="9a5e4-221">Pobierz kod hello</span><span class="sxs-lookup"><span data-stu-id="9a5e4-221">Download hello code</span></span>
3.  <span data-ttu-id="9a5e4-222">Postępuj zgodnie z instrukcjami toocompile i skonfigurować</span><span class="sxs-lookup"><span data-stu-id="9a5e4-222">Follow instructions toocompile and configure</span></span>
4.  <span data-ttu-id="9a5e4-223">Uruchom narzędzie hello</span><span class="sxs-lookup"><span data-stu-id="9a5e4-223">Run hello tool</span></span>
5.  <span data-ttu-id="9a5e4-224">Wynikowy plik CSV zawiera hello analizy danych w prostych płaskiej hierarchii.</span><span class="sxs-lookup"><span data-stu-id="9a5e4-224">Resulting CSV file shows hello analytics data in a simple flat hierarchy.</span></span>

## <a name="consuming-diagnostics-logs-from-an-oms-log-analytics-repository"></a><span data-ttu-id="9a5e4-225">Korzystanie z dzienników diagnostycznych z repozytorium OMS analizy dzienników</span><span class="sxs-lookup"><span data-stu-id="9a5e4-225">Consuming diagnostics logs from an OMS Log Analytics repository</span></span>
<span data-ttu-id="9a5e4-226">Analiza dzienników jest usługą w operacji pakietu zarządzania (OMS), obejmujący z chmury i lokalnych środowiskach toomaintain ich dostępności i wydajności.</span><span class="sxs-lookup"><span data-stu-id="9a5e4-226">Log Analytics is a service in Operations Management Suite (OMS) that monitors your cloud and on-premises environments toomaintain their availability and performance.</span></span> <span data-ttu-id="9a5e4-227">Zbiera dane generowane przez zasobów w swoich środowiskach w chmurze i lokalnie i z innych monitorowania analizy tooprovide narzędzi w wielu źródeł.</span><span class="sxs-lookup"><span data-stu-id="9a5e4-227">It collects data generated by resources in your cloud and on-premises environments and from other monitoring tools tooprovide analysis across multiple sources.</span></span> 

<span data-ttu-id="9a5e4-228">toouse analizy dzienników, należy najpierw [włączyć rejestrowanie](#enable-logging-with-azure-storage) toohello Analiza dzienników Azure OMS repozytorium, co zostało omówione w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="9a5e4-228">toouse Log Analytics, you must [enable logging](#enable-logging-with-azure-storage) toohello Azure OMS Log Analytics repository, which is discussed earlier in this article.</span></span>

### <a name="using-hello-oms-repository"></a><span data-ttu-id="9a5e4-229">Przy użyciu hello repozytorium OMS</span><span class="sxs-lookup"><span data-stu-id="9a5e4-229">Using hello OMS Repository</span></span>

 <span data-ttu-id="9a5e4-230">diagram przedstawia hello architektura hello danych wejściowych i wyjściowych repozytorium hello Hello:</span><span class="sxs-lookup"><span data-stu-id="9a5e4-230">hello following diagram shows hello architecture of hello inputs and outputs of hello repository:</span></span>

![Repozytorium analizy dziennika OMS](./media/cdn-diagnostics-log/12_Repo-overview.png)

<span data-ttu-id="9a5e4-232">*Rysunek 3 – repozytorium analizy dzienników*</span><span class="sxs-lookup"><span data-stu-id="9a5e4-232">*Figure 3 - Log Analytics Repository*</span></span>

<span data-ttu-id="9a5e4-233">Można wyświetlić dane hello na różne sposoby, za pomocą rozwiązania do zarządzania.</span><span class="sxs-lookup"><span data-stu-id="9a5e4-233">You can display hello data in a variety of ways by using Management Solutions.</span></span> <span data-ttu-id="9a5e4-234">Rozwiązania do zarządzania można uzyskać z hello [portalu Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/monitoring-management?page=1&subcategories=management-solutions).</span><span class="sxs-lookup"><span data-stu-id="9a5e4-234">You can obtain Management Solutions from hello [Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/monitoring-management?page=1&subcategories=management-solutions).</span></span>

<span data-ttu-id="9a5e4-235">Rozwiązania do zarządzania można zainstalować z portalu Azure marketplace, klikając hello **Pobierz teraz** łącze u dołu hello poszczególnych rozwiązań.</span><span class="sxs-lookup"><span data-stu-id="9a5e4-235">You can install management solutions from Azure marketplace by clicking hello **Get it now** link at hello bottom of each solution.</span></span>

### <a name="adding-an-oms-cdn-management-solution"></a><span data-ttu-id="9a5e4-236">Dodawanie rozwiązania do zarządzania OMS CDN</span><span class="sxs-lookup"><span data-stu-id="9a5e4-236">Adding an OMS CDN Management Solution</span></span>

<span data-ttu-id="9a5e4-237">Wykonaj te kroki tooadd rozwiązania do zarządzania:</span><span class="sxs-lookup"><span data-stu-id="9a5e4-237">Follow these steps tooadd a Management Solution:</span></span>

1.   <span data-ttu-id="9a5e4-238">Jeśli jeszcze tego nie zrobiono, zaloguj się toohello portalu Azure przy użyciu subskrypcji platformy Azure i przejdź tooyour pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="9a5e4-238">If you haven't already done so, sign in toohello Azure portal using your Azure subscription and go tooyour Dashboard.</span></span>
    <span data-ttu-id="9a5e4-239">![Pulpit nawigacyjny platformy Azure](./media/cdn-diagnostics-log/13_Azure-dashboard.png)</span><span class="sxs-lookup"><span data-stu-id="9a5e4-239">![Azure Dashboard](./media/cdn-diagnostics-log/13_Azure-dashboard.png)</span></span>

2. <span data-ttu-id="9a5e4-240">W hello **nowy** bloku w obszarze **Marketplace**, wybierz pozycję **monitorowanie i zarządzanie**.</span><span class="sxs-lookup"><span data-stu-id="9a5e4-240">In hello **New** blade under **Marketplace**, select **Monitoring + management**.</span></span>

    ![Portal Marketplace](./media/cdn-diagnostics-log/14_Marketplace.png)

3. <span data-ttu-id="9a5e4-242">W hello **monitorowanie i zarządzanie** bloku, kliknij przycisk **zobaczyć wszystkie**.</span><span class="sxs-lookup"><span data-stu-id="9a5e4-242">In hello **Monitoring + management** blade, click **See all**.</span></span>

    ![Zobacz wszystkie](./media/cdn-diagnostics-log/15_See-all.png)

4.  <span data-ttu-id="9a5e4-244">Wyszukiwanie CDN hello pola wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="9a5e4-244">Search for CDN in hello search box.</span></span>

    ![Zobacz wszystkie](./media/cdn-diagnostics-log/16_Search-for.png)

5.  <span data-ttu-id="9a5e4-246">Wybierz **usługi Azure CDN podstawowa analiza**.</span><span class="sxs-lookup"><span data-stu-id="9a5e4-246">Select **Azure CDN Core Analytics**.</span></span> 

    ![Zobacz wszystkie](./media/cdn-diagnostics-log/17_Core-analytics.png)

6.  <span data-ttu-id="9a5e4-248">Po kliknięciu przycisku **Utwórz**, będzie zadawane toocreate nowy obszar roboczy OMS lub użyć istniejącego.</span><span class="sxs-lookup"><span data-stu-id="9a5e4-248">After clicking **Create**, you will be asked toocreate a new OMS workspace or use an existing one.</span></span> 

    ![Zobacz wszystkie](./media/cdn-diagnostics-log/18_Adding-solution.png)

7.  <span data-ttu-id="9a5e4-250">Wybierz obszar roboczy hello utworzone przed.</span><span class="sxs-lookup"><span data-stu-id="9a5e4-250">Select hello workspace you created before.</span></span> <span data-ttu-id="9a5e4-251">Następnie należy tooadd konto automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="9a5e4-251">You then need tooadd an automation account.</span></span>

    ![Zobacz wszystkie](./media/cdn-diagnostics-log/19_Add-automation.png)

8. <span data-ttu-id="9a5e4-253">Witaj następujący ekran pokazuje hello formularz konta automatyzacji, który musisz wypełnić.</span><span class="sxs-lookup"><span data-stu-id="9a5e4-253">hello following screen shows hello automation account form you must fill out.</span></span> 

    ![Zobacz wszystkie](./media/cdn-diagnostics-log/20_Automation.png)

9. <span data-ttu-id="9a5e4-255">Po utworzeniu konta automatyzacji hello są gotowe tooadd rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="9a5e4-255">Once you have created hello automation account, you are ready tooadd your solution.</span></span> <span data-ttu-id="9a5e4-256">Kliknij przycisk hello **Utwórz** przycisku.</span><span class="sxs-lookup"><span data-stu-id="9a5e4-256">Click hello **Create** button.</span></span>

    ![Zobacz wszystkie](./media/cdn-diagnostics-log/21_Ready.png)

10. <span data-ttu-id="9a5e4-258">Rozwiązania teraz dodano tooyour obszaru roboczego.</span><span class="sxs-lookup"><span data-stu-id="9a5e4-258">Your solution has now been added tooyour workspace.</span></span> <span data-ttu-id="9a5e4-259">Przejdź wstecz tooyour pulpitu nawigacyjnego portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="9a5e4-259">Go back tooyour Azure portal Dashboard.</span></span>

    ![Zobacz wszystkie](./media/cdn-diagnostics-log/22_Dashboard.png)

    <span data-ttu-id="9a5e4-261">Kliknij obszar roboczy analizy dzienników hello utworzonego obszaru roboczego tooyour toogo.</span><span class="sxs-lookup"><span data-stu-id="9a5e4-261">Click hello Log Analytics workspace you created toogo tooyour workspace.</span></span> 

11. <span data-ttu-id="9a5e4-262">Kliknij przycisk hello **portalu OMS** Kafelek toosee nowe rozwiązania w portalu OMS hello.</span><span class="sxs-lookup"><span data-stu-id="9a5e4-262">Click hello **OMS Portal** tile toosee your new solution in hello OMS portal.</span></span>

    ![Zobacz wszystkie](./media/cdn-diagnostics-log/23_workspace.png)

12. <span data-ttu-id="9a5e4-264">Portalu OMS powinna wyglądać tak jak po ekranie powitania:</span><span class="sxs-lookup"><span data-stu-id="9a5e4-264">Your OMS portal should now look like hello following screen:</span></span>

    ![Zobacz wszystkie](./media/cdn-diagnostics-log/24_OMS-solution.png)

    <span data-ttu-id="9a5e4-266">Kliknij jeden z toosee Kafelki hello kilka widoków danych.</span><span class="sxs-lookup"><span data-stu-id="9a5e4-266">Click one of hello tiles toosee several views into your data.</span></span>

    ![Zobacz wszystkie](./media/cdn-diagnostics-log/25_Interior-view.png)

    <span data-ttu-id="9a5e4-268">Można przewijać w lewej lub prawej toosee dalsze Kafelki reprezentujących poszczególnych widoków na powitania dane.</span><span class="sxs-lookup"><span data-stu-id="9a5e4-268">You can scroll left or right toosee further tiles representing individual views into hello data.</span></span> 

    <span data-ttu-id="9a5e4-269">Kliknij jeden z fragmentów hello zapewnia szczegółowe informacje o danych.</span><span class="sxs-lookup"><span data-stu-id="9a5e4-269">Clicking one of hello tiles gives you more details about your data.</span></span>

     ![Zobacz wszystkie](./media/cdn-diagnostics-log/26_Further-detail.png)

### <a name="offers-and-pricing-tiers"></a><span data-ttu-id="9a5e4-271">Oferty i warstw cenowych</span><span class="sxs-lookup"><span data-stu-id="9a5e4-271">Offers and pricing tiers</span></span>

<span data-ttu-id="9a5e4-272">Możesz wyświetlać oferty i warstw cenowych dla rozwiązań do zarządzania OMS [tutaj](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-add-solutions#offers-and-pricing-tiers).</span><span class="sxs-lookup"><span data-stu-id="9a5e4-272">You can see offers and pricing tiers for OMS management solutions [here](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-add-solutions#offers-and-pricing-tiers).</span></span>

### <a name="customizing-views"></a><span data-ttu-id="9a5e4-273">Dostosowywanie widoków</span><span class="sxs-lookup"><span data-stu-id="9a5e4-273">Customizing views</span></span>

<span data-ttu-id="9a5e4-274">Można dostosować widok hello w dane przy użyciu hello **Widok projektanta**.</span><span class="sxs-lookup"><span data-stu-id="9a5e4-274">You can customize hello view into your data by using hello **View Designer**.</span></span> <span data-ttu-id="9a5e4-275">Przejdź tooyour obszarem roboczym pakietu OMS i rozpoczęciu projektowania, klikając hello **Widok projektanta** kafelka.</span><span class="sxs-lookup"><span data-stu-id="9a5e4-275">Go tooyour OMS workspace and begin designing by clicking hello **View Designer** tile.</span></span>

![Projektant widoków](./media/cdn-diagnostics-log/27_Designer.png)

<span data-ttu-id="9a5e4-277">Można przeciągnij i upuść typów wykresów od lewej hello i wypełnij szczegóły danych hello ma tooanalyze na powitania po lewej.</span><span class="sxs-lookup"><span data-stu-id="9a5e4-277">You can drag and drop types of charts from hello left and fill in hello data details you want tooanalyze on hello left.</span></span>

![Projektant widoków](./media/cdn-diagnostics-log/28_Designer.png)

    
## <a name="log-data-delays"></a><span data-ttu-id="9a5e4-279">Opóźnienia dane dziennika</span><span class="sxs-lookup"><span data-stu-id="9a5e4-279">Log data delays</span></span>

<span data-ttu-id="9a5e4-280">Opóźnienia danych dziennika Verizon</span><span class="sxs-lookup"><span data-stu-id="9a5e4-280">Verizon log data delays</span></span> | <span data-ttu-id="9a5e4-281">Opóźnienia danych dziennika Akamai</span><span class="sxs-lookup"><span data-stu-id="9a5e4-281">Akamai log data delays</span></span>
--- | ---
<span data-ttu-id="9a5e4-282">Dane dziennika Verizon jest opóźnione 1 godzina i podjąć toostart godziny too2 pojawiające się po zakończeniu propagowania punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="9a5e4-282">Verizon log data is 1 hour delayed, and take up too2 hours toostart appearing after endpoint propagation completion.</span></span> | <span data-ttu-id="9a5e4-283">Dane dziennika Akamai wynosi 24 godziny opóźnienie i zajmuje toostart godziny too2 pojawiające się, jeśli został on utworzony więcej niż 24 godziny temu.</span><span class="sxs-lookup"><span data-stu-id="9a5e4-283">Akamai log data is 24 hours delayed, and takes up too2 hours toostart appearing if it was created more than 24 hours ago.</span></span> <span data-ttu-id="9a5e4-284">Jeśli niedawno został utworzony, może potrwać do godziny too25 toostart dzienniki hello znajdujących się.</span><span class="sxs-lookup"><span data-stu-id="9a5e4-284">If it was recently created, it can take up too25 hours for hello logs toostart appearing.</span></span>

## <a name="diagnostic-log-types-for-cdn-core-analytics"></a><span data-ttu-id="9a5e4-285">Typy dzienników diagnostycznych do sieci CDN w warstwie podstawowa analiza</span><span class="sxs-lookup"><span data-stu-id="9a5e4-285">Diagnostic log types for CDN Core Analytics</span></span>

<span data-ttu-id="9a5e4-286">Firma Microsoft oferuje obecnie tylko podstawowa Analiza dzienników zawierających metryki wyświetlane statystki odpowiedzi HTTP i statystyki wyjście widziany z hello CDN POP/krawędzi.</span><span class="sxs-lookup"><span data-stu-id="9a5e4-286">We currently offer only Core Analytics logs, which contain metrics showing HTTP response statistics and egress statistics as seen from hello CDN POPs/edges.</span></span>

### <a name="core-analytics-metrics-details"></a><span data-ttu-id="9a5e4-287">Szczegóły metryki Analytics Core</span><span class="sxs-lookup"><span data-stu-id="9a5e4-287">Core Analytics Metrics Details</span></span>
<span data-ttu-id="9a5e4-288">Hello w poniższej tabeli przedstawiono listę dostępnych w hello podstawowa Analiza dzienników metryk.</span><span class="sxs-lookup"><span data-stu-id="9a5e4-288">hello following table shows a list of metrics available in hello Core Analytics logs.</span></span> <span data-ttu-id="9a5e4-289">Nie wszystkie metryki są dostępne z wszystkich dostawców, choć różnice są minimalne.</span><span class="sxs-lookup"><span data-stu-id="9a5e4-289">Not all metrics are available from all providers, although such differences are minimal.</span></span> <span data-ttu-id="9a5e4-290">Hello również w poniższej tabeli przedstawiono, czy dana metryka jest dostępna od dostawcy.</span><span class="sxs-lookup"><span data-stu-id="9a5e4-290">hello following table also shows if a given metric is available from a provider.</span></span> <span data-ttu-id="9a5e4-291">Należy pamiętać, że metryki hello są dostępne tylko tych punktów końcowych usługi CDN których ruch.</span><span class="sxs-lookup"><span data-stu-id="9a5e4-291">Please note that hello metrics are available for only those CDN endpoints that have traffic on them.</span></span>


|<span data-ttu-id="9a5e4-292">Metryka</span><span class="sxs-lookup"><span data-stu-id="9a5e4-292">Metric</span></span>                     | <span data-ttu-id="9a5e4-293">Opis</span><span class="sxs-lookup"><span data-stu-id="9a5e4-293">Description</span></span>   | <span data-ttu-id="9a5e4-294">Verizon</span><span class="sxs-lookup"><span data-stu-id="9a5e4-294">Verizon</span></span>  | <span data-ttu-id="9a5e4-295">Akamai</span><span class="sxs-lookup"><span data-stu-id="9a5e4-295">Akamai</span></span> 
|---------------------------|---------------|---|---|
| <span data-ttu-id="9a5e4-296">RequestCountTotal</span><span class="sxs-lookup"><span data-stu-id="9a5e4-296">RequestCountTotal</span></span>         |<span data-ttu-id="9a5e4-297">Całkowita liczba trafień żądania podczas tego okresu.</span><span class="sxs-lookup"><span data-stu-id="9a5e4-297">Total number of request hits during this period</span></span>| <span data-ttu-id="9a5e4-298">Tak</span><span class="sxs-lookup"><span data-stu-id="9a5e4-298">Yes</span></span>  |<span data-ttu-id="9a5e4-299">Tak</span><span class="sxs-lookup"><span data-stu-id="9a5e4-299">Yes</span></span>   |
| <span data-ttu-id="9a5e4-300">RequestCountHttpStatus2xx</span><span class="sxs-lookup"><span data-stu-id="9a5e4-300">RequestCountHttpStatus2xx</span></span> |<span data-ttu-id="9a5e4-301">Liczba wszystkich żądań, które wywołały kod HTTP 2xx (200, 202)</span><span class="sxs-lookup"><span data-stu-id="9a5e4-301">Count of all requests that resulted in a 2xx HTTP code (e.g. 200, 202)</span></span>              | <span data-ttu-id="9a5e4-302">Tak</span><span class="sxs-lookup"><span data-stu-id="9a5e4-302">Yes</span></span>  |<span data-ttu-id="9a5e4-303">Tak</span><span class="sxs-lookup"><span data-stu-id="9a5e4-303">Yes</span></span>   |
| <span data-ttu-id="9a5e4-304">RequestCountHttpStatus3xx</span><span class="sxs-lookup"><span data-stu-id="9a5e4-304">RequestCountHttpStatus3xx</span></span> | <span data-ttu-id="9a5e4-305">Liczba wszystkich żądań, które wywołały kod HTTP 3xx (np. 300, 302)</span><span class="sxs-lookup"><span data-stu-id="9a5e4-305">Count of all requests that resulted in a 3xx HTTP code (e.g. 300, 302)</span></span>              | <span data-ttu-id="9a5e4-306">Tak</span><span class="sxs-lookup"><span data-stu-id="9a5e4-306">Yes</span></span>  |<span data-ttu-id="9a5e4-307">Tak</span><span class="sxs-lookup"><span data-stu-id="9a5e4-307">Yes</span></span>   |
| <span data-ttu-id="9a5e4-308">RequestCountHttpStatus4xx</span><span class="sxs-lookup"><span data-stu-id="9a5e4-308">RequestCountHttpStatus4xx</span></span> |<span data-ttu-id="9a5e4-309">Liczba wszystkich żądań, które wywołały kod HTTP 4xx (np. 400, 404)</span><span class="sxs-lookup"><span data-stu-id="9a5e4-309">Count of all requests that resulted in a 4xx HTTP code (e.g. 400, 404)</span></span>               | <span data-ttu-id="9a5e4-310">Tak</span><span class="sxs-lookup"><span data-stu-id="9a5e4-310">Yes</span></span>   |<span data-ttu-id="9a5e4-311">Tak</span><span class="sxs-lookup"><span data-stu-id="9a5e4-311">Yes</span></span>   |
| <span data-ttu-id="9a5e4-312">RequestCountHttpStatus5xx</span><span class="sxs-lookup"><span data-stu-id="9a5e4-312">RequestCountHttpStatus5xx</span></span> | <span data-ttu-id="9a5e4-313">Liczba wszystkich żądań, które wywołały kod HTTP 5xx (np. 500, 504)</span><span class="sxs-lookup"><span data-stu-id="9a5e4-313">Count of all requests that resulted in a 5xx HTTP code (e.g. 500, 504)</span></span>              | <span data-ttu-id="9a5e4-314">Tak</span><span class="sxs-lookup"><span data-stu-id="9a5e4-314">Yes</span></span>  |<span data-ttu-id="9a5e4-315">Tak</span><span class="sxs-lookup"><span data-stu-id="9a5e4-315">Yes</span></span>   |
| <span data-ttu-id="9a5e4-316">RequestCountHttpStatusOthers</span><span class="sxs-lookup"><span data-stu-id="9a5e4-316">RequestCountHttpStatusOthers</span></span> |  <span data-ttu-id="9a5e4-317">Liczba innych kodów HTTP (poza 2xx 5xx)</span><span class="sxs-lookup"><span data-stu-id="9a5e4-317">Count of all other HTTP codes (outside of 2xx-5xx)</span></span> | <span data-ttu-id="9a5e4-318">Tak</span><span class="sxs-lookup"><span data-stu-id="9a5e4-318">Yes</span></span>  |<span data-ttu-id="9a5e4-319">Tak</span><span class="sxs-lookup"><span data-stu-id="9a5e4-319">Yes</span></span>   |
| <span data-ttu-id="9a5e4-320">RequestCountHttpStatus200</span><span class="sxs-lookup"><span data-stu-id="9a5e4-320">RequestCountHttpStatus200</span></span> | <span data-ttu-id="9a5e4-321">Liczba wszystkich żądań, które spowodowało 200 kod odpowiedzi HTTP</span><span class="sxs-lookup"><span data-stu-id="9a5e4-321">Count of all requests that resulted in a 200 HTTP code response</span></span>              |<span data-ttu-id="9a5e4-322">Nie</span><span class="sxs-lookup"><span data-stu-id="9a5e4-322">No</span></span>   |<span data-ttu-id="9a5e4-323">Tak</span><span class="sxs-lookup"><span data-stu-id="9a5e4-323">Yes</span></span>   |
| <span data-ttu-id="9a5e4-324">RequestCountHttpStatus206</span><span class="sxs-lookup"><span data-stu-id="9a5e4-324">RequestCountHttpStatus206</span></span> | <span data-ttu-id="9a5e4-325">Liczba wszystkich żądań, które wywołały kod odpowiedź HTTP 206</span><span class="sxs-lookup"><span data-stu-id="9a5e4-325">Count of all requests that resulted in a 206 HTTP code response</span></span>              |<span data-ttu-id="9a5e4-326">Nie</span><span class="sxs-lookup"><span data-stu-id="9a5e4-326">No</span></span>   |<span data-ttu-id="9a5e4-327">Tak</span><span class="sxs-lookup"><span data-stu-id="9a5e4-327">Yes</span></span>   |
| <span data-ttu-id="9a5e4-328">RequestCountHttpStatus302</span><span class="sxs-lookup"><span data-stu-id="9a5e4-328">RequestCountHttpStatus302</span></span> | <span data-ttu-id="9a5e4-329">Liczba wszystkich żądań, które spowodowało 302 kod odpowiedzi HTTP</span><span class="sxs-lookup"><span data-stu-id="9a5e4-329">Count of all requests that resulted in a 302 HTTP code response</span></span>              |<span data-ttu-id="9a5e4-330">Nie</span><span class="sxs-lookup"><span data-stu-id="9a5e4-330">No</span></span>   |<span data-ttu-id="9a5e4-331">Tak</span><span class="sxs-lookup"><span data-stu-id="9a5e4-331">Yes</span></span>   |
| <span data-ttu-id="9a5e4-332">RequestCountHttpStatus304</span><span class="sxs-lookup"><span data-stu-id="9a5e4-332">RequestCountHttpStatus304</span></span> |  <span data-ttu-id="9a5e4-333">Liczba wszystkich żądań, które zakończyły się odpowiedź 304 kodu HTTP</span><span class="sxs-lookup"><span data-stu-id="9a5e4-333">Count of all requests that resulted in a 304 HTTP code response</span></span>             |<span data-ttu-id="9a5e4-334">Nie</span><span class="sxs-lookup"><span data-stu-id="9a5e4-334">No</span></span>   |<span data-ttu-id="9a5e4-335">Tak</span><span class="sxs-lookup"><span data-stu-id="9a5e4-335">Yes</span></span>   |
| <span data-ttu-id="9a5e4-336">RequestCountHttpStatus404</span><span class="sxs-lookup"><span data-stu-id="9a5e4-336">RequestCountHttpStatus404</span></span> | <span data-ttu-id="9a5e4-337">Liczba wszystkich żądań, które wywołały kod odpowiedzi HTTP 404</span><span class="sxs-lookup"><span data-stu-id="9a5e4-337">Count of all requests that resulted in a 404 HTTP code response</span></span>              |<span data-ttu-id="9a5e4-338">Nie</span><span class="sxs-lookup"><span data-stu-id="9a5e4-338">No</span></span>   |<span data-ttu-id="9a5e4-339">Tak</span><span class="sxs-lookup"><span data-stu-id="9a5e4-339">Yes</span></span>   |
| <span data-ttu-id="9a5e4-340">RequestCountCacheHit</span><span class="sxs-lookup"><span data-stu-id="9a5e4-340">RequestCountCacheHit</span></span> |<span data-ttu-id="9a5e4-341">Liczba wszystkich żądań, które zakończyły się liczby trafień pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="9a5e4-341">Count of all requests that resulted in a Cache Hit.</span></span> <span data-ttu-id="9a5e4-342">Oznacza to, że zasobów hello zostało obsłużone bezpośrednio z toohello POP powitania klienta.</span><span class="sxs-lookup"><span data-stu-id="9a5e4-342">This means hello asset was served directly from hello POP toohello Client.</span></span>               | <span data-ttu-id="9a5e4-343">Tak</span><span class="sxs-lookup"><span data-stu-id="9a5e4-343">Yes</span></span>  |<span data-ttu-id="9a5e4-344">Nie</span><span class="sxs-lookup"><span data-stu-id="9a5e4-344">No</span></span>   |
| <span data-ttu-id="9a5e4-345">RequestCountCacheMiss</span><span class="sxs-lookup"><span data-stu-id="9a5e4-345">RequestCountCacheMiss</span></span> | <span data-ttu-id="9a5e4-346">Liczba wszystkich żądań, które spowodowało w Chybienie pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="9a5e4-346">Count of all requests that resulted in a Cache Miss.</span></span> <span data-ttu-id="9a5e4-347">Oznacza to hello zasobów nie został znaleziony na powitania POP najbliższego toohello klienta i w związku z tym nie została pobrana z hello pochodzenia.</span><span class="sxs-lookup"><span data-stu-id="9a5e4-347">This means hello asset was not found on hello POP closest toohello client, and therefore was retrieved from hello Origin.</span></span>              |<span data-ttu-id="9a5e4-348">Tak</span><span class="sxs-lookup"><span data-stu-id="9a5e4-348">Yes</span></span>   | <span data-ttu-id="9a5e4-349">Nie</span><span class="sxs-lookup"><span data-stu-id="9a5e4-349">No</span></span>  |
| <span data-ttu-id="9a5e4-350">RequestCountCacheNoCache</span><span class="sxs-lookup"><span data-stu-id="9a5e4-350">RequestCountCacheNoCache</span></span> | <span data-ttu-id="9a5e4-351">Liczba wszystkich żądań zawartości tooan, który uniemożliwił pamięci podręcznej ukończenia konfiguracji użytkownika tooa na powitania krawędzi.</span><span class="sxs-lookup"><span data-stu-id="9a5e4-351">Count of all requests tooan asset that are prevented from being cached due tooa user configuration on hello edge.</span></span>              |<span data-ttu-id="9a5e4-352">Tak</span><span class="sxs-lookup"><span data-stu-id="9a5e4-352">Yes</span></span>   | <span data-ttu-id="9a5e4-353">Nie</span><span class="sxs-lookup"><span data-stu-id="9a5e4-353">No</span></span>  |
| <span data-ttu-id="9a5e4-354">RequestCountCacheUncacheable</span><span class="sxs-lookup"><span data-stu-id="9a5e4-354">RequestCountCacheUncacheable</span></span> | <span data-ttu-id="9a5e4-355">Liczba wszystkich żądań tooassets, który uniemożliwił buforowana przez zasobów hello Cache-Control i wygasa nagłówki, które wskazują, że go mają nie być buforowane punktu obecności lub przez klienta na powitania HTTP</span><span class="sxs-lookup"><span data-stu-id="9a5e4-355">Count of all requests tooassets that are prevented from being cached by hello asset's Cache-Control and Expires headers, which indicate that it should not be cached on a POP or by hello HTTP client</span></span>                |<span data-ttu-id="9a5e4-356">Tak</span><span class="sxs-lookup"><span data-stu-id="9a5e4-356">Yes</span></span>   |<span data-ttu-id="9a5e4-357">Nie</span><span class="sxs-lookup"><span data-stu-id="9a5e4-357">No</span></span>   |
| <span data-ttu-id="9a5e4-358">RequestCountCacheOthers</span><span class="sxs-lookup"><span data-stu-id="9a5e4-358">RequestCountCacheOthers</span></span> | <span data-ttu-id="9a5e4-359">Liczba wszystkich żądań o stanie pamięci podręcznej nie jest objęty przez powyżej.</span><span class="sxs-lookup"><span data-stu-id="9a5e4-359">Count of all requests with cache status not covered by above.</span></span>              |<span data-ttu-id="9a5e4-360">Tak</span><span class="sxs-lookup"><span data-stu-id="9a5e4-360">Yes</span></span>   | <span data-ttu-id="9a5e4-361">Nie</span><span class="sxs-lookup"><span data-stu-id="9a5e4-361">No</span></span>  |
| <span data-ttu-id="9a5e4-362">EgressTotal</span><span class="sxs-lookup"><span data-stu-id="9a5e4-362">EgressTotal</span></span> | <span data-ttu-id="9a5e4-363">Transfer danych wychodzących w GB</span><span class="sxs-lookup"><span data-stu-id="9a5e4-363">Outbound data transfer in GB</span></span>              |<span data-ttu-id="9a5e4-364">Tak</span><span class="sxs-lookup"><span data-stu-id="9a5e4-364">Yes</span></span>   |<span data-ttu-id="9a5e4-365">Tak</span><span class="sxs-lookup"><span data-stu-id="9a5e4-365">Yes</span></span>   |
| <span data-ttu-id="9a5e4-366">EgressHttpStatus2xx</span><span class="sxs-lookup"><span data-stu-id="9a5e4-366">EgressHttpStatus2xx</span></span> | <span data-ttu-id="9a5e4-367">Danych wychodzących transfer * odpowiedzi z kodów stanu HTTP 2xx w GB</span><span class="sxs-lookup"><span data-stu-id="9a5e4-367">Outbound data transfer* for responses with 2xx HTTP status codes in GB</span></span>            |<span data-ttu-id="9a5e4-368">Tak</span><span class="sxs-lookup"><span data-stu-id="9a5e4-368">Yes</span></span>   |<span data-ttu-id="9a5e4-369">Nie</span><span class="sxs-lookup"><span data-stu-id="9a5e4-369">No</span></span>   |
| <span data-ttu-id="9a5e4-370">EgressHttpStatus3xx</span><span class="sxs-lookup"><span data-stu-id="9a5e4-370">EgressHttpStatus3xx</span></span> | <span data-ttu-id="9a5e4-371">Transfer danych wychodzących dla odpowiedzi z kodów stanu HTTP 3xx w GB</span><span class="sxs-lookup"><span data-stu-id="9a5e4-371">Outbound data transfer for responses with 3xx HTTP status codes in GB</span></span>              |<span data-ttu-id="9a5e4-372">Tak</span><span class="sxs-lookup"><span data-stu-id="9a5e4-372">Yes</span></span>   |<span data-ttu-id="9a5e4-373">Nie</span><span class="sxs-lookup"><span data-stu-id="9a5e4-373">No</span></span>   |
| <span data-ttu-id="9a5e4-374">EgressHttpStatus4xx</span><span class="sxs-lookup"><span data-stu-id="9a5e4-374">EgressHttpStatus4xx</span></span> | <span data-ttu-id="9a5e4-375">Transfer danych wychodzących dla odpowiedzi z kodów stanu HTTP 4xx w GB</span><span class="sxs-lookup"><span data-stu-id="9a5e4-375">Outbound data transfer for responses with 4xx HTTP status codes in GB</span></span>               |<span data-ttu-id="9a5e4-376">Tak</span><span class="sxs-lookup"><span data-stu-id="9a5e4-376">Yes</span></span>   | <span data-ttu-id="9a5e4-377">Nie</span><span class="sxs-lookup"><span data-stu-id="9a5e4-377">No</span></span>  |
| <span data-ttu-id="9a5e4-378">EgressHttpStatus5xx</span><span class="sxs-lookup"><span data-stu-id="9a5e4-378">EgressHttpStatus5xx</span></span> | <span data-ttu-id="9a5e4-379">Transfer danych wychodzących dla odpowiedzi z kodów stanu HTTP 5xx w GB</span><span class="sxs-lookup"><span data-stu-id="9a5e4-379">Outbound data transfer for responses with 5xx HTTP status codes in GB</span></span>               |<span data-ttu-id="9a5e4-380">Tak</span><span class="sxs-lookup"><span data-stu-id="9a5e4-380">Yes</span></span>   |  <span data-ttu-id="9a5e4-381">Nie</span><span class="sxs-lookup"><span data-stu-id="9a5e4-381">No</span></span> |
| <span data-ttu-id="9a5e4-382">EgressHttpStatusOthers</span><span class="sxs-lookup"><span data-stu-id="9a5e4-382">EgressHttpStatusOthers</span></span> | <span data-ttu-id="9a5e4-383">Transfer danych wychodzących dla odpowiedzi o innych kodach stanów HTTP w GB</span><span class="sxs-lookup"><span data-stu-id="9a5e4-383">Outbound data transfer for responses with other HTTP status codes in GB</span></span>                |<span data-ttu-id="9a5e4-384">Tak</span><span class="sxs-lookup"><span data-stu-id="9a5e4-384">Yes</span></span>   |<span data-ttu-id="9a5e4-385">Nie</span><span class="sxs-lookup"><span data-stu-id="9a5e4-385">No</span></span>   |
| <span data-ttu-id="9a5e4-386">EgressCacheHit</span><span class="sxs-lookup"><span data-stu-id="9a5e4-386">EgressCacheHit</span></span> |  <span data-ttu-id="9a5e4-387">Transfer danych wychodzących dla odpowiedzi, które zostały dostarczone bezpośrednio z pamięci podręcznej CDN hello na powitania CDN POP/krawędzi</span><span class="sxs-lookup"><span data-stu-id="9a5e4-387">Outbound data transfer for responses that were delivered directly from hello CDN cache on hello CDN POPs/Edges</span></span>  |<span data-ttu-id="9a5e4-388">Tak</span><span class="sxs-lookup"><span data-stu-id="9a5e4-388">Yes</span></span>   |  <span data-ttu-id="9a5e4-389">Nie</span><span class="sxs-lookup"><span data-stu-id="9a5e4-389">No</span></span> |
| <span data-ttu-id="9a5e4-390">EgressCacheMiss</span><span class="sxs-lookup"><span data-stu-id="9a5e4-390">EgressCacheMiss</span></span> | <span data-ttu-id="9a5e4-391">Transfer danych wychodzących dla odpowiedzi, które nie zostały znalezione na powitania najbliższy serwer protokołu POP i pobierane z serwera źródłowego hello</span><span class="sxs-lookup"><span data-stu-id="9a5e4-391">Outbound data transfer for responses that were not found on hello nearest POP server, and retrieved from hello origin server</span></span>              |<span data-ttu-id="9a5e4-392">Tak</span><span class="sxs-lookup"><span data-stu-id="9a5e4-392">Yes</span></span>   |  <span data-ttu-id="9a5e4-393">Nie</span><span class="sxs-lookup"><span data-stu-id="9a5e4-393">No</span></span> |
| <span data-ttu-id="9a5e4-394">EgressCacheNoCache</span><span class="sxs-lookup"><span data-stu-id="9a5e4-394">EgressCacheNoCache</span></span> | <span data-ttu-id="9a5e4-395">Transfer danych wychodzących dla zasobów, które nie będą mogli pamięci podręcznej ukończenia konfiguracji użytkownika tooa na powitania krawędzi.</span><span class="sxs-lookup"><span data-stu-id="9a5e4-395">Outbound data transfer for assets that are prevented from being cached due tooa user configuration on hello edge.</span></span>                |<span data-ttu-id="9a5e4-396">Tak</span><span class="sxs-lookup"><span data-stu-id="9a5e4-396">Yes</span></span>   |<span data-ttu-id="9a5e4-397">Nie</span><span class="sxs-lookup"><span data-stu-id="9a5e4-397">No</span></span>   |
| <span data-ttu-id="9a5e4-398">EgressCacheUncacheable</span><span class="sxs-lookup"><span data-stu-id="9a5e4-398">EgressCacheUncacheable</span></span> | <span data-ttu-id="9a5e4-399">Transfer danych wychodzących dla zasobów, które uniemożliwiały buforowana przez Cache-Control hello zasobów i/lub Expires nagłówków, wskazujące, że go mają nie być buforowane punktu obecności lub przez klienta na powitania HTTP</span><span class="sxs-lookup"><span data-stu-id="9a5e4-399">Outbound data transfer for assets that are prevented from being cached by hello asset's Cache-Control and/or Expires headers, which indicate that it should not be cached on a POP or by hello HTTP client</span></span>                    |<span data-ttu-id="9a5e4-400">Tak</span><span class="sxs-lookup"><span data-stu-id="9a5e4-400">Yes</span></span>   | <span data-ttu-id="9a5e4-401">Nie</span><span class="sxs-lookup"><span data-stu-id="9a5e4-401">No</span></span>  |
| <span data-ttu-id="9a5e4-402">EgressCacheOthers</span><span class="sxs-lookup"><span data-stu-id="9a5e4-402">EgressCacheOthers</span></span> |  <span data-ttu-id="9a5e4-403">Transfery danych wychodzących w innych sytuacjach pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="9a5e4-403">Outbound data transfers for other cache scenarios.</span></span>             |<span data-ttu-id="9a5e4-404">Tak</span><span class="sxs-lookup"><span data-stu-id="9a5e4-404">Yes</span></span>   | <span data-ttu-id="9a5e4-405">Nie</span><span class="sxs-lookup"><span data-stu-id="9a5e4-405">No</span></span>  |

<span data-ttu-id="9a5e4-406">* Transfer danych wychodzących odwołuje się tootraffic dostarczone z klienta toohello serwerów POP w sieci CDN.</span><span class="sxs-lookup"><span data-stu-id="9a5e4-406">*Outbound data transfer refers tootraffic delivered from CDN POP servers toohello client.</span></span>


### <a name="schema-of-hello-core-analytics-logs"></a><span data-ttu-id="9a5e4-407">Schemat hello Core analizy dzienników</span><span class="sxs-lookup"><span data-stu-id="9a5e4-407">Schema of hello Core Analytics Logs</span></span> 

<span data-ttu-id="9a5e4-408">Wszystkie dzienniki są przechowywane w formacie JSON i każdy wpis ma pól ciągów po hello poniżej schematu:</span><span class="sxs-lookup"><span data-stu-id="9a5e4-408">All logs are stored in JSON format and each entry has string fields following hello below schema:</span></span>

```json
    "records": [
        {
            "time": "2017-04-27T01:00:00",
            "resourceId": "<ARM Resource Id of hello CDN Endpoint>",
            "operationName": "Microsoft.Cdn/profiles/endpoints/contentDelivery",
            "category": "CoreAnalytics",
            "properties": {
                "DomainName": "<Name of hello domain for which hello statistics is reported>",
                "RequestCountTotal": integer value,
                "RequestCountHttpStatus2xx": integer value,
                "RequestCountHttpStatus3xx": integer value,
                "RequestCountHttpStatus4xx": integer value,
                "RequestCountHttpStatus5xx": integer value,
                "RequestCountHttpStatusOthers": integer value,
                "RequestCountHttpStatus200": integer value,
                "RequestCountHttpStatus206": integer value,
                "RequestCountHttpStatus302": integer value,
                "RequestCountHttpStatus304": integer value,
                "RequestCountHttpStatus404": integer value,
                "RequestCountCacheHit": integer value,
                "RequestCountCacheMiss": integer value,
                "RequestCountCacheNoCache": integer value,
                "RequestCountCacheUncacheable": integer value,
                "RequestCountCacheOthers": integer value,
                "EgressTotal": double value,
                "EgressHttpStatus2xx": double value,
                "EgressHttpStatus3xx": double value,
                "EgressHttpStatus4xx": double value,
                "EgressHttpStatus5xx": double value,
                "EgressHttpStatusOthers": double value,
                "EgressCacheHit": double value,
                "EgressCacheMiss": double value,
                "EgressCacheNoCache": double value,
                "EgressCacheUncacheable": double value,
                "EgressCacheOthers": double value,
            }
        }

    ]
}
```

<span data-ttu-id="9a5e4-409">Gdy czas"hello" reprezentuje czas rozpoczęcia hello hello godzina granic, dla którego jest raportowane dane statystyczne hello.</span><span class="sxs-lookup"><span data-stu-id="9a5e4-409">Where hello ‘time’ represents hello start time of hello hour boundary for which hello statistics is reported.</span></span> <span data-ttu-id="9a5e4-410">Gdy metryki nie jest obsługiwany przez dostawcę sieci CDN w warstwie, a nie wartość o podwójnej precyzji lub liczba całkowita będzie być wartość null.</span><span class="sxs-lookup"><span data-stu-id="9a5e4-410">When a metric is not supported by a CDN provider, instead of a double or integer value, there will be a null value.</span></span> <span data-ttu-id="9a5e4-411">Ta wartość null oznacza braku hello metryki i to różni się od wartości 0.</span><span class="sxs-lookup"><span data-stu-id="9a5e4-411">This null value indicates hello absence of a metric, and this is different from a 0 value.</span></span> <span data-ttu-id="9a5e4-412">Należy również zauważyć, że będą istnieć jeden zestaw te metryki dla domeny skonfigurowany w punkcie końcowym hello.</span><span class="sxs-lookup"><span data-stu-id="9a5e4-412">Also note that there will be one set of these metrics per domain configured on hello endpoint.</span></span>

<span data-ttu-id="9a5e4-413">Właściwości przykładzie poniżej:</span><span class="sxs-lookup"><span data-stu-id="9a5e4-413">Example properties below:</span></span>

```json
{
     "DomainName": "manlingakamaitest2.azureedge.net",
     "RequestCountTotal": 480,
     "RequestCountHttpStatus2xx": 480,
     "RequestCountHttpStatus3xx": 0,
     "RequestCountHttpStatus4xx": 0,
     "RequestCountHttpStatus5xx": 0,
     "RequestCountHttpStatusOthers": 0,
     "RequestCountHttpStatus200": 480,
     "RequestCountHttpStatus206": 0,
     "RequestCountHttpStatus302": 0,
     "RequestCountHttpStatus304": 0,
     "RequestCountHttpStatus404": 0,
     "RequestCountCacheHit": null,
     "RequestCountCacheMiss": null,
     "RequestCountCacheNoCache": null,
     "RequestCountCacheUncacheable": null,
     "RequestCountCacheOthers": null,
     "EgressTotal": 0.09,
     "EgressHttpStatus2xx": null,
     "EgressHttpStatus3xx": null,
     "EgressHttpStatus4xx": null,
     "EgressHttpStatus5xx": null,
     "EgressHttpStatusOthers": null,
     "EgressCacheHit": null,
     "EgressCacheMiss": null,
     "EgressCacheNoCache": null,
     "EgressCacheUncacheable": null,
     "EgressCacheOthers": null
}

```

## <a name="additional-resources"></a><span data-ttu-id="9a5e4-414">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="9a5e4-414">Additional resources</span></span>

* [<span data-ttu-id="9a5e4-415">Dzienniki diagnostyczne platformy Azure</span><span class="sxs-lookup"><span data-stu-id="9a5e4-415">Azure Diagnostic logs</span></span>](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs)
* [<span data-ttu-id="9a5e4-416">Podstawowa analiza uzupełniające portalu usługi Azure CDN</span><span class="sxs-lookup"><span data-stu-id="9a5e4-416">Core analytics via Azure CDN supplemental portal</span></span>](https://docs.microsoft.com/azure/cdn/cdn-analyze-usage-patterns)
* [<span data-ttu-id="9a5e4-417">Analiza dzienników Azure OMS</span><span class="sxs-lookup"><span data-stu-id="9a5e4-417">Azure OMS Log Analytics</span></span>](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-overview)
* [<span data-ttu-id="9a5e4-418">Analiza dzienników Azure interfejsu API REST</span><span class="sxs-lookup"><span data-stu-id="9a5e4-418">Azure Log Analytics REST API</span></span>](https://docs.microsoft.com/en-us/rest/api/loganalytics)







