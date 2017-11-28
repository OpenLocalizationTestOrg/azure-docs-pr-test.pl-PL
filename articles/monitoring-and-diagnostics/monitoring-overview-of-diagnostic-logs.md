---
title: "aaaOverview dzienników diagnostycznych platformy Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, co to są dzienników diagnostycznych platformy Azure i używania ich toounderstand zdarzeń występujących w ramach zasobów platformy Azure."
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
ms.openlocfilehash: e38991c540626b4bb5b5b9a995276881ee58f368
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="collect-and-consume-log-data-from-your-azure-resources"></a><span data-ttu-id="9fad5-103">Zbierania i wykorzystywania danych dziennika z zasobów platformy Azure</span><span class="sxs-lookup"><span data-stu-id="9fad5-103">Collect and consume log data from your Azure resources</span></span>

## <a name="what-are-azure-resource-diagnostic-logs"></a><span data-ttu-id="9fad5-104">Co to są dzienniki diagnostyczne zasobów platformy Azure</span><span class="sxs-lookup"><span data-stu-id="9fad5-104">What are Azure resource diagnostic logs</span></span>
<span data-ttu-id="9fad5-105">**Azure dzienników diagnostycznych poziom zasobów** są dzienniki emitowane przez zasób, które zawierają rozbudowane, często dane dotyczące operacji hello tego zasobu.</span><span class="sxs-lookup"><span data-stu-id="9fad5-105">**Azure resource-level diagnostic logs** are logs emitted by a resource that provide rich, frequent data about hello operation of that resource.</span></span> <span data-ttu-id="9fad5-106">zawartość Hello te dzienniki zależy od typu zasobu.</span><span class="sxs-lookup"><span data-stu-id="9fad5-106">hello content of these logs varies by resource type.</span></span> <span data-ttu-id="9fad5-107">Na przykład liczników reguły grupy zabezpieczeń sieci i usługi Key Vault inspekcje są dwie kategorie dzienników zasobów.</span><span class="sxs-lookup"><span data-stu-id="9fad5-107">For example, Network Security Group rule counters and Key Vault audits are two categories of resource logs.</span></span>

<span data-ttu-id="9fad5-108">Dzienniki diagnostyczne poziom zasobów różnią się od hello [dziennik aktywności](monitoring-overview-activity-logs.md).</span><span class="sxs-lookup"><span data-stu-id="9fad5-108">Resource-level diagnostic logs differ from hello [Activity Log](monitoring-overview-activity-logs.md).</span></span> <span data-ttu-id="9fad5-109">Witaj dziennik aktywności zapewnia wgląd w operacji hello, wykonywane na zasobów w ramach subskrypcji, za pomocą Menedżera zasobów, na przykład tworzenia maszyny wirtualnej lub usuwanie aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="9fad5-109">hello Activity Log provides insight into hello operations that were performed on resources in your subscription using Resource Manager, for example, creating a virtual machine or deleting a logic app.</span></span> <span data-ttu-id="9fad5-110">Dziennik aktywności Hello jest dziennika poziomu subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="9fad5-110">hello Activity Log is a subscription-level log.</span></span> <span data-ttu-id="9fad5-111">Dzienniki diagnostyczne poziom zasobów zapewniają wgląd w operacji wykonanych w ramach tego zasobu, na przykład pobierania klucza tajnego z magazynu kluczy.</span><span class="sxs-lookup"><span data-stu-id="9fad5-111">Resource-level diagnostic logs provide insight into operations that were performed within that resource itself, for example, getting a secret from a Key Vault.</span></span>

