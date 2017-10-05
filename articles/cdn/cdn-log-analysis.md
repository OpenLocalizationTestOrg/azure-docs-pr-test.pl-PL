---
title: "Zaloguj się do usługi Azure CDN analizy | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 03ff74ae4e40d3f2279caaf4f73e9b4aac6a2ebb
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="diagnostics-logs-for-azure-cdn"></a><span data-ttu-id="e353c-103">Dzienniki diagnostyczne dla usługi Azure CDN</span><span class="sxs-lookup"><span data-stu-id="e353c-103">Diagnostics Logs for Azure CDN</span></span>

<span data-ttu-id="e353c-104">Po włączeniu sieci CDN w warstwie aplikacji, prawdopodobnie należy do monitorowania użycia sieci CDN w warstwie, Sprawdź kondycję firmy i rozwiązywania potencjalnych problemów.</span><span class="sxs-lookup"><span data-stu-id="e353c-104">After enabling CDN for your application, you will likely want to monitor the CDN usage, check the health of your delivery, and troubleshoot potential issues.</span></span> <span data-ttu-id="e353c-105">Usługi Azure CDN zapewnia dodatkowe możliwości z [sieci CDN w warstwie podstawowa analiza](cdn-analyze-usage-patterns.md) i [dzienników diagnostycznych](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs)</span><span class="sxs-lookup"><span data-stu-id="e353c-105">Azure CDN provides these capabilities with [CDN Core Analytics](cdn-analyze-usage-patterns.md) and [Diagnostic Logs](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs)</span></span>

## <a name="cdn-core-analytics"></a><span data-ttu-id="e353c-106">Sieci CDN w warstwie podstawowa analiza</span><span class="sxs-lookup"><span data-stu-id="e353c-106">CDN Core Analytics</span></span>
<span data-ttu-id="e353c-107">Bieżący użytkownik usługi Azure CDN z Verizon standardowa lub premium profilu masz już możliwość wyświetlania core analytics w portalu uzupełniającym dostępny przy użyciu opcji "Manage" z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="e353c-107">As a current Azure CDN user with Verizon standard or premium profile, you are already able to view core analytics in the supplemental portal accessible via the "Manage" option from the Azure portal.</span></span> 

## <a name="azure-diagnostic-logs"></a><span data-ttu-id="e353c-108">Dzienniki diagnostyczne platformy Azure</span><span class="sxs-lookup"><span data-stu-id="e353c-108">Azure Diagnostic Logs</span></span>

