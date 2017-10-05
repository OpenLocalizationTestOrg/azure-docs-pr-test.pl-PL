---
title: "Przegląd dzienników diagnostycznych platformy Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, co to są dzienników diagnostycznych platformy Azure i jak ich używać zrozumienie zdarzenia występujące w obrębie zasobów platformy Azure."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: fe8887df-b0e6-46f8-b2c0-11994d28e44f
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: johnkem; magoedte
ms.openlocfilehash: d59abde29fc7b73a799e5bf3659b02f824b693de
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="collect-and-consume-log-data-from-your-azure-resources"></a><span data-ttu-id="6c01e-103">Zbierania i wykorzystywania danych dziennika z zasobów platformy Azure</span><span class="sxs-lookup"><span data-stu-id="6c01e-103">Collect and consume log data from your Azure resources</span></span>

## <a name="what-are-azure-resource-diagnostic-logs"></a><span data-ttu-id="6c01e-104">Co to są dzienniki diagnostyczne zasobów platformy Azure</span><span class="sxs-lookup"><span data-stu-id="6c01e-104">What are Azure resource diagnostic logs</span></span>
<span data-ttu-id="6c01e-105">**Azure dzienników diagnostycznych poziom zasobów** są dzienniki emitowane przez zasób, które zawierają rozbudowane, często dane dotyczące operacji tego zasobu.</span><span class="sxs-lookup"><span data-stu-id="6c01e-105">**Azure resource-level diagnostic logs** are logs emitted by a resource that provide rich, frequent data about the operation of that resource.</span></span> <span data-ttu-id="6c01e-106">Zawartość tych dzienników zależy od typu zasobu.</span><span class="sxs-lookup"><span data-stu-id="6c01e-106">The content of these logs varies by resource type.</span></span> <span data-ttu-id="6c01e-107">Na przykład liczników reguły grupy zabezpieczeń sieci i usługi Key Vault inspekcje są dwie kategorie dzienników zasobów.</span><span class="sxs-lookup"><span data-stu-id="6c01e-107">For example, Network Security Group rule counters and Key Vault audits are two categories of resource logs.</span></span>

<span data-ttu-id="6c01e-108">Dzienniki diagnostyczne poziom zasobów różnią się od [dziennik aktywności](monitoring-overview-activity-logs.md).</span><span class="sxs-lookup"><span data-stu-id="6c01e-108">Resource-level diagnostic logs differ from the [Activity Log](monitoring-overview-activity-logs.md).</span></span> <span data-ttu-id="6c01e-109">Dziennik aktywności zapewnia wgląd w operacje wykonywane na zasobów w ramach subskrypcji, za pomocą Menedżera zasobów, na przykład tworzenia maszyny wirtualnej lub usuwanie aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="6c01e-109">The Activity Log provides insight into the operations that were performed on resources in your subscription using Resource Manager, for example, creating a virtual machine or deleting a logic app.</span></span> <span data-ttu-id="6c01e-110">Dziennik aktywności jest dziennika poziomu subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="6c01e-110">The Activity Log is a subscription-level log.</span></span> <span data-ttu-id="6c01e-111">Dzienniki diagnostyczne poziom zasobów zapewniają wgląd w operacji wykonanych w ramach tego zasobu, na przykład pobierania klucza tajnego z magazynu kluczy.</span><span class="sxs-lookup"><span data-stu-id="6c01e-111">Resource-level diagnostic logs provide insight into operations that were performed within that resource itself, for example, getting a secret from a Key Vault.</span></span>