<span data-ttu-id="9fad5-112">Dzienniki diagnostyczne poziom zasobów również różnią się od dzienników diagnostycznych na poziomie systemu operacyjnego gościa.</span><span class="sxs-lookup"><span data-stu-id="9fad5-112">Resource-level diagnostic logs also differ from guest OS-level diagnostic logs.</span></span> <span data-ttu-id="9fad5-113">Dzienniki diagnostyczne systemu operacyjnego gościa znajdują się te zebranych przez agenta, które działają w ramach maszyny wirtualnej lub inne obsługiwane typu zasobu.</span><span class="sxs-lookup"><span data-stu-id="9fad5-113">Guest OS diagnostic logs are those collected by an agent running inside of a virtual machine or other supported resource type.</span></span> <span data-ttu-id="9fad5-114">Poziom zasobów dzienników diagnostycznych wymagają żadne dane specyficzne dla zasobów agenta do przechwycenia z hello platformy Azure, podczas dzienników diagnostycznych na poziomie systemu operacyjnego gościa przechwycenia danych z systemu operacyjnego hello i aplikacje działające na maszynie wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="9fad5-114">Resource-level diagnostic logs require no agent and capture resource-specific data from hello Azure platform itself, while guest OS-level diagnostic logs capture data from hello operating system and applications running on a virtual machine.</span></span>

<span data-ttu-id="9fad5-115">Nie wszystkie zasoby obsługuje hello nowego typu zasobu dzienników diagnostycznych opisanych tutaj.</span><span class="sxs-lookup"><span data-stu-id="9fad5-115">Not all resources support hello new type of resource diagnostic logs described here.</span></span> <span data-ttu-id="9fad5-116">Ten artykuł zawiera listę sekcji typów zasobów, które obsługują nowe dzienniki diagnostyczne hello poziom zasobów.</span><span class="sxs-lookup"><span data-stu-id="9fad5-116">This article contains a section listing which resource types support hello new resource-level diagnostic logs.</span></span>

![<span data-ttu-id="9fad5-117">Diagnostyka zasobów rejestruje vs innych typów dzienników</span><span class="sxs-lookup"><span data-stu-id="9fad5-117">Resource diagnostics logs vs other types of logs</span></span> ](./media/monitoring-overview-of-diagnostic-logs/Diagnostics_Logs_vs_other_logs_v5.png)

## <a name="what-you-can-do-with-resource-level-diagnostic-logs"></a><span data-ttu-id="9fad5-118">Co należy zrobić z dzienników diagnostycznych poziom zasobów</span><span class="sxs-lookup"><span data-stu-id="9fad5-118">What you can do with resource-level diagnostic logs</span></span>
<span data-ttu-id="9fad5-119">Poniżej podano niektóre czynności hello, które można wykonać za pomocą dzienników diagnostycznych zasobu:</span><span class="sxs-lookup"><span data-stu-id="9fad5-119">Here are some of hello things you can do with resource diagnostic logs:</span></span>

![Logiczne umieszczania dzienników diagnostycznych zasobu](./media/monitoring-overview-of-diagnostic-logs/Diagnostics_Logs_Actions.png)


* <span data-ttu-id="9fad5-121">Zapisz je tooa [ **konta magazynu** ](monitoring-archive-diagnostic-logs.md) inspekcji inspekcji lub ręcznie.</span><span class="sxs-lookup"><span data-stu-id="9fad5-121">Save them tooa [**Storage Account**](monitoring-archive-diagnostic-logs.md) for auditing or manual inspection.</span></span> <span data-ttu-id="9fad5-122">Można określić za pomocą czasu (w dniach) przechowywania hello **ustawień diagnostycznych zasobu**.</span><span class="sxs-lookup"><span data-stu-id="9fad5-122">You can specify hello retention time (in days) using **resource diagnostic settings**.</span></span>
* <span data-ttu-id="9fad5-123">[Strumienia ich zbyt**usługi Event Hubs** ](monitoring-stream-diagnostic-logs-to-event-hubs.md) dla wprowadzanie przez usługi innej firmy lub rozwiązania analizy niestandardowych, takich jak usługi Power BI.</span><span class="sxs-lookup"><span data-stu-id="9fad5-123">[Stream them too**Event Hubs**](monitoring-stream-diagnostic-logs-to-event-hubs.md) for ingestion by a third-party service or custom analytics solution such as PowerBI.</span></span>
* <span data-ttu-id="9fad5-124">Analizuj je za pomocą [OMS analizy dzienników](../log-analytics/log-analytics-azure-storage.md)</span><span class="sxs-lookup"><span data-stu-id="9fad5-124">Analyze them with [OMS Log Analytics](../log-analytics/log-analytics-azure-storage.md)</span></span>