<span data-ttu-id="e353c-109">Azure przy użyciu tej nowej funkcji, można teraz wyświetlić podstawowa analiza i zapisać je w co najmniej jednego miejsca docelowe, w tym:</span><span class="sxs-lookup"><span data-stu-id="e353c-109">Azure With this new feature, you can now view core analytics and save them into one or more destinations including:</span></span>

 - <span data-ttu-id="e353c-110">Konto usługi Azure Storage</span><span class="sxs-lookup"><span data-stu-id="e353c-110">Azure Storage account</span></span>
 - <span data-ttu-id="e353c-111">Azure Event Hubs</span><span class="sxs-lookup"><span data-stu-id="e353c-111">Azure Event Hubs</span></span>
 - [<span data-ttu-id="e353c-112">Repozytorium OMS analizy dzienników</span><span class="sxs-lookup"><span data-stu-id="e353c-112">OMS Log Analytics repository</span></span>](https://docs.microsoft.com/azure/log-analytics/log-analytics-get-started)
 
 <span data-ttu-id="e353c-113">Ta funkcja jest dostępna dla wszystkich punktów końcowych usługi CDN Verizon (Standard i Premium) oraz profilów usługi CDN Akamai (Standard).</span><span class="sxs-lookup"><span data-stu-id="e353c-113">This feature is available for all CDN endpoints belonging to Verizon (Standard & Premium) and Akamai (Standard) CDN Profiles.</span></span>

<span data-ttu-id="e353c-114">Dzienniki diagnostyczne umożliwiają eksportowania metryki użycia podstawowe z punktu końcowego CDN do różnych źródeł, dzięki czemu będzie można korzystać dostosowany sposób.</span><span class="sxs-lookup"><span data-stu-id="e353c-114">Diagnostics logs allow you to export basic usage metrics from your CDN endpoint to a variety of sources so that you can consume them in a customized way.</span></span> <span data-ttu-id="e353c-115">Na przykład można wykonać następujące typy eksportu danych:</span><span class="sxs-lookup"><span data-stu-id="e353c-115">For example, you can do the following types of data export:</span></span>

- <span data-ttu-id="e353c-116">Eksportuj dane do magazynu obiektów blob, Eksportuj do pliku CSV i Generowanie wykresów w formacie programu excel.</span><span class="sxs-lookup"><span data-stu-id="e353c-116">Export data to blob storage, export to CSV, and generate graphs in excel.</span></span>
- <span data-ttu-id="e353c-117">Eksportuj dane do usługi event hubs i skorelowania danych z innymi usługami azure.</span><span class="sxs-lookup"><span data-stu-id="e353c-117">Export data to event hubs and correlate with data from other azure services.</span></span>
- <span data-ttu-id="e353c-118">Eksportuj dane do dziennika analizy i wyświetlania danych w własne obszar roboczy OMS</span><span class="sxs-lookup"><span data-stu-id="e353c-118">Export data to log analytics and view data in your own OMS work space</span></span>

<span data-ttu-id="e353c-119">Na poniższej ilustracji przedstawiono typowe przeglądanie sieci CDN w warstwie podstawowa analiza danych.</span><span class="sxs-lookup"><span data-stu-id="e353c-119">The following figure shows a typical CDN Core Analytics view into data.</span></span>

![Portal — dzienniki diagnostyczne](./media/cdn-diagnostics-log/01_OMS-workspace.png)

<span data-ttu-id="e353c-121">*Rysunek 1 — widok sieci CDN w warstwie podstawowa analiza*</span><span class="sxs-lookup"><span data-stu-id="e353c-121">*Figure 1 - CDN Core Analytics view*</span></span>

<span data-ttu-id="e353c-122">Poniższe wskazówki przechodzi przez schemat core analizy danych, etapy włączenie funkcji oraz dostarczania ich do różnych miejsc docelowych i korzystanie z tych miejsc docelowych.</span><span class="sxs-lookup"><span data-stu-id="e353c-122">The following walkthrough goes through the schema of the core analytics data, steps involved in enabling the feature and delivering them to various destinations, and consuming from these destinations.</span></span>

## <a name="enable-logging-with-azure-portal"></a><span data-ttu-id="e353c-123">Włącz rejestrowanie z portalu Azure</span><span class="sxs-lookup"><span data-stu-id="e353c-123">Enable logging with Azure portal</span></span>

> [!NOTE]
> <span data-ttu-id="e353c-124">Dzienniki diagnostyczne są włączane **poza** domyślnie.</span><span class="sxs-lookup"><span data-stu-id="e353c-124">The diagnostics logs are turned **off** by default.</span></span> 

<span data-ttu-id="e353c-125">Wykonaj poniższe kroki, aby włączyć rejestrowanie z sieci CDN w warstwie podstawowa analiza:</span><span class="sxs-lookup"><span data-stu-id="e353c-125">Follow the steps below to enable logging with CDN Core Analytics:</span></span>

<span data-ttu-id="e353c-126">Zaloguj się w witrynie [Azure Portal](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e353c-126">Sign in to the [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="e353c-127">Jeśli nie masz już włączone dla przepływu pracy, w sieci CDN [włączyć usługi Azure CDN](cdn-create-new-endpoint.md) przed kontynuowaniem.</span><span class="sxs-lookup"><span data-stu-id="e353c-127">If you don't already have CDN enabled for your workflow, [Enable Azure CDN](cdn-create-new-endpoint.md) before you continue.</span></span>

1. <span data-ttu-id="e353c-128">W portalu, przejdź do **profilu CDN**.</span><span class="sxs-lookup"><span data-stu-id="e353c-128">In the portal, navigate to **CDN profile**.</span></span>
2. <span data-ttu-id="e353c-129">Wybierz profil CDN, a następnie wybierz punkt końcowy CDN, który chcesz włączyć **dzienników diagnostycznych**.</span><span class="sxs-lookup"><span data-stu-id="e353c-129">Select a CDN profile, then select the CDN endpoint that you want to enable **Diagnostics Logs**.</span></span>

    ![Portal — dzienniki diagnostyczne](./media/cdn-diagnostics-log/02_Browse-to-Diagnostics-logs.png)

3. <span data-ttu-id="e353c-131">Przejdź do **dzienników diagnostycznych** bloku w obszarze **monitorowanie** sekcji, a następnie zmień stan **na**.</span><span class="sxs-lookup"><span data-stu-id="e353c-131">Go to **Diagnostics Logs** blade Under **Monitoring** section, then change the status to **On**.</span></span>

    ![Portal — dzienniki diagnostyczne](./media/cdn-diagnostics-log/03_Diagnostics-logs-options.png)

### <a name="enable-logging-with-azure-storage"></a><span data-ttu-id="e353c-133">Włącz rejestrowanie z usługą Azure Storage</span><span class="sxs-lookup"><span data-stu-id="e353c-133">Enable logging with Azure Storage</span></span>
    
<span data-ttu-id="e353c-134">Aby używać usługi Azure Storage do przechowywania dzienników, wybierz **archiwum na konto magazynu**, wybierz dni przechowywania i kliknij przycisk **CoreAnalytics** w obszarze **dziennika**.</span><span class="sxs-lookup"><span data-stu-id="e353c-134">To use Azure Storage to store the logs, select **Archive to a storage account**, select retention days, and click **CoreAnalytics** under **Log**.</span></span>

![Portal — dzienniki diagnostyczne](./media/cdn-diagnostics-log/04_Diagnostics-logs-storage.png)

<span data-ttu-id="e353c-136">*Rysunek 2 — rejestrowanie z usługą Azure Storage*</span><span class="sxs-lookup"><span data-stu-id="e353c-136">*Figure 2 - Logging with Azure Storage*</span></span>

### <a name="logging-with-oms-log-analytics"></a><span data-ttu-id="e353c-137">Rejestrowanie z OMS analizy dzienników</span><span class="sxs-lookup"><span data-stu-id="e353c-137">Logging with OMS Log Analytics</span></span>

<span data-ttu-id="e353c-138">Aby użyć OMS analizy dzienników do przechowywania dzienników, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="e353c-138">To use OMS Log Analytics to store the logs, follow these steps:</span></span>

1. <span data-ttu-id="e353c-139">Z **dzienników diagnostycznych** bloku w obszarze **monitorowanie**, wybierz pozycję **wysyłać do analizy dzienników** z</span><span class="sxs-lookup"><span data-stu-id="e353c-139">From the **Diagnostics Logs** blade Under **Monitoring**, select **Send to Log Analytics** from</span></span> 

    ![Portal — dzienniki diagnostyczne](./media/cdn-diagnostics-log/05_Ready-to-Configure.png)    

2. <span data-ttu-id="e353c-141">Konfiguruj rejestrowanie analizy dzienników, klikając polecenie Konfiguruj.</span><span class="sxs-lookup"><span data-stu-id="e353c-141">Configure the Log Analytics logging by clicking on Configure.</span></span> <span data-ttu-id="e353c-142">Zostanie wyświetlone okno dialogowe, w którym poprzedniej obszaru roboczego wybierz lub Utwórz nową.</span><span class="sxs-lookup"><span data-stu-id="e353c-142">This takes you to a dialog where you can select a previous workspace or create a new one.</span></span>

    ![Portal — dzienniki diagnostyczne](./media/cdn-diagnostics-log/06_Choose-workspace.png)

3. <span data-ttu-id="e353c-144">Kliknij przycisk **Utwórz nowy obszar roboczy**.</span><span class="sxs-lookup"><span data-stu-id="e353c-144">Click **Create New Workspace**.</span></span>

    ![Portal — dzienniki diagnostyczne](./media/cdn-diagnostics-log/07_Create-new.png)

4. <span data-ttu-id="e353c-146">Następnie musisz wybrać nową nazwę obszaru roboczego, istniejącej subskrypcji, grupy zasobów (Nowa lub istniejąca), lokalizacji i warstwę cenową.</span><span class="sxs-lookup"><span data-stu-id="e353c-146">Next you must select a new workspace name, existing subscription, resource group (new or existing), location, and pricing tier.</span></span> <span data-ttu-id="e353c-147">Dostępna jest opcja kotwiczenia tej konfiguracji do pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="e353c-147">You have the option of pinning this configuration to your dashboard.</span></span> <span data-ttu-id="e353c-148">Kliknij przycisk OK, aby zakończyć konfigurację.</span><span class="sxs-lookup"><span data-stu-id="e353c-148">Click OK to complete the configuration.</span></span>

    <span data-ttu-id="e353c-149">Obok obszaru roboczego powinna zostać wyświetlona z nazwami grup obszarem roboczym pakietu OMS i zasobów.</span><span class="sxs-lookup"><span data-stu-id="e353c-149">Next you should see your workspace with your OMS Workspace and Resource group names.</span></span> <span data-ttu-id="e353c-150">Nazwy musi być unikatowa i można używać tylko litery, cyfry i łączniki.</span><span class="sxs-lookup"><span data-stu-id="e353c-150">Names must be unique and can only use letters, numbers, and hyphens.</span></span> <span data-ttu-id="e353c-151">Spacje i znaki podkreślenia są niedozwolone.</span><span class="sxs-lookup"><span data-stu-id="e353c-151">Spaces and underscores are not allowed.</span></span> 

    ![Portal — dzienniki diagnostyczne](./media/cdn-diagnostics-log/08_Workspace-resource.png)

5. <span data-ttu-id="e353c-153">Otrzymasz obok krótki komunikat informujący, że obszar roboczy użytkownika został utworzony i nastąpi powrót do ekranu Konfiguracja rejestrowania.</span><span class="sxs-lookup"><span data-stu-id="e353c-153">You next get a short message saying that your workspace has been created and you are returned to your logging configuration screen.</span></span> <span data-ttu-id="e353c-154">Można potwierdzić nazwę obszaru roboczego analizy dzienników.</span><span class="sxs-lookup"><span data-stu-id="e353c-154">You can confirm the name of your Log Analytics workspace.</span></span>

    ![Portal — dzienniki diagnostyczne](./media/cdn-diagnostics-log/09_Return-to-logging.png)

    <span data-ttu-id="e353c-156">Po skonfigurowaniu konfiguracji analizy dzienników upewnij się, że możesz również CoreAnalytics pole wyboru dla rejestracji w sieci CDN.</span><span class="sxs-lookup"><span data-stu-id="e353c-156">Once you have set up the Log Analytics configuration, make sure you also check the CoreAnalytics box for CDN logging.</span></span>

6. <span data-ttu-id="e353c-157">Jeśli wszystko jest Twoim preferencjom, kliknij przycisk **zapisać** przycisk w górnej części okna dialogowego konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="e353c-157">If everything is to your liking, click the **Save** button at the top of the configuration dialog.</span></span>

    ![Portal — dzienniki diagnostyczne](./media/cdn-diagnostics-log/10_Save-me.png)

    <span data-ttu-id="e353c-159">**Zapisać** przycisk nie jest już aktywne i że naciśnięcie przycisku Dalej/OFF jest teraz na, ale blue zamiast purpurowy.</span><span class="sxs-lookup"><span data-stu-id="e353c-159">The **Save** button is no longer active and that the ON/OFF button is now ON, but blue instead of purple.</span></span>

7. <span data-ttu-id="e353c-160">Jeśli chcesz wyświetlić nowy obszar roboczy OMS, przejdź do pulpitu nawigacyjnego portalu Azure, kliknij nazwę obszaru roboczego analizy dzienników.</span><span class="sxs-lookup"><span data-stu-id="e353c-160">If you want to see your new OMS workspace, go to your Azure portal Dashboard, click the name of your Log Analytics workspace.</span></span> <span data-ttu-id="e353c-161">Następnie zostanie wyświetlony obszar roboczy (Upewnij się, że obszarem roboczym pakietu OMS są wyróżnione po lewej stronie).</span><span class="sxs-lookup"><span data-stu-id="e353c-161">Next you will see your workspace (make sure that OMS Workspace is highlighted on the left).</span></span> <span data-ttu-id="e353c-162">Kliknij Kafelek portalu OMS, aby wyświetlić obszar roboczy w repozytorium OMS.</span><span class="sxs-lookup"><span data-stu-id="e353c-162">Click on the OMS Portal tile to see your workspace in the OMS repository.</span></span> 

    ![Portal — dzienniki diagnostyczne](./media/cdn-diagnostics-log/11_OMS-dashboard.png) 

    <span data-ttu-id="e353c-164">Repozytorium OMS jest teraz gotowy do rejestrowania danych.</span><span class="sxs-lookup"><span data-stu-id="e353c-164">Your OMS repository is now ready to log data.</span></span> <span data-ttu-id="e353c-165">Aby można było korzystać z tych danych, należy użyć [rozwiązania OMS](#consuming-oms-log-analytics-data), wymienionych w dalszej części tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="e353c-165">In order to consume that data, you must use an [OMS Solution](#consuming-oms-log-analytics-data), covered later in this article.</span></span>

<span data-ttu-id="e353c-166">Więcej informacji na temat opóźnienia danych dziennika [tutaj](#log-data-delays).</span><span class="sxs-lookup"><span data-stu-id="e353c-166">For more information about log data delays, go [here](#log-data-delays).</span></span>

## <a name="enable-logging-with-powershell"></a><span data-ttu-id="e353c-167">Włącz rejestrowanie przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="e353c-167">Enable logging with PowerShell</span></span>

<span data-ttu-id="e353c-168">Poniżej znajduje się przykład sposobu włączania i pobieranie dzienników diagnostycznych za pomocą poleceń cmdlet programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e353c-168">Below is an example on how to enable and get Diagnostic Logs via the Azure PowerShell Cmdlets.</span></span>

###<a name="enabling-diagnostic-logs-in-a-storage-account"></a><span data-ttu-id="e353c-169">Włączanie diagnostyki logowania na koncie magazynu</span><span class="sxs-lookup"><span data-stu-id="e353c-169">Enabling Diagnostic Logs in a Storage Account</span></span>

<span data-ttu-id="e353c-170">Zaloguj się najpierw, a następnie wybierz subskrypcję:</span><span class="sxs-lookup"><span data-stu-id="e353c-170">First log in and select a subscription:</span></span>

    Login-AzureRmAccount 

    Select-AzureSubscription -SubscriptionId 


<span data-ttu-id="e353c-171">Aby włączyć dzienniki diagnostyczne na koncie magazynu należy użyć tego polecenia:</span><span class="sxs-lookup"><span data-stu-id="e353c-171">To Enable Diagnostic Logs in a Storage Account, use this command:</span></span>

```powershell
    Set-AzureRmDiagnosticSetting -ResourceId "/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Cdn/profiles/{profileName}/endpoints/{endpointName}" -StorageAccountId "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ClassicStorage/storageAccounts/{storageAccountName}" -Enabled $true -Categories CoreAnalytics
```
<span data-ttu-id="e353c-172">Aby włączyć dzienniki diagnostyki w obszarze roboczym pakietu OMS należy użyć tego polecenia:</span><span class="sxs-lookup"><span data-stu-id="e353c-172">To Enable Diagnostics Logs in an OMS workspace, use this command:</span></span>

```powershell
    Set-AzureRmDiagnosticSetting -ResourceId "/subscriptions/`{subscriptionId}<subscriptionId>
    .<subscriptionName>" -WorkspaceId "/subscriptions/<workspaceId>.<workspaceName>" -Enabled $true -Categories CoreAnalytics 
```



## <a name="consuming-diagnostics-logs-from-azure-storage"></a><span data-ttu-id="e353c-173">Korzystanie z dzienników diagnostycznych z usługi Azure Storage</span><span class="sxs-lookup"><span data-stu-id="e353c-173">Consuming diagnostics logs from Azure Storage</span></span>
<span data-ttu-id="e353c-174">W tej sekcji opisano schematu z sieci CDN w warstwie podstawowa analiza, jak te są zorganizowane w ramach konta magazynu platformy Azure i udostępnia przykładowy kod, aby pobrać dzienniki w pliku CSV.</span><span class="sxs-lookup"><span data-stu-id="e353c-174">This section describes the schema of the CDN core analytics, how these are organized inside of an Azure Storage Account and provides sample code to download the logs in to a CSV file.</span></span>

### <a name="using-microsoft-azure-storage-explorer"></a><span data-ttu-id="e353c-175">Za pomocą Eksploratora usługi Storage platformy Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="e353c-175">Using Microsoft Azure Storage Explorer</span></span>
<span data-ttu-id="e353c-176">Przed uzyskujesz dostęp do podstawowych danych analytics z konta magazynu Azure, musisz najpierw narzędzia dostępu do zawartości na koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="e353c-176">Before you can access the core analytics data from the Azure Storage Account, you first need a tool to access the contents in a storage account.</span></span> <span data-ttu-id="e353c-177">Gdy brak kilka narzędzi dostępnych na rynku, zaleca się jest Eksploratora magazynu Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="e353c-177">While there are several tools available in the market, the one that we recommend is the Microsoft Azure Storage Explorer.</span></span> <span data-ttu-id="e353c-178">Możesz pobrać narzędzie z [tutaj](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="e353c-178">You can download the tool from [here](http://storageexplorer.com/).</span></span> <span data-ttu-id="e353c-179">Po pobraniu i zainstalowaniu oprogramowania, należy skonfigurować go do używania tego samego konta magazynu Azure, który został skonfigurowany jako miejsce docelowe do dzienników diagnostycznych CDN.</span><span class="sxs-lookup"><span data-stu-id="e353c-179">After downloading and installing the software, configure it to use the same Azure Storage Account that was configured as a destination to the CDN Diagnostics Logs.</span></span>

1.  <span data-ttu-id="e353c-180">Otwórz **Eksploratora usługi Storage platformy Microsoft Azure**</span><span class="sxs-lookup"><span data-stu-id="e353c-180">Open **Microsoft Azure Storage Explorer**</span></span>
2.  <span data-ttu-id="e353c-181">Zlokalizuj konto magazynu</span><span class="sxs-lookup"><span data-stu-id="e353c-181">Locate the storage account</span></span>
3.  <span data-ttu-id="e353c-182">Przejdź do **"Kontenerów obiektów Blob"** węźle tego magazynu konta, a następnie rozwiń węzeł</span><span class="sxs-lookup"><span data-stu-id="e353c-182">Go to the **“Blob Containers”** node under this storage account and expand the node</span></span>
4.  <span data-ttu-id="e353c-183">Wybierz kontener o nazwie **"insights dzienniki coreanalytics"** i kliknij ją dwukrotnie</span><span class="sxs-lookup"><span data-stu-id="e353c-183">Select the container named **“insights-logs-coreanalytics”** and double-click it</span></span>
5.  <span data-ttu-id="e353c-184">Powoduje Pokaż się w okienku po prawej stronie, rozpoczynając od pierwszego poziomu, który wygląda podobnie **"resourceId ="**.</span><span class="sxs-lookup"><span data-stu-id="e353c-184">Results show up on the right-hand pane starting with the first level, which looks like **“resourceId=”**.</span></span> <span data-ttu-id="e353c-185">Klikaj aż do momentu znajduje się w pliku **PT1H.json**.</span><span class="sxs-lookup"><span data-stu-id="e353c-185">Continue clicking all the way until you see the file **PT1H.json**.</span></span> <span data-ttu-id="e353c-186">Zobacz uwagę następujące wyjaśnienie ścieżki.</span><span class="sxs-lookup"><span data-stu-id="e353c-186">See the following note for explanation of the path.</span></span>
6.  <span data-ttu-id="e353c-187">Każdy obiekt blob **PT1H.json** reprezentuje dzienniki analizy przez godzinę dla określonego punktu końcowego CDN lub jego domeny niestandardowej.</span><span class="sxs-lookup"><span data-stu-id="e353c-187">Each blob **PT1H.json** represents the analytics logs for one hour for a specific CDN endpoint or its custom domain.</span></span>
7.  <span data-ttu-id="e353c-188">Schemat zawartość tego pliku JSON jest opisany w sekcji schematu Core analizy dzienników</span><span class="sxs-lookup"><span data-stu-id="e353c-188">The schema of the contents of this JSON file is described in the section Schema of the Core Analytics Logs</span></span>


> [!NOTE]
> <span data-ttu-id="e353c-189">**Format ścieżki obiektu blob**</span><span class="sxs-lookup"><span data-stu-id="e353c-189">**Blob path format**</span></span>
> 
> <span data-ttu-id="e353c-190">Dzienniki Analytics Core są generowane co godzinę.</span><span class="sxs-lookup"><span data-stu-id="e353c-190">Core Analytics logs are generated every hour.</span></span> <span data-ttu-id="e353c-191">Wszystkie dane przez godzinę są zbierane i przechowywane wewnątrz pojedynczego obiektu Blob Azure jako ładunek JSON.</span><span class="sxs-lookup"><span data-stu-id="e353c-191">All data for an hour are collected and stored inside a single Azure Blob as a JSON payload.</span></span> <span data-ttu-id="e353c-192">Ścieżka do tego obiektu Blob Azure jest wyświetlana tak, jakby to hierarchiczna struktura.</span><span class="sxs-lookup"><span data-stu-id="e353c-192">The path to this Azure Blob appears as if there is a hierarchical structure.</span></span> <span data-ttu-id="e353c-193">Jest ponieważ narzędzia Eksplorator magazynu interpretuje "/" jako separatora katalogu, który wyświetla hierarchię jako udogodnienie.</span><span class="sxs-lookup"><span data-stu-id="e353c-193">This is because the Storage explorer tool interprets '/' as a directory separator and shows the hierarchy for convenience.</span></span> <span data-ttu-id="e353c-194">W rzeczywistości pełną ścieżkę reprezentuje tylko nazwa obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="e353c-194">Actually, the whole path just represents the blob name.</span></span> <span data-ttu-id="e353c-195">Następuje to nazwa obiektu blob następującej konwencji nazewnictwa</span><span class="sxs-lookup"><span data-stu-id="e353c-195">This name of the blob follows the following naming convention</span></span>   
    
    resourceId=/SUBSCRIPTIONS/{Subscription Id}/RESOURCEGROUPS/{Resource Group Name}/PROVIDERS/MICROSOFT.CDN/PROFILES/{Profile Name}/ENDPOINTS/{Endpoint Name}/ y={Year}/m={Month}/d={Day}/h={Hour}/m={Minutes}/PT1H.json

<span data-ttu-id="e353c-196">**Opis pola:**</span><span class="sxs-lookup"><span data-stu-id="e353c-196">**Description of fields:**</span></span>

|<span data-ttu-id="e353c-197">wartość</span><span class="sxs-lookup"><span data-stu-id="e353c-197">value</span></span>|<span data-ttu-id="e353c-198">Opis elementu</span><span class="sxs-lookup"><span data-stu-id="e353c-198">description</span></span>|
|-------|---------|
|<span data-ttu-id="e353c-199">Identyfikator subskrypcji</span><span class="sxs-lookup"><span data-stu-id="e353c-199">Subscription ID</span></span>    |<span data-ttu-id="e353c-200">Identyfikator subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="e353c-200">ID of the Azure Subscription.</span></span> <span data-ttu-id="e353c-201">To jest w formacie Guid.</span><span class="sxs-lookup"><span data-stu-id="e353c-201">This is in the Guid format.</span></span>|
|<span data-ttu-id="e353c-202">Zasób</span><span class="sxs-lookup"><span data-stu-id="e353c-202">Resource</span></span> |<span data-ttu-id="e353c-203">Nazwa grupy Nazwa grupy zasobów, do której należą zasoby sieci CDN.</span><span class="sxs-lookup"><span data-stu-id="e353c-203">Group Name   Name of the resource group to which the CDN resources belong.</span></span>|
|<span data-ttu-id="e353c-204">Nazwa profilu</span><span class="sxs-lookup"><span data-stu-id="e353c-204">Profile Name</span></span> |<span data-ttu-id="e353c-205">Nazwa profilu CDN</span><span class="sxs-lookup"><span data-stu-id="e353c-205">Name of the CDN Profile</span></span>|
|<span data-ttu-id="e353c-206">Nazwa punktu końcowego</span><span class="sxs-lookup"><span data-stu-id="e353c-206">Endpoint Name</span></span> |<span data-ttu-id="e353c-207">Nazwa punktu końcowego CDN</span><span class="sxs-lookup"><span data-stu-id="e353c-207">Name of the CDN Endpoint</span></span>|
|<span data-ttu-id="e353c-208">Roku</span><span class="sxs-lookup"><span data-stu-id="e353c-208">Year</span></span>|  <span data-ttu-id="e353c-209">Reprezentacja 4-cyfrowego roku, na przykład 2017 r.</span><span class="sxs-lookup"><span data-stu-id="e353c-209">4-digit representation of the year for example, 2017</span></span>|
|<span data-ttu-id="e353c-210">Miesiąc</span><span class="sxs-lookup"><span data-stu-id="e353c-210">Month</span></span>| <span data-ttu-id="e353c-211">Reprezentacja 2-cyfrowy numer miesiąca.</span><span class="sxs-lookup"><span data-stu-id="e353c-211">2-digit representation of the month number.</span></span> <span data-ttu-id="e353c-212">01 stycznia =... 12 grudnia =</span><span class="sxs-lookup"><span data-stu-id="e353c-212">01=January ... 12=December</span></span>|
|<span data-ttu-id="e353c-213">Dzień</span><span class="sxs-lookup"><span data-stu-id="e353c-213">Day</span></span>|   <span data-ttu-id="e353c-214">Reprezentacja 2 cyfry dnia miesiąca</span><span class="sxs-lookup"><span data-stu-id="e353c-214">2 digit representation of the day of the month</span></span>|
|<span data-ttu-id="e353c-215">PT1H.JSON</span><span class="sxs-lookup"><span data-stu-id="e353c-215">PT1H.json</span></span>| <span data-ttu-id="e353c-216">Rzeczywisty plik JSON, gdzie są przechowywane dane analityczne</span><span class="sxs-lookup"><span data-stu-id="e353c-216">Actual JSON file where the analytics data is stored</span></span>|

### <a name="exporting-the-core-analytics-data-to-a-csv-file"></a><span data-ttu-id="e353c-217">Eksportowanie danych Analytics Core do pliku CSV</span><span class="sxs-lookup"><span data-stu-id="e353c-217">Exporting the Core Analytics Data to a CSV File</span></span>

<span data-ttu-id="e353c-218">Aby ułatwić dostęp do analizy Core, udostępniamy przykładowy kod dla narzędzia, która umożliwia pobieranie plików JSON na format pliku płaskim przecinkami, który umożliwia łatwe tworzenie wykresów lub innych agregacji.</span><span class="sxs-lookup"><span data-stu-id="e353c-218">To make it easy to access the Core Analytics, we provide a sample code for a tool, which allows downloading the JSON files into a flat comma-separated file format, which can be used to easily create charts or other aggregations.</span></span>

<span data-ttu-id="e353c-219">Oto, jak można użyć narzędzia:</span><span class="sxs-lookup"><span data-stu-id="e353c-219">Here is how you can use the tool:</span></span>

1.  <span data-ttu-id="e353c-220">Skorzystaj z łącza github: [https://github.com/Azure-Samples/azure-cdn-samples/tree/master/CoreAnalytics-ExportToCsv](https://github.com/Azure-Samples/azure-cdn-samples/tree/master/CoreAnalytics-ExportToCsv )</span><span class="sxs-lookup"><span data-stu-id="e353c-220">Visit the github link: [https://github.com/Azure-Samples/azure-cdn-samples/tree/master/CoreAnalytics-ExportToCsv ](https://github.com/Azure-Samples/azure-cdn-samples/tree/master/CoreAnalytics-ExportToCsv )</span></span>
2.  <span data-ttu-id="e353c-221">Pobieranie kodu</span><span class="sxs-lookup"><span data-stu-id="e353c-221">Download the code</span></span>
3.  <span data-ttu-id="e353c-222">Postępuj zgodnie z instrukcjami, aby skompilować i skonfigurować</span><span class="sxs-lookup"><span data-stu-id="e353c-222">Follow instructions to compile and configure</span></span>
4.  <span data-ttu-id="e353c-223">Uruchom narzędzie</span><span class="sxs-lookup"><span data-stu-id="e353c-223">Run the tool</span></span>
5.  <span data-ttu-id="e353c-224">Wynikowy plik CSV zawiera dane analityczne w prosty płaskiej hierarchii.</span><span class="sxs-lookup"><span data-stu-id="e353c-224">Resulting CSV file shows the analytics data in a simple flat hierarchy.</span></span>

## <a name="consuming-diagnostics-logs-from-an-oms-log-analytics-repository"></a><span data-ttu-id="e353c-225">Korzystanie z dzienników diagnostycznych z repozytorium OMS analizy dzienników</span><span class="sxs-lookup"><span data-stu-id="e353c-225">Consuming diagnostics logs from an OMS Log Analytics repository</span></span>
<span data-ttu-id="e353c-226">Analiza dzienników jest usługą w operacji pakietu zarządzania (OMS), który monitoruje chmurze i lokalnych środowiskach utrzymywać ich dostępności i wydajności.</span><span class="sxs-lookup"><span data-stu-id="e353c-226">Log Analytics is a service in Operations Management Suite (OMS) that monitors your cloud and on-premises environments to maintain their availability and performance.</span></span> <span data-ttu-id="e353c-227">Zbiera ona dane generowane przez zasoby w środowiskach chmurowych i lokalnych oraz inne narzędzia do monitorowania, aby przeprowadzać analizę na podstawie wielu źródeł.</span><span class="sxs-lookup"><span data-stu-id="e353c-227">It collects data generated by resources in your cloud and on-premises environments and from other monitoring tools to provide analysis across multiple sources.</span></span> 

<span data-ttu-id="e353c-228">Aby korzystać z analizy dzienników, należy najpierw [włączyć rejestrowanie](#enable-logging-with-azure-storage) do repozytorium Analiza dzienników Azure OMS które omówione w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="e353c-228">To use Log Analytics, you must [enable logging](#enable-logging-with-azure-storage) to the Azure OMS Log Analytics repository, which is discussed earlier in this article.</span></span>

### <a name="using-the-oms-repository"></a><span data-ttu-id="e353c-229">Przy użyciu repozytorium OMS</span><span class="sxs-lookup"><span data-stu-id="e353c-229">Using the OMS Repository</span></span>

 <span data-ttu-id="e353c-230">Na poniższym diagramie przedstawiono architekturę danych wejściowych i wyjściowych repozytorium:</span><span class="sxs-lookup"><span data-stu-id="e353c-230">The following diagram shows the architecture of the inputs and outputs of the repository:</span></span>

![Repozytorium analizy dziennika OMS](./media/cdn-diagnostics-log/12_Repo-overview.png)

<span data-ttu-id="e353c-232">*Rysunek 3 – repozytorium analizy dzienników*</span><span class="sxs-lookup"><span data-stu-id="e353c-232">*Figure 3 - Log Analytics Repository*</span></span>

<span data-ttu-id="e353c-233">Dane można wyświetlić w na różne sposoby, za pomocą rozwiązania do zarządzania.</span><span class="sxs-lookup"><span data-stu-id="e353c-233">You can display the data in a variety of ways by using Management Solutions.</span></span> <span data-ttu-id="e353c-234">Można uzyskać z rozwiązania do zarządzania [portalu Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/monitoring-management?page=1&subcategories=management-solutions).</span><span class="sxs-lookup"><span data-stu-id="e353c-234">You can obtain Management Solutions from the [Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/monitoring-management?page=1&subcategories=management-solutions).</span></span>

<span data-ttu-id="e353c-235">Rozwiązania do zarządzania można zainstalować z portalu Azure marketplace, klikając **Pobierz teraz** łącze u dołu każdego z rozwiązań.</span><span class="sxs-lookup"><span data-stu-id="e353c-235">You can install management solutions from Azure marketplace by clicking the **Get it now** link at the bottom of each solution.</span></span>

### <a name="adding-an-oms-cdn-management-solution"></a><span data-ttu-id="e353c-236">Dodawanie rozwiązania do zarządzania OMS CDN</span><span class="sxs-lookup"><span data-stu-id="e353c-236">Adding an OMS CDN Management Solution</span></span>

<span data-ttu-id="e353c-237">Wykonaj następujące kroki, aby dodać rozwiązanie do zarządzania:</span><span class="sxs-lookup"><span data-stu-id="e353c-237">Follow these steps to add a Management Solution:</span></span>

1.   <span data-ttu-id="e353c-238">Jeśli jeszcze tego nie zrobiono, zaloguj się do portalu Azure przy użyciu subskrypcji platformy Azure i przejdź do pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="e353c-238">If you haven't already done so, sign in to the Azure portal using your Azure subscription and go to your Dashboard.</span></span>
    <span data-ttu-id="e353c-239">![Pulpit nawigacyjny platformy Azure](./media/cdn-diagnostics-log/13_Azure-dashboard.png)</span><span class="sxs-lookup"><span data-stu-id="e353c-239">![Azure Dashboard](./media/cdn-diagnostics-log/13_Azure-dashboard.png)</span></span>

2. <span data-ttu-id="e353c-240">W **nowy** bloku w obszarze **Marketplace**, wybierz pozycję **monitorowanie i zarządzanie**.</span><span class="sxs-lookup"><span data-stu-id="e353c-240">In the **New** blade under **Marketplace**, select **Monitoring + management**.</span></span>

    ![Portal Marketplace](./media/cdn-diagnostics-log/14_Marketplace.png)

3. <span data-ttu-id="e353c-242">W **monitorowanie i zarządzanie** bloku, kliknij przycisk **zobaczyć wszystkie**.</span><span class="sxs-lookup"><span data-stu-id="e353c-242">In the **Monitoring + management** blade, click **See all**.</span></span>

    ![Zobacz wszystkie](./media/cdn-diagnostics-log/15_See-all.png)

4.  <span data-ttu-id="e353c-244">Wyszukiwanie sieci CDN w polu wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="e353c-244">Search for CDN in the search box.</span></span>

    ![Zobacz wszystkie](./media/cdn-diagnostics-log/16_Search-for.png)

5.  <span data-ttu-id="e353c-246">Wybierz **usługi Azure CDN podstawowa analiza**.</span><span class="sxs-lookup"><span data-stu-id="e353c-246">Select **Azure CDN Core Analytics**.</span></span> 

    ![Zobacz wszystkie](./media/cdn-diagnostics-log/17_Core-analytics.png)

6.  <span data-ttu-id="e353c-248">Po kliknięciu przycisku **Utwórz**, użytkownik będzie musiał utworzyć nowy obszar roboczy OMS lub użyć istniejącego.</span><span class="sxs-lookup"><span data-stu-id="e353c-248">After clicking **Create**, you will be asked to create a new OMS workspace or use an existing one.</span></span> 

    ![Zobacz wszystkie](./media/cdn-diagnostics-log/18_Adding-solution.png)

7.  <span data-ttu-id="e353c-250">Wybierz obszar roboczy utworzony przed.</span><span class="sxs-lookup"><span data-stu-id="e353c-250">Select the workspace you created before.</span></span> <span data-ttu-id="e353c-251">Następnie należy dodać konto usługi Automatyzacja.</span><span class="sxs-lookup"><span data-stu-id="e353c-251">You then need to add an automation account.</span></span>

    ![Zobacz wszystkie](./media/cdn-diagnostics-log/19_Add-automation.png)

8. <span data-ttu-id="e353c-253">Następujący ekran pokazuje musisz wypełnić formularz konta automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="e353c-253">The following screen shows the automation account form you must fill out.</span></span> 

    ![Zobacz wszystkie](./media/cdn-diagnostics-log/20_Automation.png)

9. <span data-ttu-id="e353c-255">Po utworzeniu konta automatyzacji, można przystąpić do dodawania rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="e353c-255">Once you have created the automation account, you are ready to add your solution.</span></span> <span data-ttu-id="e353c-256">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="e353c-256">Click the **Create** button.</span></span>

    ![Zobacz wszystkie](./media/cdn-diagnostics-log/21_Ready.png)

10. <span data-ttu-id="e353c-258">Teraz dodano rozwiązania do swojego obszaru roboczego.</span><span class="sxs-lookup"><span data-stu-id="e353c-258">Your solution has now been added to your workspace.</span></span> <span data-ttu-id="e353c-259">Wróć do pulpitu nawigacyjnego portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="e353c-259">Go back to your Azure portal Dashboard.</span></span>

    ![Zobacz wszystkie](./media/cdn-diagnostics-log/22_Dashboard.png)

    <span data-ttu-id="e353c-261">Kliknij obszar roboczy analizy dzienników, utworzonego przejdź do obszaru roboczego.</span><span class="sxs-lookup"><span data-stu-id="e353c-261">Click the Log Analytics workspace you created to go to your workspace.</span></span> 

11. <span data-ttu-id="e353c-262">Kliknij przycisk **portalu OMS** Kafelek, aby zobaczyć nowe rozwiązania w portalu OMS.</span><span class="sxs-lookup"><span data-stu-id="e353c-262">Click the **OMS Portal** tile to see your new solution in the OMS portal.</span></span>

    ![Zobacz wszystkie](./media/cdn-diagnostics-log/23_workspace.png)

12. <span data-ttu-id="e353c-264">Portalu OMS powinna wyglądać tak jak następujący ekran:</span><span class="sxs-lookup"><span data-stu-id="e353c-264">Your OMS portal should now look like the following screen:</span></span>

    ![Zobacz wszystkie](./media/cdn-diagnostics-log/24_OMS-solution.png)

    <span data-ttu-id="e353c-266">Kliknij jeden z fragmentów, aby wyświetlić kilka widoków danych.</span><span class="sxs-lookup"><span data-stu-id="e353c-266">Click one of the tiles to see several views into your data.</span></span>

    ![Zobacz wszystkie](./media/cdn-diagnostics-log/25_Interior-view.png)

    <span data-ttu-id="e353c-268">Po lewej lub prawej strony, aby wyświetlić dalsze Kafelki reprezentujących poszczególnych widoków do danych mogą być przewijane.</span><span class="sxs-lookup"><span data-stu-id="e353c-268">You can scroll left or right to see further tiles representing individual views into the data.</span></span> 

    <span data-ttu-id="e353c-269">Kliknij jeden z fragmentów zapewnia szczegółowe informacje o danych.</span><span class="sxs-lookup"><span data-stu-id="e353c-269">Clicking one of the tiles gives you more details about your data.</span></span>

     ![Zobacz wszystkie](./media/cdn-diagnostics-log/26_Further-detail.png)

### <a name="offers-and-pricing-tiers"></a><span data-ttu-id="e353c-271">Oferty i warstw cenowych</span><span class="sxs-lookup"><span data-stu-id="e353c-271">Offers and pricing tiers</span></span>

<span data-ttu-id="e353c-272">Możesz wyświetlać oferty i warstw cenowych dla rozwiązań do zarządzania OMS [tutaj](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-add-solutions#offers-and-pricing-tiers).</span><span class="sxs-lookup"><span data-stu-id="e353c-272">You can see offers and pricing tiers for OMS management solutions [here](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-add-solutions#offers-and-pricing-tiers).</span></span>

### <a name="customizing-views"></a><span data-ttu-id="e353c-273">Dostosowywanie widoków</span><span class="sxs-lookup"><span data-stu-id="e353c-273">Customizing views</span></span>

<span data-ttu-id="e353c-274">Widok danych można dostosować za pomocą **Widok projektanta**.</span><span class="sxs-lookup"><span data-stu-id="e353c-274">You can customize the view into your data by using the **View Designer**.</span></span> <span data-ttu-id="e353c-275">Przejdź do obszaru roboczego OMS i rozpoczęciu projektowania, klikając **Widok projektanta** kafelka.</span><span class="sxs-lookup"><span data-stu-id="e353c-275">Go to your OMS workspace and begin designing by clicking the **View Designer** tile.</span></span>

![Projektant widoków](./media/cdn-diagnostics-log/27_Designer.png)

<span data-ttu-id="e353c-277">Można przeciągnąć i upuścić typów wykresów z lewej strony i wypełnij szczegóły danych, które mają być analizowane po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="e353c-277">You can drag and drop types of charts from the left and fill in the data details you want to analyze on the left.</span></span>

![Projektant widoków](./media/cdn-diagnostics-log/28_Designer.png)

    
## <a name="log-data-delays"></a><span data-ttu-id="e353c-279">Opóźnienia dane dziennika</span><span class="sxs-lookup"><span data-stu-id="e353c-279">Log data delays</span></span>

<span data-ttu-id="e353c-280">Opóźnienia danych dziennika Verizon</span><span class="sxs-lookup"><span data-stu-id="e353c-280">Verizon log data delays</span></span> | <span data-ttu-id="e353c-281">Opóźnienia danych dziennika Akamai</span><span class="sxs-lookup"><span data-stu-id="e353c-281">Akamai log data delays</span></span>
--- | ---
<span data-ttu-id="e353c-282">Dane dziennika Verizon 1 godzina opóźnienia i potrwać maksymalnie 2 godziny, aby uruchomić pojawiające się po zakończeniu propagowania punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="e353c-282">Verizon log data is 1 hour delayed, and take up to 2 hours to start appearing after endpoint propagation completion.</span></span> | <span data-ttu-id="e353c-283">Dane dziennika Akamai wynosi 24 godziny, opóźnienia i przejście do 2 godzin Rozpocznij wyświetlaniu, jeśli został on utworzony więcej niż 24 godziny temu.</span><span class="sxs-lookup"><span data-stu-id="e353c-283">Akamai log data is 24 hours delayed, and takes up to 2 hours to start appearing if it was created more than 24 hours ago.</span></span> <span data-ttu-id="e353c-284">Jeśli niedawno został utworzony, może upłynąć do 25 godzin dzienniki, aby uruchomić wyświetlaniu.</span><span class="sxs-lookup"><span data-stu-id="e353c-284">If it was recently created, it can take up to 25 hours for the logs to start appearing.</span></span>

## <a name="diagnostic-log-types-for-cdn-core-analytics"></a><span data-ttu-id="e353c-285">Typy dzienników diagnostycznych do sieci CDN w warstwie podstawowa analiza</span><span class="sxs-lookup"><span data-stu-id="e353c-285">Diagnostic log types for CDN Core Analytics</span></span>

<span data-ttu-id="e353c-286">Firma Microsoft oferuje obecnie tylko podstawowa Analiza dzienników zawierających metryki wyświetlane statystki odpowiedzi HTTP i statystyki wyjście widziany od obecności CDN/krawędzi.</span><span class="sxs-lookup"><span data-stu-id="e353c-286">We currently offer only Core Analytics logs, which contain metrics showing HTTP response statistics and egress statistics as seen from the CDN POPs/edges.</span></span>

### <a name="core-analytics-metrics-details"></a><span data-ttu-id="e353c-287">Szczegóły metryki Analytics Core</span><span class="sxs-lookup"><span data-stu-id="e353c-287">Core Analytics Metrics Details</span></span>
<span data-ttu-id="e353c-288">W poniższej tabeli przedstawiono listę dostępnych w dziennikach podstawowa analiza metryk.</span><span class="sxs-lookup"><span data-stu-id="e353c-288">The following table shows a list of metrics available in the Core Analytics logs.</span></span> <span data-ttu-id="e353c-289">Nie wszystkie metryki są dostępne z wszystkich dostawców, choć różnice są minimalne.</span><span class="sxs-lookup"><span data-stu-id="e353c-289">Not all metrics are available from all providers, although such differences are minimal.</span></span> <span data-ttu-id="e353c-290">W poniższej tabeli przedstawiono także, czy dana metryka jest dostępna od dostawcy.</span><span class="sxs-lookup"><span data-stu-id="e353c-290">The following table also shows if a given metric is available from a provider.</span></span> <span data-ttu-id="e353c-291">Należy pamiętać, że metryki są dostępne tylko tych punktów końcowych usługi CDN których ruchu.</span><span class="sxs-lookup"><span data-stu-id="e353c-291">Please note that the metrics are available for only those CDN endpoints that have traffic on them.</span></span>


|<span data-ttu-id="e353c-292">Metryka</span><span class="sxs-lookup"><span data-stu-id="e353c-292">Metric</span></span>                     | <span data-ttu-id="e353c-293">Opis</span><span class="sxs-lookup"><span data-stu-id="e353c-293">Description</span></span>   | <span data-ttu-id="e353c-294">Verizon</span><span class="sxs-lookup"><span data-stu-id="e353c-294">Verizon</span></span>  | <span data-ttu-id="e353c-295">Akamai</span><span class="sxs-lookup"><span data-stu-id="e353c-295">Akamai</span></span> 
|---------------------------|---------------|---|---|
| <span data-ttu-id="e353c-296">RequestCountTotal</span><span class="sxs-lookup"><span data-stu-id="e353c-296">RequestCountTotal</span></span>         |<span data-ttu-id="e353c-297">Całkowita liczba trafień żądania podczas tego okresu.</span><span class="sxs-lookup"><span data-stu-id="e353c-297">Total number of request hits during this period</span></span>| <span data-ttu-id="e353c-298">Tak</span><span class="sxs-lookup"><span data-stu-id="e353c-298">Yes</span></span>  |<span data-ttu-id="e353c-299">Tak</span><span class="sxs-lookup"><span data-stu-id="e353c-299">Yes</span></span>   |
| <span data-ttu-id="e353c-300">RequestCountHttpStatus2xx</span><span class="sxs-lookup"><span data-stu-id="e353c-300">RequestCountHttpStatus2xx</span></span> |<span data-ttu-id="e353c-301">Liczba wszystkich żądań, które wywołały kod HTTP 2xx (200, 202)</span><span class="sxs-lookup"><span data-stu-id="e353c-301">Count of all requests that resulted in a 2xx HTTP code (e.g. 200, 202)</span></span>              | <span data-ttu-id="e353c-302">Tak</span><span class="sxs-lookup"><span data-stu-id="e353c-302">Yes</span></span>  |<span data-ttu-id="e353c-303">Tak</span><span class="sxs-lookup"><span data-stu-id="e353c-303">Yes</span></span>   |
| <span data-ttu-id="e353c-304">RequestCountHttpStatus3xx</span><span class="sxs-lookup"><span data-stu-id="e353c-304">RequestCountHttpStatus3xx</span></span> | <span data-ttu-id="e353c-305">Liczba wszystkich żądań, które wywołały kod HTTP 3xx (np. 300, 302)</span><span class="sxs-lookup"><span data-stu-id="e353c-305">Count of all requests that resulted in a 3xx HTTP code (e.g. 300, 302)</span></span>              | <span data-ttu-id="e353c-306">Tak</span><span class="sxs-lookup"><span data-stu-id="e353c-306">Yes</span></span>  |<span data-ttu-id="e353c-307">Tak</span><span class="sxs-lookup"><span data-stu-id="e353c-307">Yes</span></span>   |
| <span data-ttu-id="e353c-308">RequestCountHttpStatus4xx</span><span class="sxs-lookup"><span data-stu-id="e353c-308">RequestCountHttpStatus4xx</span></span> |<span data-ttu-id="e353c-309">Liczba wszystkich żądań, które wywołały kod HTTP 4xx (np. 400, 404)</span><span class="sxs-lookup"><span data-stu-id="e353c-309">Count of all requests that resulted in a 4xx HTTP code (e.g. 400, 404)</span></span>               | <span data-ttu-id="e353c-310">Tak</span><span class="sxs-lookup"><span data-stu-id="e353c-310">Yes</span></span>   |<span data-ttu-id="e353c-311">Tak</span><span class="sxs-lookup"><span data-stu-id="e353c-311">Yes</span></span>   |
| <span data-ttu-id="e353c-312">RequestCountHttpStatus5xx</span><span class="sxs-lookup"><span data-stu-id="e353c-312">RequestCountHttpStatus5xx</span></span> | <span data-ttu-id="e353c-313">Liczba wszystkich żądań, które wywołały kod HTTP 5xx (np. 500, 504)</span><span class="sxs-lookup"><span data-stu-id="e353c-313">Count of all requests that resulted in a 5xx HTTP code (e.g. 500, 504)</span></span>              | <span data-ttu-id="e353c-314">Tak</span><span class="sxs-lookup"><span data-stu-id="e353c-314">Yes</span></span>  |<span data-ttu-id="e353c-315">Tak</span><span class="sxs-lookup"><span data-stu-id="e353c-315">Yes</span></span>   |
| <span data-ttu-id="e353c-316">RequestCountHttpStatusOthers</span><span class="sxs-lookup"><span data-stu-id="e353c-316">RequestCountHttpStatusOthers</span></span> |  <span data-ttu-id="e353c-317">Liczba innych kodów HTTP (poza 2xx 5xx)</span><span class="sxs-lookup"><span data-stu-id="e353c-317">Count of all other HTTP codes (outside of 2xx-5xx)</span></span> | <span data-ttu-id="e353c-318">Tak</span><span class="sxs-lookup"><span data-stu-id="e353c-318">Yes</span></span>  |<span data-ttu-id="e353c-319">Tak</span><span class="sxs-lookup"><span data-stu-id="e353c-319">Yes</span></span>   |
| <span data-ttu-id="e353c-320">RequestCountHttpStatus200</span><span class="sxs-lookup"><span data-stu-id="e353c-320">RequestCountHttpStatus200</span></span> | <span data-ttu-id="e353c-321">Liczba wszystkich żądań, które spowodowało 200 kod odpowiedzi HTTP</span><span class="sxs-lookup"><span data-stu-id="e353c-321">Count of all requests that resulted in a 200 HTTP code response</span></span>              |<span data-ttu-id="e353c-322">Nie</span><span class="sxs-lookup"><span data-stu-id="e353c-322">No</span></span>   |<span data-ttu-id="e353c-323">Tak</span><span class="sxs-lookup"><span data-stu-id="e353c-323">Yes</span></span>   |
| <span data-ttu-id="e353c-324">RequestCountHttpStatus206</span><span class="sxs-lookup"><span data-stu-id="e353c-324">RequestCountHttpStatus206</span></span> | <span data-ttu-id="e353c-325">Liczba wszystkich żądań, które wywołały kod odpowiedź HTTP 206</span><span class="sxs-lookup"><span data-stu-id="e353c-325">Count of all requests that resulted in a 206 HTTP code response</span></span>              |<span data-ttu-id="e353c-326">Nie</span><span class="sxs-lookup"><span data-stu-id="e353c-326">No</span></span>   |<span data-ttu-id="e353c-327">Tak</span><span class="sxs-lookup"><span data-stu-id="e353c-327">Yes</span></span>   |
| <span data-ttu-id="e353c-328">RequestCountHttpStatus302</span><span class="sxs-lookup"><span data-stu-id="e353c-328">RequestCountHttpStatus302</span></span> | <span data-ttu-id="e353c-329">Liczba wszystkich żądań, które spowodowało 302 kod odpowiedzi HTTP</span><span class="sxs-lookup"><span data-stu-id="e353c-329">Count of all requests that resulted in a 302 HTTP code response</span></span>              |<span data-ttu-id="e353c-330">Nie</span><span class="sxs-lookup"><span data-stu-id="e353c-330">No</span></span>   |<span data-ttu-id="e353c-331">Tak</span><span class="sxs-lookup"><span data-stu-id="e353c-331">Yes</span></span>   |
| <span data-ttu-id="e353c-332">RequestCountHttpStatus304</span><span class="sxs-lookup"><span data-stu-id="e353c-332">RequestCountHttpStatus304</span></span> |  <span data-ttu-id="e353c-333">Liczba wszystkich żądań, które zakończyły się odpowiedź 304 kodu HTTP</span><span class="sxs-lookup"><span data-stu-id="e353c-333">Count of all requests that resulted in a 304 HTTP code response</span></span>             |<span data-ttu-id="e353c-334">Nie</span><span class="sxs-lookup"><span data-stu-id="e353c-334">No</span></span>   |<span data-ttu-id="e353c-335">Tak</span><span class="sxs-lookup"><span data-stu-id="e353c-335">Yes</span></span>   |
| <span data-ttu-id="e353c-336">RequestCountHttpStatus404</span><span class="sxs-lookup"><span data-stu-id="e353c-336">RequestCountHttpStatus404</span></span> | <span data-ttu-id="e353c-337">Liczba wszystkich żądań, które wywołały kod odpowiedzi HTTP 404</span><span class="sxs-lookup"><span data-stu-id="e353c-337">Count of all requests that resulted in a 404 HTTP code response</span></span>              |<span data-ttu-id="e353c-338">Nie</span><span class="sxs-lookup"><span data-stu-id="e353c-338">No</span></span>   |<span data-ttu-id="e353c-339">Tak</span><span class="sxs-lookup"><span data-stu-id="e353c-339">Yes</span></span>   |
| <span data-ttu-id="e353c-340">RequestCountCacheHit</span><span class="sxs-lookup"><span data-stu-id="e353c-340">RequestCountCacheHit</span></span> |<span data-ttu-id="e353c-341">Liczba wszystkich żądań, które zakończyły się liczby trafień pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="e353c-341">Count of all requests that resulted in a Cache Hit.</span></span> <span data-ttu-id="e353c-342">Oznacza to, że zasób zostało obsłużone bezpośrednio z punktu obecności do klienta.</span><span class="sxs-lookup"><span data-stu-id="e353c-342">This means the asset was served directly from the POP to the Client.</span></span>               | <span data-ttu-id="e353c-343">Tak</span><span class="sxs-lookup"><span data-stu-id="e353c-343">Yes</span></span>  |<span data-ttu-id="e353c-344">Nie</span><span class="sxs-lookup"><span data-stu-id="e353c-344">No</span></span>   |
| <span data-ttu-id="e353c-345">RequestCountCacheMiss</span><span class="sxs-lookup"><span data-stu-id="e353c-345">RequestCountCacheMiss</span></span> | <span data-ttu-id="e353c-346">Liczba wszystkich żądań, które spowodowało w Chybienie pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="e353c-346">Count of all requests that resulted in a Cache Miss.</span></span> <span data-ttu-id="e353c-347">Oznacza to zasób nie został znaleziony na POP najbliżej klienta i w związku z tym nie została pobrana z punktu początkowego.</span><span class="sxs-lookup"><span data-stu-id="e353c-347">This means the asset was not found on the POP closest to the client, and therefore was retrieved from the Origin.</span></span>              |<span data-ttu-id="e353c-348">Tak</span><span class="sxs-lookup"><span data-stu-id="e353c-348">Yes</span></span>   | <span data-ttu-id="e353c-349">Nie</span><span class="sxs-lookup"><span data-stu-id="e353c-349">No</span></span>  |
| <span data-ttu-id="e353c-350">RequestCountCacheNoCache</span><span class="sxs-lookup"><span data-stu-id="e353c-350">RequestCountCacheNoCache</span></span> | <span data-ttu-id="e353c-351">Liczba wszystkich żądań do zasobu, uniemożliwiających w pamięci podręcznej z powodu konfiguracji użytkownika na krawędzi.</span><span class="sxs-lookup"><span data-stu-id="e353c-351">Count of all requests to an asset that are prevented from being cached due to a user configuration on the edge.</span></span>              |<span data-ttu-id="e353c-352">Tak</span><span class="sxs-lookup"><span data-stu-id="e353c-352">Yes</span></span>   | <span data-ttu-id="e353c-353">Nie</span><span class="sxs-lookup"><span data-stu-id="e353c-353">No</span></span>  |
| <span data-ttu-id="e353c-354">RequestCountCacheUncacheable</span><span class="sxs-lookup"><span data-stu-id="e353c-354">RequestCountCacheUncacheable</span></span> | <span data-ttu-id="e353c-355">Liczba wszystkich żądań do zasobów, które uniemożliwiały buforowana przez Cache-Control elementu zawartości i nagłówków wygasa, wskazujące, że go mają nie być buforowane punktu obecności lub przez klienta protokołu HTTP</span><span class="sxs-lookup"><span data-stu-id="e353c-355">Count of all requests to assets that are prevented from being cached by the asset's Cache-Control and Expires headers, which indicate that it should not be cached on a POP or by the HTTP client</span></span>                |<span data-ttu-id="e353c-356">Tak</span><span class="sxs-lookup"><span data-stu-id="e353c-356">Yes</span></span>   |<span data-ttu-id="e353c-357">Nie</span><span class="sxs-lookup"><span data-stu-id="e353c-357">No</span></span>   |
| <span data-ttu-id="e353c-358">RequestCountCacheOthers</span><span class="sxs-lookup"><span data-stu-id="e353c-358">RequestCountCacheOthers</span></span> | <span data-ttu-id="e353c-359">Liczba wszystkich żądań o stanie pamięci podręcznej nie jest objęty przez powyżej.</span><span class="sxs-lookup"><span data-stu-id="e353c-359">Count of all requests with cache status not covered by above.</span></span>              |<span data-ttu-id="e353c-360">Tak</span><span class="sxs-lookup"><span data-stu-id="e353c-360">Yes</span></span>   | <span data-ttu-id="e353c-361">Nie</span><span class="sxs-lookup"><span data-stu-id="e353c-361">No</span></span>  |
| <span data-ttu-id="e353c-362">EgressTotal</span><span class="sxs-lookup"><span data-stu-id="e353c-362">EgressTotal</span></span> | <span data-ttu-id="e353c-363">Transfer danych wychodzących w GB</span><span class="sxs-lookup"><span data-stu-id="e353c-363">Outbound data transfer in GB</span></span>              |<span data-ttu-id="e353c-364">Tak</span><span class="sxs-lookup"><span data-stu-id="e353c-364">Yes</span></span>   |<span data-ttu-id="e353c-365">Tak</span><span class="sxs-lookup"><span data-stu-id="e353c-365">Yes</span></span>   |
| <span data-ttu-id="e353c-366">EgressHttpStatus2xx</span><span class="sxs-lookup"><span data-stu-id="e353c-366">EgressHttpStatus2xx</span></span> | <span data-ttu-id="e353c-367">Danych wychodzących transfer * odpowiedzi z kodów stanu HTTP 2xx w GB</span><span class="sxs-lookup"><span data-stu-id="e353c-367">Outbound data transfer* for responses with 2xx HTTP status codes in GB</span></span>            |<span data-ttu-id="e353c-368">Tak</span><span class="sxs-lookup"><span data-stu-id="e353c-368">Yes</span></span>   |<span data-ttu-id="e353c-369">Nie</span><span class="sxs-lookup"><span data-stu-id="e353c-369">No</span></span>   |
| <span data-ttu-id="e353c-370">EgressHttpStatus3xx</span><span class="sxs-lookup"><span data-stu-id="e353c-370">EgressHttpStatus3xx</span></span> | <span data-ttu-id="e353c-371">Transfer danych wychodzących dla odpowiedzi z kodów stanu HTTP 3xx w GB</span><span class="sxs-lookup"><span data-stu-id="e353c-371">Outbound data transfer for responses with 3xx HTTP status codes in GB</span></span>              |<span data-ttu-id="e353c-372">Tak</span><span class="sxs-lookup"><span data-stu-id="e353c-372">Yes</span></span>   |<span data-ttu-id="e353c-373">Nie</span><span class="sxs-lookup"><span data-stu-id="e353c-373">No</span></span>   |
| <span data-ttu-id="e353c-374">EgressHttpStatus4xx</span><span class="sxs-lookup"><span data-stu-id="e353c-374">EgressHttpStatus4xx</span></span> | <span data-ttu-id="e353c-375">Transfer danych wychodzących dla odpowiedzi z kodów stanu HTTP 4xx w GB</span><span class="sxs-lookup"><span data-stu-id="e353c-375">Outbound data transfer for responses with 4xx HTTP status codes in GB</span></span>               |<span data-ttu-id="e353c-376">Tak</span><span class="sxs-lookup"><span data-stu-id="e353c-376">Yes</span></span>   | <span data-ttu-id="e353c-377">Nie</span><span class="sxs-lookup"><span data-stu-id="e353c-377">No</span></span>  |
| <span data-ttu-id="e353c-378">EgressHttpStatus5xx</span><span class="sxs-lookup"><span data-stu-id="e353c-378">EgressHttpStatus5xx</span></span> | <span data-ttu-id="e353c-379">Transfer danych wychodzących dla odpowiedzi z kodów stanu HTTP 5xx w GB</span><span class="sxs-lookup"><span data-stu-id="e353c-379">Outbound data transfer for responses with 5xx HTTP status codes in GB</span></span>               |<span data-ttu-id="e353c-380">Tak</span><span class="sxs-lookup"><span data-stu-id="e353c-380">Yes</span></span>   |  <span data-ttu-id="e353c-381">Nie</span><span class="sxs-lookup"><span data-stu-id="e353c-381">No</span></span> |
| <span data-ttu-id="e353c-382">EgressHttpStatusOthers</span><span class="sxs-lookup"><span data-stu-id="e353c-382">EgressHttpStatusOthers</span></span> | <span data-ttu-id="e353c-383">Transfer danych wychodzących dla odpowiedzi o innych kodach stanów HTTP w GB</span><span class="sxs-lookup"><span data-stu-id="e353c-383">Outbound data transfer for responses with other HTTP status codes in GB</span></span>                |<span data-ttu-id="e353c-384">Tak</span><span class="sxs-lookup"><span data-stu-id="e353c-384">Yes</span></span>   |<span data-ttu-id="e353c-385">Nie</span><span class="sxs-lookup"><span data-stu-id="e353c-385">No</span></span>   |
| <span data-ttu-id="e353c-386">EgressCacheHit</span><span class="sxs-lookup"><span data-stu-id="e353c-386">EgressCacheHit</span></span> |  <span data-ttu-id="e353c-387">Transfer danych wychodzących dla odpowiedzi, które zostały dostarczone bezpośrednio z pamięci podręcznej CDN CDN POP/krawędzi</span><span class="sxs-lookup"><span data-stu-id="e353c-387">Outbound data transfer for responses that were delivered directly from the CDN cache on the CDN POPs/Edges</span></span>  |<span data-ttu-id="e353c-388">Tak</span><span class="sxs-lookup"><span data-stu-id="e353c-388">Yes</span></span>   |  <span data-ttu-id="e353c-389">Nie</span><span class="sxs-lookup"><span data-stu-id="e353c-389">No</span></span> |
| <span data-ttu-id="e353c-390">EgressCacheMiss</span><span class="sxs-lookup"><span data-stu-id="e353c-390">EgressCacheMiss</span></span> | <span data-ttu-id="e353c-391">Transfer danych wychodzących dla odpowiedzi, które nie zostały znalezione na najbliższy serwer protokołu POP i pobrać z serwera pochodzenia</span><span class="sxs-lookup"><span data-stu-id="e353c-391">Outbound data transfer for responses that were not found on the nearest POP server, and retrieved from the origin server</span></span>              |<span data-ttu-id="e353c-392">Tak</span><span class="sxs-lookup"><span data-stu-id="e353c-392">Yes</span></span>   |  <span data-ttu-id="e353c-393">Nie</span><span class="sxs-lookup"><span data-stu-id="e353c-393">No</span></span> |
| <span data-ttu-id="e353c-394">EgressCacheNoCache</span><span class="sxs-lookup"><span data-stu-id="e353c-394">EgressCacheNoCache</span></span> | <span data-ttu-id="e353c-395">Transfer danych wychodzących dla zasobów, które uniemożliwiały pamięci podręcznej z powodu konfiguracji użytkownika na krawędzi.</span><span class="sxs-lookup"><span data-stu-id="e353c-395">Outbound data transfer for assets that are prevented from being cached due to a user configuration on the edge.</span></span>                |<span data-ttu-id="e353c-396">Tak</span><span class="sxs-lookup"><span data-stu-id="e353c-396">Yes</span></span>   |<span data-ttu-id="e353c-397">Nie</span><span class="sxs-lookup"><span data-stu-id="e353c-397">No</span></span>   |
| <span data-ttu-id="e353c-398">EgressCacheUncacheable</span><span class="sxs-lookup"><span data-stu-id="e353c-398">EgressCacheUncacheable</span></span> | <span data-ttu-id="e353c-399">Transfer danych wychodzących dla zasobów, które nie będą mogli buforowana przez Cache-Control elementu zawartości i/lub Expires nagłówków, wskazujące, że go mają nie być buforowane punktu obecności lub przez klienta HTTP</span><span class="sxs-lookup"><span data-stu-id="e353c-399">Outbound data transfer for assets that are prevented from being cached by the asset's Cache-Control and/or Expires headers, which indicate that it should not be cached on a POP or by the HTTP client</span></span>                    |<span data-ttu-id="e353c-400">Tak</span><span class="sxs-lookup"><span data-stu-id="e353c-400">Yes</span></span>   | <span data-ttu-id="e353c-401">Nie</span><span class="sxs-lookup"><span data-stu-id="e353c-401">No</span></span>  |
| <span data-ttu-id="e353c-402">EgressCacheOthers</span><span class="sxs-lookup"><span data-stu-id="e353c-402">EgressCacheOthers</span></span> |  <span data-ttu-id="e353c-403">Transfery danych wychodzących w innych sytuacjach pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="e353c-403">Outbound data transfers for other cache scenarios.</span></span>             |<span data-ttu-id="e353c-404">Tak</span><span class="sxs-lookup"><span data-stu-id="e353c-404">Yes</span></span>   | <span data-ttu-id="e353c-405">Nie</span><span class="sxs-lookup"><span data-stu-id="e353c-405">No</span></span>  |

<span data-ttu-id="e353c-406">* Transfer danych wychodzących odwołuje się do ruchu dostarczane z serwerów POP w sieci CDN do klienta.</span><span class="sxs-lookup"><span data-stu-id="e353c-406">*Outbound data transfer refers to traffic delivered from CDN POP servers to the client.</span></span>


### <a name="schema-of-the-core-analytics-logs"></a><span data-ttu-id="e353c-407">Schemat Core analizy dzienników</span><span class="sxs-lookup"><span data-stu-id="e353c-407">Schema of the Core Analytics Logs</span></span> 

<span data-ttu-id="e353c-408">Wszystkie dzienniki są przechowywane w formacie JSON i każdy wpis ma następujące pola ciągu poniżej schematu:</span><span class="sxs-lookup"><span data-stu-id="e353c-408">All logs are stored in JSON format and each entry has string fields following the below schema:</span></span>

```json
    "records": [
        {
            "time": "2017-04-27T01:00:00",
            "resourceId": "<ARM Resource Id of the CDN Endpoint>",
            "operationName": "Microsoft.Cdn/profiles/endpoints/contentDelivery",
            "category": "CoreAnalytics",
            "properties": {
                "DomainName": "<Name of the domain for which the statistics is reported>",
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

<span data-ttu-id="e353c-409">Gdzie "czas" oznacza czas rozpoczęcia granic godzinę, dla którego jest raportowane dane statystyczne.</span><span class="sxs-lookup"><span data-stu-id="e353c-409">Where the ‘time’ represents the start time of the hour boundary for which the statistics is reported.</span></span> <span data-ttu-id="e353c-410">Gdy metryki nie jest obsługiwany przez dostawcę sieci CDN w warstwie, a nie wartość o podwójnej precyzji lub liczba całkowita będzie być wartość null.</span><span class="sxs-lookup"><span data-stu-id="e353c-410">When a metric is not supported by a CDN provider, instead of a double or integer value, there will be a null value.</span></span> <span data-ttu-id="e353c-411">Tej wartości null wskazuje brak metrykę, a ta różni się od wartości 0.</span><span class="sxs-lookup"><span data-stu-id="e353c-411">This null value indicates the absence of a metric, and this is different from a 0 value.</span></span> <span data-ttu-id="e353c-412">Należy również zauważyć, że będą istnieć jeden zestaw te metryki dla domeny skonfigurowany w punkcie końcowym.</span><span class="sxs-lookup"><span data-stu-id="e353c-412">Also note that there will be one set of these metrics per domain configured on the endpoint.</span></span>

<span data-ttu-id="e353c-413">Właściwości przykładzie poniżej:</span><span class="sxs-lookup"><span data-stu-id="e353c-413">Example properties below:</span></span>

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

## <a name="additional-resources"></a><span data-ttu-id="e353c-414">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="e353c-414">Additional resources</span></span>

* [<span data-ttu-id="e353c-415">Dzienniki diagnostyczne platformy Azure</span><span class="sxs-lookup"><span data-stu-id="e353c-415">Azure Diagnostic logs</span></span>](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs)
* [<span data-ttu-id="e353c-416">Podstawowa analiza uzupełniające portalu usługi Azure CDN</span><span class="sxs-lookup"><span data-stu-id="e353c-416">Core analytics via Azure CDN supplemental portal</span></span>](https://docs.microsoft.com/azure/cdn/cdn-analyze-usage-patterns)
* [<span data-ttu-id="e353c-417">Analiza dzienników Azure OMS</span><span class="sxs-lookup"><span data-stu-id="e353c-417">Azure OMS Log Analytics</span></span>](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-overview)
* [<span data-ttu-id="e353c-418">Analiza dzienników Azure interfejsu API REST</span><span class="sxs-lookup"><span data-stu-id="e353c-418">Azure Log Analytics REST API</span></span>](https://docs.microsoft.com/en-us/rest/api/loganalytics)