<span data-ttu-id="6c01e-112">Dzienniki diagnostyczne poziom zasobów również różnią się od dzienników diagnostycznych na poziomie systemu operacyjnego gościa.</span><span class="sxs-lookup"><span data-stu-id="6c01e-112">Resource-level diagnostic logs also differ from guest OS-level diagnostic logs.</span></span> <span data-ttu-id="6c01e-113">Dzienniki diagnostyczne systemu operacyjnego gościa znajdują się te zebranych przez agenta, które działają w ramach maszyny wirtualnej lub inne obsługiwane typu zasobu.</span><span class="sxs-lookup"><span data-stu-id="6c01e-113">Guest OS diagnostic logs are those collected by an agent running inside of a virtual machine or other supported resource type.</span></span> <span data-ttu-id="6c01e-114">Poziom zasobów dzienników diagnostycznych wymagają żadne dane specyficzne dla zasobów agenta do przechwycenia z platformą Azure, podczas dzienników diagnostycznych na poziomie systemu operacyjnego gościa przechwycenia danych z systemu operacyjnego i aplikacji uruchomionych na maszynie wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="6c01e-114">Resource-level diagnostic logs require no agent and capture resource-specific data from the Azure platform itself, while guest OS-level diagnostic logs capture data from the operating system and applications running on a virtual machine.</span></span>

<span data-ttu-id="6c01e-115">Nie wszystkie zasoby obsługi nowego typu zasobu dzienników diagnostycznych opisanych tutaj.</span><span class="sxs-lookup"><span data-stu-id="6c01e-115">Not all resources support the new type of resource diagnostic logs described here.</span></span> <span data-ttu-id="6c01e-116">Ten artykuł zawiera listę typów zasobów, które obsługują nowe dzienniki diagnostyczne zasobów na poziomie sekcji.</span><span class="sxs-lookup"><span data-stu-id="6c01e-116">This article contains a section listing which resource types support the new resource-level diagnostic logs.</span></span>

![<span data-ttu-id="6c01e-117">Diagnostyka zasobów rejestruje vs innych typów dzienników</span><span class="sxs-lookup"><span data-stu-id="6c01e-117">Resource diagnostics logs vs other types of logs</span></span> ](./media/monitoring-overview-of-diagnostic-logs/Diagnostics_Logs_vs_other_logs_v5.png)

## <a name="what-you-can-do-with-resource-level-diagnostic-logs"></a><span data-ttu-id="6c01e-118">Co należy zrobić z dzienników diagnostycznych poziom zasobów</span><span class="sxs-lookup"><span data-stu-id="6c01e-118">What you can do with resource-level diagnostic logs</span></span>
<span data-ttu-id="6c01e-119">Poniżej podano niektóre czynności, które można wykonywać z dzienników diagnostycznych zasobu:</span><span class="sxs-lookup"><span data-stu-id="6c01e-119">Here are some of the things you can do with resource diagnostic logs:</span></span>

![Logiczne umieszczania dzienników diagnostycznych zasobu](./media/monitoring-overview-of-diagnostic-logs/Diagnostics_Logs_Actions.png)


* <span data-ttu-id="6c01e-121">Zapisywanie ich [ **konta magazynu** ](monitoring-archive-diagnostic-logs.md) inspekcji inspekcji lub ręcznie.</span><span class="sxs-lookup"><span data-stu-id="6c01e-121">Save them to a [**Storage Account**](monitoring-archive-diagnostic-logs.md) for auditing or manual inspection.</span></span> <span data-ttu-id="6c01e-122">Można określić za pomocą czasu (w dniach) przechowywania **ustawień diagnostycznych zasobu**.</span><span class="sxs-lookup"><span data-stu-id="6c01e-122">You can specify the retention time (in days) using **resource diagnostic settings**.</span></span>
* <span data-ttu-id="6c01e-123">[Do strumienia **usługi Event Hubs** ](monitoring-stream-diagnostic-logs-to-event-hubs.md) dla wprowadzanie przez usługi innej firmy lub rozwiązania analizy niestandardowych, takich jak usługi Power BI.</span><span class="sxs-lookup"><span data-stu-id="6c01e-123">[Stream them to **Event Hubs**](monitoring-stream-diagnostic-logs-to-event-hubs.md) for ingestion by a third-party service or custom analytics solution such as PowerBI.</span></span>
* <span data-ttu-id="6c01e-124">Analizuj je za pomocą [OMS analizy dzienników](../log-analytics/log-analytics-azure-storage.md)</span><span class="sxs-lookup"><span data-stu-id="6c01e-124">Analyze them with [OMS Log Analytics](../log-analytics/log-analytics-azure-storage.md)</span></span>