<span data-ttu-id="9fad5-125">Możesz użyć konta magazynu lub przestrzeni nazw usługi Event Hubs, która nie znajduje się w tej samej subskrypcji Witaj, zgodnie z jedną emitowanie dzienniki hello.</span><span class="sxs-lookup"><span data-stu-id="9fad5-125">You can use a storage account or Event Hubs namespace that is not in hello same subscription as hello one emitting logs.</span></span> <span data-ttu-id="9fad5-126">Witaj, użytkownik konfiguruje ustawienie hello musi mieć hello odpowiednie RBAC dostępu tooboth subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="9fad5-126">hello user who configures hello setting must have hello appropriate RBAC access tooboth subscriptions.</span></span>

## <a name="resource-diagnostic-settings"></a><span data-ttu-id="9fad5-127">Ustawienia diagnostyczne zasobu</span><span class="sxs-lookup"><span data-stu-id="9fad5-127">Resource diagnostic settings</span></span>
<span data-ttu-id="9fad5-128">Dzienniki diagnostyczne zasobu z systemem innym niż — obliczeń się, że zasoby są skonfigurowane przy użyciu ustawień diagnostycznych zasobu.</span><span class="sxs-lookup"><span data-stu-id="9fad5-128">Resource diagnostic logs for non-Compute resources are configured using resource diagnostic settings.</span></span> <span data-ttu-id="9fad5-129">**Ustawienia diagnostyczne zasobu** formantów zasobów:</span><span class="sxs-lookup"><span data-stu-id="9fad5-129">**Resource diagnostic settings** for a resource control:</span></span>

* <span data-ttu-id="9fad5-130">W przypadku dzienników diagnostycznych zasobu i metryki wysyłania (konto magazynu, centra zdarzeń i/lub analizy dzienników OMS).</span><span class="sxs-lookup"><span data-stu-id="9fad5-130">Where resource diagnostic logs and metrics are sent (Storage Account, Event Hubs, and/or OMS Log Analytics).</span></span>
* <span data-ttu-id="9fad5-131">Kategorie dziennika, które są wysyłane i czy dane są także wysyłane.</span><span class="sxs-lookup"><span data-stu-id="9fad5-131">Which log categories are sent and whether metric data is also sent.</span></span>
* <span data-ttu-id="9fad5-132">Jak długo każdej kategorii dziennika powinny zostać zachowane na koncie magazynu</span><span class="sxs-lookup"><span data-stu-id="9fad5-132">How long each log category should be retained in a storage account</span></span>
    - <span data-ttu-id="9fad5-133">Przechowywanie 0 oznacza, że dzienniki są przechowywane w nieskończoność.</span><span class="sxs-lookup"><span data-stu-id="9fad5-133">A retention of zero days means logs are kept forever.</span></span> <span data-ttu-id="9fad5-134">W przeciwnym razie wartość hello może być dowolną liczbę dni od 1 do 2147483647.</span><span class="sxs-lookup"><span data-stu-id="9fad5-134">Otherwise, hello value can be any number of days between 1 and 2147483647.</span></span>
    - <span data-ttu-id="9fad5-135">Jeśli zasady przechowywania są skonfigurowane, ale przechowywanie dzienniki na koncie magazynu jest wyłączone (na przykład, jeśli tylko opcje usługi Event Hubs lub OMS są zaznaczone), zasad przechowywania hello nie obowiązują.</span><span class="sxs-lookup"><span data-stu-id="9fad5-135">If retention policies are set but storing logs in a Storage Account is disabled (for example, if only Event Hubs or OMS options are selected), hello retention policies have no effect.</span></span>
    - <span data-ttu-id="9fad5-136">Zasady przechowywania są stosowane na dzień, więc na powitania koniec dnia (UTC), rejestruje od dnia hello, która jest teraz poza zasady przechowywania hello są usuwane.</span><span class="sxs-lookup"><span data-stu-id="9fad5-136">Retention policies are applied per-day, so at hello end of a day (UTC), logs from hello day that is now beyond hello retention policy are deleted.</span></span> <span data-ttu-id="9fad5-137">Na przykład jeśli masz zasady przechowywania jeden dzień początku hello dzisiaj dzień hello hello dzienniki hello dzień przed wczoraj zostaną usunięte.</span><span class="sxs-lookup"><span data-stu-id="9fad5-137">For example, if you had a retention policy of one day, at hello beginning of hello day today hello logs from hello day before yesterday would be deleted.</span></span>

<span data-ttu-id="9fad5-138">Te ustawienia można łatwo skonfigurować za pomocą hello ustawień diagnostycznych dla zasobu w hello portalu Azure, za pomocą poleceń programu PowerShell systemu Azure i interfejsu wiersza polecenia lub za pośrednictwem hello [interfejsu API REST Monitor Azure](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span><span class="sxs-lookup"><span data-stu-id="9fad5-138">These settings are easily configured via hello diagnostic settings for a resource in hello Azure portal, via Azure PowerShell and CLI commands, or via hello [Azure Monitor REST API](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span></span>

> [!WARNING]
> <span data-ttu-id="9fad5-139">Dzienniki diagnostyczne i metryki z warstwy systemu operacyjnego gościa hello użycia zasobów (na przykład maszyny wirtualne lub sieci szkieletowej usług) obliczeń [odrębny mechanizm konfiguracji i wybór wyjścia](../azure-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="9fad5-139">Diagnostic logs and metrics for from hello guest OS layer of Compute resources (for example, VMs or Service Fabric) use [a separate mechanism for configuration and selection of outputs](../azure-diagnostics.md).</span></span>
>
>

## <a name="how-tooenable-collection-of-resource-diagnostic-logs"></a><span data-ttu-id="9fad5-140">Jak tooenable zbierania dzienników diagnostycznych zasobu</span><span class="sxs-lookup"><span data-stu-id="9fad5-140">How tooenable collection of resource diagnostic logs</span></span>
<span data-ttu-id="9fad5-141">Można włączyć zbierania dzienników diagnostycznych zasobu [podczas tworzenia zasobu w szablonie usługi Resource Manager](./monitoring-enable-diagnostic-logs-using-template.md) lub po utworzeniu zasobu ze strony tego zasobu w portalu hello.</span><span class="sxs-lookup"><span data-stu-id="9fad5-141">Collection of resource diagnostic logs can be enabled [as part of creating a resource in a Resource Manager template](./monitoring-enable-diagnostic-logs-using-template.md) or after a resource is created from that resource's page in hello portal.</span></span> <span data-ttu-id="9fad5-142">Można również włączyć kolekcji w dowolnym momencie za pomocą poleceń programu Azure PowerShell lub interfejsu wiersza polecenia lub hello interfejsu API REST Monitor Azure.</span><span class="sxs-lookup"><span data-stu-id="9fad5-142">You can also enable collection at any point using Azure PowerShell or CLI commands, or using hello Azure Monitor REST API.</span></span>

> [!TIP]
> <span data-ttu-id="9fad5-143">Te instrukcje mogą nie dotyczyć bezpośrednio tooevery zasobów.</span><span class="sxs-lookup"><span data-stu-id="9fad5-143">These instructions may not apply directly tooevery resource.</span></span> <span data-ttu-id="9fad5-144">Zobacz linki schematu hello u dołu tej strony toounderstand specjalne kroki, które mogą być zastosowane toocertain typów zasobów hello.</span><span class="sxs-lookup"><span data-stu-id="9fad5-144">See hello schema links at hello bottom of this page toounderstand special steps that may apply toocertain resource types.</span></span>
>
>

### <a name="enable-collection-of-resource-diagnostic-logs-in-hello-portal"></a><span data-ttu-id="9fad5-145">Włącz zbieranie dzienników diagnostycznych zasobu w portalu hello</span><span class="sxs-lookup"><span data-stu-id="9fad5-145">Enable collection of resource diagnostic logs in hello portal</span></span>
<span data-ttu-id="9fad5-146">Możesz włączyć zbierania dzienników diagnostycznych zasobu w hello Azure portalu po utworzeniu zasobu przez przechodzi do określonego zasobu tooa lub przechodząc tooAzure monitora.</span><span class="sxs-lookup"><span data-stu-id="9fad5-146">You can enable collection of resource diagnostic logs in hello Azure portal after a resource has been created either by going tooa specific resource or by navigating tooAzure Monitor.</span></span> <span data-ttu-id="9fad5-147">tooenable za pomocą monitora Azure:</span><span class="sxs-lookup"><span data-stu-id="9fad5-147">tooenable this via Azure Monitor:</span></span>

1. <span data-ttu-id="9fad5-148">W hello [portalu Azure](http://portal.azure.com), przejdź tooAzure monitora i kliknij na **ustawień diagnostycznych**</span><span class="sxs-lookup"><span data-stu-id="9fad5-148">In hello [Azure portal](http://portal.azure.com), navigate tooAzure Monitor and click on **Diagnostic Settings**</span></span>

    ![Monitorowanie sekcji Azure Monitor](media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-blade.png)

2. <span data-ttu-id="9fad5-150">Opcjonalnie Filtruj listę hello według grupy zasobów lub typ zasobu, a następnie kliknij na powitania zasobu, dla którego chcesz tooset ustawienie diagnostyczne.</span><span class="sxs-lookup"><span data-stu-id="9fad5-150">Optionally filter hello list by resource group or resource type, then click on hello resource for which you would like tooset a diagnostic setting.</span></span>

3. <span data-ttu-id="9fad5-151">Jeśli nie istnieją żadne ustawienia na powitania zasobów, wybrana przez Ciebie, jesteś toocreate zostanie wyświetlony monit o ustawienie.</span><span class="sxs-lookup"><span data-stu-id="9fad5-151">If no settings exist on hello resource you have selected, you are prompted toocreate a setting.</span></span> <span data-ttu-id="9fad5-152">Kliknij pozycję "Włącz diagnostykę."</span><span class="sxs-lookup"><span data-stu-id="9fad5-152">Click "Turn on diagnostics."</span></span>

   ![Dodaj ustawienie diagnostyczne - żadnych istniejących ustawień](media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-none.png)

   <span data-ttu-id="9fad5-154">W przypadku ustawienia istniejące na powitania zasobów, zostanie wyświetlona lista ustawień już skonfigurowana dla tego zasobu.</span><span class="sxs-lookup"><span data-stu-id="9fad5-154">If there are existing settings on hello resource, you will see a list of settings already configured on this resource.</span></span> <span data-ttu-id="9fad5-155">Kliknij przycisk "Dodaj ustawienie diagnostyczne".</span><span class="sxs-lookup"><span data-stu-id="9fad5-155">Click "Add diagnostic setting."</span></span>

   ![Dodaj ustawienie diagnostyczne — istniejące ustawienia](media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-multiple.png)

3. <span data-ttu-id="9fad5-157">Nadaj nazwę ustawienie, hello pola wyboru, dla każdego toowhich docelowego chcesz toosend danych i skonfiguruj zasobów jest używana dla każdej lokalizacji docelowej.</span><span class="sxs-lookup"><span data-stu-id="9fad5-157">Give your setting a name, check hello boxes for each destination toowhich you would like toosend data, and configure which resource is used for each destination.</span></span> <span data-ttu-id="9fad5-158">Opcjonalnie ustawić liczbę dni tooretain tych dzienników przy użyciu hello **przechowywania (dni)** suwaki (tylko toohello odpowiednie konta miejscem docelowym magazynu).</span><span class="sxs-lookup"><span data-stu-id="9fad5-158">Optionally, set a number of days tooretain these logs by using hello **Retention (days)** sliders (only applicable toohello storage account destination).</span></span> <span data-ttu-id="9fad5-159">Przechowywanie zero dni przechowuje dzienniki hello nieskończoność.</span><span class="sxs-lookup"><span data-stu-id="9fad5-159">A retention of zero days stores hello logs indefinitely.</span></span>
   
   ![Dodaj ustawienie diagnostyczne — istniejące ustawienia](media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-configure.png)
    
4. <span data-ttu-id="9fad5-161">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="9fad5-161">Click **Save**.</span></span>

<span data-ttu-id="9fad5-162">Po kilku chwilach hello nowe ustawienie jest wyświetlane na liście ustawień dla tego zasobu i dzienników diagnostycznych są wysyłane toohello określonych miejsc docelowych zaraz po wygenerowaniu nowych danych zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="9fad5-162">After a few moments, hello new setting appears in your list of settings for this resource, and diagnostic logs are sent toohello specified destinations as soon as new event data is generated.</span></span>

### <a name="enable-collection-of-resource-diagnostic-logs-via-powershell"></a><span data-ttu-id="9fad5-163">Włącz zbieranie dzienników diagnostycznych zasobów za pomocą programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="9fad5-163">Enable collection of resource diagnostic logs via PowerShell</span></span>
<span data-ttu-id="9fad5-164">Kolekcja tooenable dzienników diagnostycznych zasobów za pomocą programu Azure PowerShell hello Użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="9fad5-164">tooenable collection of resource diagnostic logs via Azure PowerShell, use hello following commands:</span></span>

<span data-ttu-id="9fad5-165">Magazyn tooenable dzienników diagnostycznych na koncie magazynu, użyj tego polecenia:</span><span class="sxs-lookup"><span data-stu-id="9fad5-165">tooenable storage of diagnostic logs in a storage account, use this command:</span></span>

```powershell
Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -StorageAccountId [your storage account id] -Enabled $true
```

<span data-ttu-id="9fad5-166">Witaj magazynu, który jest identyfikator konta hello identyfikator zasobu dla toowhich konta magazynu hello ma toosend hello dzienniki.</span><span class="sxs-lookup"><span data-stu-id="9fad5-166">hello storage account ID is hello resource ID for hello storage account toowhich you want toosend hello logs.</span></span>

<span data-ttu-id="9fad5-167">tooenable przesyłania strumieniowego dzienników diagnostycznych tooan Centrum zdarzeń, użyj tego polecenia:</span><span class="sxs-lookup"><span data-stu-id="9fad5-167">tooenable streaming of diagnostic logs tooan event hub, use this command:</span></span>

```powershell
Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -ServiceBusRuleId [your Service Bus rule id] -Enabled $true
```

<span data-ttu-id="9fad5-168">Identyfikator reguły magistrali usługi Hello jest ciągiem o następującym formacie: `{Service Bus resource ID}/authorizationrules/{key name}`.</span><span class="sxs-lookup"><span data-stu-id="9fad5-168">hello service bus rule ID is a string with this format: `{Service Bus resource ID}/authorizationrules/{key name}`.</span></span>

<span data-ttu-id="9fad5-169">tooenable wysyłania dzienników diagnostycznych obszaru roboczego analizy dzienników tooa, użyj tego polecenia:</span><span class="sxs-lookup"><span data-stu-id="9fad5-169">tooenable sending of diagnostic logs tooa Log Analytics workspace, use this command:</span></span>

```powershell
Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -WorkspaceId [resource id of hello log analytics workspace] -Enabled $true
```

<span data-ttu-id="9fad5-170">Można uzyskać Identyfikatora zasobu hello obszaru roboczego analizy dzienników przy użyciu hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="9fad5-170">You can obtain hello resource ID of your Log Analytics workspace using hello following command:</span></span>

```powershell
(Get-AzureRmOperationalInsightsWorkspace).ResourceId
```

<span data-ttu-id="9fad5-171">Tooenable te parametry można łączyć wiele opcji danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="9fad5-171">You can combine these parameters tooenable multiple output options.</span></span>

### <a name="enable-collection-of-resource-diagnostic-logs-via-cli"></a><span data-ttu-id="9fad5-172">Włącz zbieranie dzienników diagnostycznych zasobów za pomocą interfejsu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="9fad5-172">Enable collection of resource diagnostic logs via CLI</span></span>
<span data-ttu-id="9fad5-173">Kolekcja tooenable dzienników diagnostycznych zasobu za pośrednictwem hello Azure CLI hello Użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="9fad5-173">tooenable collection of resource diagnostic logs via hello Azure CLI, use hello following commands:</span></span>

<span data-ttu-id="9fad5-174">Magazyn tooenable dzienników diagnostycznych na koncie magazynu, użyj tego polecenia:</span><span class="sxs-lookup"><span data-stu-id="9fad5-174">tooenable storage of diagnostic logs in a Storage Account, use this command:</span></span>

```azurecli
azure insights diagnostic set --resourceId <resourceId> --storageId <storageAccountId> --enabled true
```

<span data-ttu-id="9fad5-175">Witaj magazynu, który jest identyfikator konta hello identyfikator zasobu dla toowhich konta magazynu hello ma toosend hello dzienniki.</span><span class="sxs-lookup"><span data-stu-id="9fad5-175">hello storage account ID is hello resource ID for hello storage account toowhich you want toosend hello logs.</span></span>

<span data-ttu-id="9fad5-176">tooenable przesyłania strumieniowego dzienników diagnostycznych tooan Centrum zdarzeń, użyj tego polecenia:</span><span class="sxs-lookup"><span data-stu-id="9fad5-176">tooenable streaming of diagnostic logs tooan event hub, use this command:</span></span>

```azurecli
azure insights diagnostic set --resourceId <resourceId> --serviceBusRuleId <serviceBusRuleId> --enabled true
```

<span data-ttu-id="9fad5-177">Identyfikator reguły magistrali usługi Hello jest ciągiem o następującym formacie: `{Service Bus resource ID}/authorizationrules/{key name}`.</span><span class="sxs-lookup"><span data-stu-id="9fad5-177">hello service bus rule ID is a string with this format: `{Service Bus resource ID}/authorizationrules/{key name}`.</span></span>

<span data-ttu-id="9fad5-178">tooenable wysyłania dzienników diagnostycznych obszaru roboczego analizy dzienników tooa, użyj tego polecenia:</span><span class="sxs-lookup"><span data-stu-id="9fad5-178">tooenable sending of diagnostic logs tooa Log Analytics workspace, use this command:</span></span>

```azurecli
azure insights diagnostic set --resourceId <resourceId> --workspaceId <resource id of hello log analytics workspace> --enabled true
```

<span data-ttu-id="9fad5-179">Tooenable te parametry można łączyć wiele opcji danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="9fad5-179">You can combine these parameters tooenable multiple output options.</span></span>

### <a name="enable-collection-of-resource-diagnostic-logs-via-rest-api"></a><span data-ttu-id="9fad5-180">Włącz zbieranie dzienników diagnostycznych zasobów za pomocą interfejsu API REST</span><span class="sxs-lookup"><span data-stu-id="9fad5-180">Enable collection of resource diagnostic logs via REST API</span></span>
<span data-ttu-id="9fad5-181">ustawienia diagnostyki toochange przy użyciu hello interfejsu API REST Monitor Azure, zobacz [tego dokumentu](https://msdn.microsoft.com/library/azure/dn931931.aspx).</span><span class="sxs-lookup"><span data-stu-id="9fad5-181">toochange diagnostic settings using hello Azure Monitor REST API, see [this document](https://msdn.microsoft.com/library/azure/dn931931.aspx).</span></span>

## <a name="manage-resource-diagnostic-settings-in-hello-portal"></a><span data-ttu-id="9fad5-182">Zarządzanie ustawień diagnostycznych zasobu w portalu hello</span><span class="sxs-lookup"><span data-stu-id="9fad5-182">Manage resource diagnostic settings in hello portal</span></span>
<span data-ttu-id="9fad5-183">Upewnij się, że wszystkie zasoby zostały skonfigurowane przy użyciu ustawień diagnostycznych.</span><span class="sxs-lookup"><span data-stu-id="9fad5-183">Ensure that all of your resources are set up with diagnostic settings.</span></span> <span data-ttu-id="9fad5-184">Przejdź za**Monitor** w hello portalu i Otwórz **ustawień diagnostycznych**.</span><span class="sxs-lookup"><span data-stu-id="9fad5-184">Navigate too**Monitor** in hello portal and open **Diagnostic settings**.</span></span>

![Diagnostycznych dzienników bloku w portalu hello](./media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-nav.png)

<span data-ttu-id="9fad5-186">Konieczne może być tooclick sekcji Monitor hello toofind "Więcej usług".</span><span class="sxs-lookup"><span data-stu-id="9fad5-186">You may have tooclick "More services" toofind hello Monitor section.</span></span>

<span data-ttu-id="9fad5-187">W tym miejscu możesz wyświetlić i filtrować wszystkie zasoby, które obsługują toosee ustawień diagnostycznych, jeśli mają włączoną diagnostykę.</span><span class="sxs-lookup"><span data-stu-id="9fad5-187">Here you can view and filter all resources that support diagnostic settings toosee if they have diagnostics enabled.</span></span> <span data-ttu-id="9fad5-188">Można również przejść do szczegółów toosee skonfigurowanie wielu ustawień do zasobu i sprawdzić, które konta magazynu, przestrzeni nazw usługi Event Hubs i/lub obszar roboczy analizy dzienników, które dane są przesyłane do.</span><span class="sxs-lookup"><span data-stu-id="9fad5-188">You can also drill down toosee if multiple settings are set on a resource and check which storage account, Event Hubs namespace, and/or Log Analytics workspace that data are flowing to.</span></span>

![Wyniki diagnostyki dzienniki w portalu](./media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-blade.png)

<span data-ttu-id="9fad5-190">Dodanie ustawienie diagnostyczne wywołuje hello ustawień diagnostycznych widoku, gdzie można włączyć, wyłączyć lub zmodyfikować ustawienia diagnostyczne dla hello wybrany zasobów.</span><span class="sxs-lookup"><span data-stu-id="9fad5-190">Adding a diagnostic setting brings up hello Diagnostic Settings view, where you can enable, disable, or modify your diagnostic settings for hello selected resource.</span></span>

## <a name="supported-services-categories-and-schemas-for-resource-diagnostic-logs"></a><span data-ttu-id="9fad5-191">Obsługiwane usługi, kategorie i schematy do dzienników diagnostycznych zasobu</span><span class="sxs-lookup"><span data-stu-id="9fad5-191">Supported services, categories, and schemas for resource diagnostic logs</span></span>
<span data-ttu-id="9fad5-192">[Znajduje się w artykule](monitoring-diagnostic-logs-schema.md) pełną listę obsługiwanych usług i hello dziennika kategorii i schematy używane przez te usługi.</span><span class="sxs-lookup"><span data-stu-id="9fad5-192">[See this article](monitoring-diagnostic-logs-schema.md) for a complete list of supported services and hello log categories and schemas used by those services.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9fad5-193">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="9fad5-193">Next steps</span></span>

* [<span data-ttu-id="9fad5-194">Zbyt strumienia dzienników diagnostycznych zasobu**centra zdarzeń**</span><span class="sxs-lookup"><span data-stu-id="9fad5-194">Stream resource diagnostic logs too**Event Hubs**</span></span>](monitoring-stream-diagnostic-logs-to-event-hubs.md)
* [<span data-ttu-id="9fad5-195">Zmień ustawienia diagnostyczne zasobu przy użyciu interfejsu API REST Monitor Azure hello</span><span class="sxs-lookup"><span data-stu-id="9fad5-195">Change resource diagnostic settings using hello Azure Monitor REST API</span></span>](https://msdn.microsoft.com/library/azure/dn931931.aspx)
* [<span data-ttu-id="9fad5-196">Analizowanie dzienników z usługi Azure storage z analizy dzienników</span><span class="sxs-lookup"><span data-stu-id="9fad5-196">Analyze logs from Azure storage with Log Analytics</span></span>](../log-analytics/log-analytics-azure-storage.md)