<span data-ttu-id="6c01e-125">Można użyć konta magazynu lub przestrzeni nazw usługi Event Hubs, która nie znajduje się w tej samej subskrypcji co jeden emitowanie dzienników.</span><span class="sxs-lookup"><span data-stu-id="6c01e-125">You can use a storage account or Event Hubs namespace that is not in the same subscription as the one emitting logs.</span></span> <span data-ttu-id="6c01e-126">Użytkownik, który konfiguruje ustawienie musi mieć odpowiedni dostęp RBAC do obu subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="6c01e-126">The user who configures the setting must have the appropriate RBAC access to both subscriptions.</span></span>

## <a name="resource-diagnostic-settings"></a><span data-ttu-id="6c01e-127">Ustawienia diagnostyczne zasobu</span><span class="sxs-lookup"><span data-stu-id="6c01e-127">Resource diagnostic settings</span></span>
<span data-ttu-id="6c01e-128">Dzienniki diagnostyczne zasobu z systemem innym niż — obliczeń się, że zasoby są skonfigurowane przy użyciu ustawień diagnostycznych zasobu.</span><span class="sxs-lookup"><span data-stu-id="6c01e-128">Resource diagnostic logs for non-Compute resources are configured using resource diagnostic settings.</span></span> <span data-ttu-id="6c01e-129">**Ustawienia diagnostyczne zasobu** formantów zasobów:</span><span class="sxs-lookup"><span data-stu-id="6c01e-129">**Resource diagnostic settings** for a resource control:</span></span>

* <span data-ttu-id="6c01e-130">W przypadku dzienników diagnostycznych zasobu i metryki wysyłania (konto magazynu, centra zdarzeń i/lub analizy dzienników OMS).</span><span class="sxs-lookup"><span data-stu-id="6c01e-130">Where resource diagnostic logs and metrics are sent (Storage Account, Event Hubs, and/or OMS Log Analytics).</span></span>
* <span data-ttu-id="6c01e-131">Kategorie dziennika, które są wysyłane i czy dane są także wysyłane.</span><span class="sxs-lookup"><span data-stu-id="6c01e-131">Which log categories are sent and whether metric data is also sent.</span></span>
* <span data-ttu-id="6c01e-132">Jak długo każdej kategorii dziennika powinny zostać zachowane na koncie magazynu</span><span class="sxs-lookup"><span data-stu-id="6c01e-132">How long each log category should be retained in a storage account</span></span>
    - <span data-ttu-id="6c01e-133">Przechowywanie 0 oznacza, że dzienniki są przechowywane w nieskończoność.</span><span class="sxs-lookup"><span data-stu-id="6c01e-133">A retention of zero days means logs are kept forever.</span></span> <span data-ttu-id="6c01e-134">W przeciwnym razie wartość może być dowolną liczbę dni od 1 do 2147483647.</span><span class="sxs-lookup"><span data-stu-id="6c01e-134">Otherwise, the value can be any number of days between 1 and 2147483647.</span></span>
    - <span data-ttu-id="6c01e-135">Jeśli zasady przechowywania są skonfigurowane, ale przechowywanie dzienniki na koncie magazynu jest wyłączone (na przykład, jeśli tylko opcje usługi Event Hubs lub OMS są zaznaczone), zasad przechowywania nie obowiązują.</span><span class="sxs-lookup"><span data-stu-id="6c01e-135">If retention policies are set but storing logs in a Storage Account is disabled (for example, if only Event Hubs or OMS options are selected), the retention policies have no effect.</span></span>
    - <span data-ttu-id="6c01e-136">Zasady przechowywania są zastosowane na dni, więc pod koniec dnia (UTC), dzienniki od dnia, która jest teraz poza przechowywania zasad są usuwane.</span><span class="sxs-lookup"><span data-stu-id="6c01e-136">Retention policies are applied per-day, so at the end of a day (UTC), logs from the day that is now beyond the retention policy are deleted.</span></span> <span data-ttu-id="6c01e-137">Na przykład jeśli masz zasady przechowywania jeden dzień na początku dnia dzisiaj dzienniki na wczoraj zanim dzień zostaną usunięte.</span><span class="sxs-lookup"><span data-stu-id="6c01e-137">For example, if you had a retention policy of one day, at the beginning of the day today the logs from the day before yesterday would be deleted.</span></span>

<span data-ttu-id="6c01e-138">Te ustawienia można łatwo skonfigurować za pomocą ustawień diagnostycznych dla zasobu w portalu Azure, za pomocą programu Azure PowerShell i polecenia interfejsu wiersza polecenia lub za pośrednictwem [interfejsu API REST Monitor Azure](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span><span class="sxs-lookup"><span data-stu-id="6c01e-138">These settings are easily configured via the diagnostic settings for a resource in the Azure portal, via Azure PowerShell and CLI commands, or via the [Azure Monitor REST API](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span></span>

> [!WARNING]
> <span data-ttu-id="6c01e-139">Dzienniki diagnostyczne i metryki z warstwy systemu operacyjnego gościa użycia zasobów (na przykład maszyny wirtualne lub sieci szkieletowej usług) obliczeń [odrębny mechanizm konfiguracji i wybór wyjścia](../azure-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="6c01e-139">Diagnostic logs and metrics for from the guest OS layer of Compute resources (for example, VMs or Service Fabric) use [a separate mechanism for configuration and selection of outputs](../azure-diagnostics.md).</span></span>
>
>

## <a name="how-to-enable-collection-of-resource-diagnostic-logs"></a><span data-ttu-id="6c01e-140">Jak włączyć kolekcję dzienników diagnostycznych zasobu</span><span class="sxs-lookup"><span data-stu-id="6c01e-140">How to enable collection of resource diagnostic logs</span></span>
<span data-ttu-id="6c01e-141">Można włączyć zbierania dzienników diagnostycznych zasobu [podczas tworzenia zasobu w szablonie usługi Resource Manager](./monitoring-enable-diagnostic-logs-using-template.md) lub po utworzeniu zasobu ze strony tego zasobu w portalu.</span><span class="sxs-lookup"><span data-stu-id="6c01e-141">Collection of resource diagnostic logs can be enabled [as part of creating a resource in a Resource Manager template](./monitoring-enable-diagnostic-logs-using-template.md) or after a resource is created from that resource's page in the portal.</span></span> <span data-ttu-id="6c01e-142">Można również włączyć kolekcji w dowolnym momencie za pomocą poleceń programu Azure PowerShell lub interfejsu wiersza polecenia lub interfejsu API REST Azure monitora.</span><span class="sxs-lookup"><span data-stu-id="6c01e-142">You can also enable collection at any point using Azure PowerShell or CLI commands, or using the Azure Monitor REST API.</span></span>

> [!TIP]
> <span data-ttu-id="6c01e-143">Te instrukcje nie może zastosować bezpośrednio do każdego zasobu.</span><span class="sxs-lookup"><span data-stu-id="6c01e-143">These instructions may not apply directly to every resource.</span></span> <span data-ttu-id="6c01e-144">Skorzystaj z łączy schematu u dołu tej strony, aby zrozumieć specjalne kroki, które mogą być zastosowane do określonych typów zasobów.</span><span class="sxs-lookup"><span data-stu-id="6c01e-144">See the schema links at the bottom of this page to understand special steps that may apply to certain resource types.</span></span>
>
>

### <a name="enable-collection-of-resource-diagnostic-logs-in-the-portal"></a><span data-ttu-id="6c01e-145">Włącz zbieranie dzienników diagnostycznych zasobu w portalu</span><span class="sxs-lookup"><span data-stu-id="6c01e-145">Enable collection of resource diagnostic logs in the portal</span></span>
<span data-ttu-id="6c01e-146">Po utworzeniu zasobu, przechodząc do określonego zasobu lub przechodząc do monitora Azure, można włączyć zbierania dzienników diagnostycznych zasobu w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="6c01e-146">You can enable collection of resource diagnostic logs in the Azure portal after a resource has been created either by going to a specific resource or by navigating to Azure Monitor.</span></span> <span data-ttu-id="6c01e-147">Aby je włączyć za pomocą monitora Azure:</span><span class="sxs-lookup"><span data-stu-id="6c01e-147">To enable this via Azure Monitor:</span></span>

1. <span data-ttu-id="6c01e-148">W [portalu Azure](http://portal.azure.com), przejdź do monitora Azure i kliknij na **ustawień diagnostycznych**</span><span class="sxs-lookup"><span data-stu-id="6c01e-148">In the [Azure portal](http://portal.azure.com), navigate to Azure Monitor and click on **Diagnostic Settings**</span></span>

    ![Monitorowanie sekcji Azure Monitor](media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-blade.png)

2. <span data-ttu-id="6c01e-150">Opcjonalnie Filtruj listę według grupy zasobów lub typ zasobu, a następnie kliknij na zasobie, dla której chcesz skonfigurować ustawienie diagnostyczne.</span><span class="sxs-lookup"><span data-stu-id="6c01e-150">Optionally filter the list by resource group or resource type, then click on the resource for which you would like to set a diagnostic setting.</span></span>

3. <span data-ttu-id="6c01e-151">Jeśli nie istnieją żadne ustawienia zasobu wybrany, zostanie wyświetlony monit, aby utworzyć ustawienie.</span><span class="sxs-lookup"><span data-stu-id="6c01e-151">If no settings exist on the resource you have selected, you are prompted to create a setting.</span></span> <span data-ttu-id="6c01e-152">Kliknij pozycję "Włącz diagnostykę."</span><span class="sxs-lookup"><span data-stu-id="6c01e-152">Click "Turn on diagnostics."</span></span>

   ![Dodaj ustawienie diagnostyczne - żadnych istniejących ustawień](media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-none.png)

   <span data-ttu-id="6c01e-154">W przypadku istniejących ustawień na zasobie, zostanie wyświetlona lista ustawień już skonfigurowana dla tego zasobu.</span><span class="sxs-lookup"><span data-stu-id="6c01e-154">If there are existing settings on the resource, you will see a list of settings already configured on this resource.</span></span> <span data-ttu-id="6c01e-155">Kliknij przycisk "Dodaj ustawienie diagnostyczne".</span><span class="sxs-lookup"><span data-stu-id="6c01e-155">Click "Add diagnostic setting."</span></span>

   ![Dodaj ustawienie diagnostyczne — istniejące ustawienia](media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-multiple.png)

3. <span data-ttu-id="6c01e-157">Sprawdź pola dla każdej lokalizacji docelowej, do którego chcesz wysyłać dane i skonfigurować, którego zasobu jest używana dla każdej lokalizacji docelowej, nadaj nazwę ustawienia.</span><span class="sxs-lookup"><span data-stu-id="6c01e-157">Give your setting a name, check the boxes for each destination to which you would like to send data, and configure which resource is used for each destination.</span></span> <span data-ttu-id="6c01e-158">Opcjonalnie można ustawić liczbę dni, aby zachować te dzienniki przy użyciu **przechowywania (dni)** suwaki (dotyczy tylko miejsce docelowe konto magazynu).</span><span class="sxs-lookup"><span data-stu-id="6c01e-158">Optionally, set a number of days to retain these logs by using the **Retention (days)** sliders (only applicable to the storage account destination).</span></span> <span data-ttu-id="6c01e-159">Przechowywanie zero dni są przechowywane dzienniki nieskończoność.</span><span class="sxs-lookup"><span data-stu-id="6c01e-159">A retention of zero days stores the logs indefinitely.</span></span>
   
   ![Dodaj ustawienie diagnostyczne — istniejące ustawienia](media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-configure.png)
    
4. <span data-ttu-id="6c01e-161">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="6c01e-161">Click **Save**.</span></span>

<span data-ttu-id="6c01e-162">Po kilku chwilach nowe ustawienie jest wyświetlane na liście ustawień dla tego zasobu, a dzienników diagnostycznych są wysyłane do określonego miejsca docelowe zaraz po wygenerowaniu nowych danych zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="6c01e-162">After a few moments, the new setting appears in your list of settings for this resource, and diagnostic logs are sent to the specified destinations as soon as new event data is generated.</span></span>

### <a name="enable-collection-of-resource-diagnostic-logs-via-powershell"></a><span data-ttu-id="6c01e-163">Włącz zbieranie dzienników diagnostycznych zasobów za pomocą programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="6c01e-163">Enable collection of resource diagnostic logs via PowerShell</span></span>
<span data-ttu-id="6c01e-164">Aby włączyć zbieranie dzienników diagnostycznych zasobów za pomocą programu Azure PowerShell, użyj następujących poleceń:</span><span class="sxs-lookup"><span data-stu-id="6c01e-164">To enable collection of resource diagnostic logs via Azure PowerShell, use the following commands:</span></span>

<span data-ttu-id="6c01e-165">Aby włączyć magazyn dzienników diagnostycznych na konto magazynu, należy użyć tego polecenia:</span><span class="sxs-lookup"><span data-stu-id="6c01e-165">To enable storage of diagnostic logs in a storage account, use this command:</span></span>

```powershell
Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -StorageAccountId [your storage account id] -Enabled $true
```

<span data-ttu-id="6c01e-166">Identyfikator konta magazynu jest identyfikator zasobu dla konta magazynu, do którego chcesz wysłać dzienniki.</span><span class="sxs-lookup"><span data-stu-id="6c01e-166">The storage account ID is the resource ID for the storage account to which you want to send the logs.</span></span>

<span data-ttu-id="6c01e-167">Do przesyłania strumieniowego dzienników diagnostycznych do Centrum zdarzeń, użyj tego polecenia:</span><span class="sxs-lookup"><span data-stu-id="6c01e-167">To enable streaming of diagnostic logs to an event hub, use this command:</span></span>

```powershell
Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -ServiceBusRuleId [your Service Bus rule id] -Enabled $true
```

<span data-ttu-id="6c01e-168">Identyfikator reguły magistrali usług jest ciąg w formacie: `{Service Bus resource ID}/authorizationrules/{key name}`.</span><span class="sxs-lookup"><span data-stu-id="6c01e-168">The service bus rule ID is a string with this format: `{Service Bus resource ID}/authorizationrules/{key name}`.</span></span>

<span data-ttu-id="6c01e-169">Aby włączyć wysyłanie dzienników diagnostycznych do obszaru roboczego analizy dzienników, użyj tego polecenia:</span><span class="sxs-lookup"><span data-stu-id="6c01e-169">To enable sending of diagnostic logs to a Log Analytics workspace, use this command:</span></span>

```powershell
Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -WorkspaceId [resource id of the log analytics workspace] -Enabled $true
```

<span data-ttu-id="6c01e-170">Można uzyskać Identyfikatora zasobu obszaru roboczego analizy dzienników przy użyciu następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="6c01e-170">You can obtain the resource ID of your Log Analytics workspace using the following command:</span></span>

```powershell
(Get-AzureRmOperationalInsightsWorkspace).ResourceId
```

<span data-ttu-id="6c01e-171">Można połączyć tych parametrów, aby włączyć wiele opcji danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="6c01e-171">You can combine these parameters to enable multiple output options.</span></span>

### <a name="enable-collection-of-resource-diagnostic-logs-via-cli"></a><span data-ttu-id="6c01e-172">Włącz zbieranie dzienników diagnostycznych zasobów za pomocą interfejsu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="6c01e-172">Enable collection of resource diagnostic logs via CLI</span></span>
<span data-ttu-id="6c01e-173">Aby włączyć zbieranie dzienników diagnostycznych zasobów za pomocą interfejsu wiersza polecenia Azure, użyj następujących poleceń:</span><span class="sxs-lookup"><span data-stu-id="6c01e-173">To enable collection of resource diagnostic logs via the Azure CLI, use the following commands:</span></span>

<span data-ttu-id="6c01e-174">Aby włączyć magazyn dzienników diagnostycznych na konto magazynu, należy użyć tego polecenia:</span><span class="sxs-lookup"><span data-stu-id="6c01e-174">To enable storage of diagnostic logs in a Storage Account, use this command:</span></span>

```azurecli
azure insights diagnostic set --resourceId <resourceId> --storageId <storageAccountId> --enabled true
```

<span data-ttu-id="6c01e-175">Identyfikator konta magazynu jest identyfikator zasobu dla konta magazynu, do którego chcesz wysłać dzienniki.</span><span class="sxs-lookup"><span data-stu-id="6c01e-175">The storage account ID is the resource ID for the storage account to which you want to send the logs.</span></span>

<span data-ttu-id="6c01e-176">Do przesyłania strumieniowego dzienników diagnostycznych do Centrum zdarzeń, użyj tego polecenia:</span><span class="sxs-lookup"><span data-stu-id="6c01e-176">To enable streaming of diagnostic logs to an event hub, use this command:</span></span>

```azurecli
azure insights diagnostic set --resourceId <resourceId> --serviceBusRuleId <serviceBusRuleId> --enabled true
```

<span data-ttu-id="6c01e-177">Identyfikator reguły magistrali usług jest ciąg w formacie: `{Service Bus resource ID}/authorizationrules/{key name}`.</span><span class="sxs-lookup"><span data-stu-id="6c01e-177">The service bus rule ID is a string with this format: `{Service Bus resource ID}/authorizationrules/{key name}`.</span></span>

<span data-ttu-id="6c01e-178">Aby włączyć wysyłanie dzienników diagnostycznych do obszaru roboczego analizy dzienników, użyj tego polecenia:</span><span class="sxs-lookup"><span data-stu-id="6c01e-178">To enable sending of diagnostic logs to a Log Analytics workspace, use this command:</span></span>

```azurecli
azure insights diagnostic set --resourceId <resourceId> --workspaceId <resource id of the log analytics workspace> --enabled true
```

<span data-ttu-id="6c01e-179">Można połączyć tych parametrów, aby włączyć wiele opcji danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="6c01e-179">You can combine these parameters to enable multiple output options.</span></span>

### <a name="enable-collection-of-resource-diagnostic-logs-via-rest-api"></a><span data-ttu-id="6c01e-180">Włącz zbieranie dzienników diagnostycznych zasobów za pomocą interfejsu API REST</span><span class="sxs-lookup"><span data-stu-id="6c01e-180">Enable collection of resource diagnostic logs via REST API</span></span>
<span data-ttu-id="6c01e-181">Aby zmienić ustawienia diagnostyki za pomocą interfejsu API REST Monitor Azure, zobacz [tego dokumentu](https://msdn.microsoft.com/library/azure/dn931931.aspx).</span><span class="sxs-lookup"><span data-stu-id="6c01e-181">To change diagnostic settings using the Azure Monitor REST API, see [this document](https://msdn.microsoft.com/library/azure/dn931931.aspx).</span></span>

## <a name="manage-resource-diagnostic-settings-in-the-portal"></a><span data-ttu-id="6c01e-182">Ustawienia diagnostyczne zasobu w portalu zarządzania</span><span class="sxs-lookup"><span data-stu-id="6c01e-182">Manage resource diagnostic settings in the portal</span></span>
<span data-ttu-id="6c01e-183">Upewnij się, że wszystkie zasoby zostały skonfigurowane przy użyciu ustawień diagnostycznych.</span><span class="sxs-lookup"><span data-stu-id="6c01e-183">Ensure that all of your resources are set up with diagnostic settings.</span></span> <span data-ttu-id="6c01e-184">Przejdź do **Monitor** w portalu i Otwórz **ustawień diagnostycznych**.</span><span class="sxs-lookup"><span data-stu-id="6c01e-184">Navigate to **Monitor** in the portal and open **Diagnostic settings**.</span></span>

![Diagnostycznych dzienników bloku w portalu](./media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-nav.png)

<span data-ttu-id="6c01e-186">Może być konieczne kliknięcie pozycji "Więcej usług" nie można znaleźć sekcji monitora.</span><span class="sxs-lookup"><span data-stu-id="6c01e-186">You may have to click "More services" to find the Monitor section.</span></span>

<span data-ttu-id="6c01e-187">W tym miejscu możesz wyświetlić i filtrować wszystkie zasoby, które obsługują ustawień diagnostycznych, aby zobaczyć, czy mają włączoną diagnostykę.</span><span class="sxs-lookup"><span data-stu-id="6c01e-187">Here you can view and filter all resources that support diagnostic settings to see if they have diagnostics enabled.</span></span> <span data-ttu-id="6c01e-188">Możesz również przejść do Zobacz Jeśli wiele ustawień są ustawiane w zasobie i sprawdź, które konta magazynu, przestrzeni nazw usługi Event Hubs i/lub obszar roboczy analizy dzienników, które dane są przesyłane do.</span><span class="sxs-lookup"><span data-stu-id="6c01e-188">You can also drill down to see if multiple settings are set on a resource and check which storage account, Event Hubs namespace, and/or Log Analytics workspace that data are flowing to.</span></span>

![Wyniki diagnostyki dzienniki w portalu](./media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-blade.png)

<span data-ttu-id="6c01e-190">Dodawanie ustawienie diagnostyczne wyświetlenie widoku ustawień diagnostycznych, w którym można włączyć, wyłączyć lub zmodyfikować ustawienia diagnostyczne dla wybranego zasobu.</span><span class="sxs-lookup"><span data-stu-id="6c01e-190">Adding a diagnostic setting brings up the Diagnostic Settings view, where you can enable, disable, or modify your diagnostic settings for the selected resource.</span></span>

## <a name="supported-services-categories-and-schemas-for-resource-diagnostic-logs"></a><span data-ttu-id="6c01e-191">Obsługiwane usługi, kategorie i schematy do dzienników diagnostycznych zasobu</span><span class="sxs-lookup"><span data-stu-id="6c01e-191">Supported services, categories, and schemas for resource diagnostic logs</span></span>
<span data-ttu-id="6c01e-192">[Znajduje się w artykule](monitoring-diagnostic-logs-schema.md) pełną listę obsługiwanych usług i kategorie dziennika i schematy używane przez te usługi.</span><span class="sxs-lookup"><span data-stu-id="6c01e-192">[See this article](monitoring-diagnostic-logs-schema.md) for a complete list of supported services and the log categories and schemas used by those services.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6c01e-193">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6c01e-193">Next steps</span></span>

* [<span data-ttu-id="6c01e-194">Strumień zasobu dzienników diagnostycznych do **centra zdarzeń**</span><span class="sxs-lookup"><span data-stu-id="6c01e-194">Stream resource diagnostic logs to **Event Hubs**</span></span>](monitoring-stream-diagnostic-logs-to-event-hubs.md)
* [<span data-ttu-id="6c01e-195">Zmień ustawienia diagnostyczne zasobu przy użyciu interfejsu API REST Azure monitora</span><span class="sxs-lookup"><span data-stu-id="6c01e-195">Change resource diagnostic settings using the Azure Monitor REST API</span></span>](https://msdn.microsoft.com/library/azure/dn931931.aspx)
* [<span data-ttu-id="6c01e-196">Analizowanie dzienników z usługi Azure storage z analizy dzienników</span><span class="sxs-lookup"><span data-stu-id="6c01e-196">Analyze logs from Azure storage with Log Analytics</span></span>](../log-analytics/log-analytics-azure-storage.md)
