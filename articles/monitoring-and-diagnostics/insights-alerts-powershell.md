---
title: "alerty aaaCreate dla usług Azure - PowerShell | Dokumentacja firmy Microsoft"
description: "Gdy są spełnione warunki hello wyzwolenia wiadomości e-mail, powiadomienia, adresy URL witryny sieci Web wywołania (elementy webhook) lub automatyzacji."
author: rboucher
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: d26ab15b-7b7e-42a9-81c8-3ce9ead5d252
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/20/2016
ms.author: robb
ms.openlocfilehash: 80d3a3f194fc6a5a09a81d04206ea7a1640bddb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-metric-alerts-in-azure-monitor-for-azure-services---powershell"></a><span data-ttu-id="744ec-103">W monitorze Azure tworzyć alerty metryki dla usługi Azure - PowerShell</span><span class="sxs-lookup"><span data-stu-id="744ec-103">Create metric alerts in Azure Monitor for Azure services - PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="744ec-104">Portal</span><span class="sxs-lookup"><span data-stu-id="744ec-104">Portal</span></span>](insights-alerts-portal.md)
> * [<span data-ttu-id="744ec-105">Program PowerShell</span><span class="sxs-lookup"><span data-stu-id="744ec-105">PowerShell</span></span>](insights-alerts-powershell.md)
> * [<span data-ttu-id="744ec-106">Interfejs wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="744ec-106">CLI</span></span>](insights-alerts-command-line-interface.md)
>
>

## <a name="overview"></a><span data-ttu-id="744ec-107">Omówienie</span><span class="sxs-lookup"><span data-stu-id="744ec-107">Overview</span></span>
<span data-ttu-id="744ec-108">W tym artykule opisano, jak tooset zapasowej Azure Metryka alerty za pomocą programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="744ec-108">This article shows you how tooset up Azure metric alerts using PowerShell.</span></span>  

<span data-ttu-id="744ec-109">Możesz otrzymywać alertu na podstawie metryki monitorowania lub zdarzenia na usługami Azure.</span><span class="sxs-lookup"><span data-stu-id="744ec-109">You can receive an alert based on monitoring metrics for, or events on, your Azure services.</span></span>

* <span data-ttu-id="744ec-110">**Wartości metryki** — Witaj alertu wyzwalacze, jeśli wartość hello określonej metryki przecina próg przypisać w żadnym kierunku.</span><span class="sxs-lookup"><span data-stu-id="744ec-110">**Metric values** - hello alert triggers when hello value of a specified metric crosses a threshold you assign in either direction.</span></span> <span data-ttu-id="744ec-111">Oznacza to, że oba wyzwala kiedy najpierw zostanie spełniony warunek hello i następnie później podczas warunku jest już spełniane.</span><span class="sxs-lookup"><span data-stu-id="744ec-111">That is, it triggers both when hello condition is first met and then afterwards when that condition is no longer being met.</span></span>    
* <span data-ttu-id="744ec-112">**Zdarzenia dziennika aktywności** — alert może wyzwolić na *co* zdarzenia lub tylko wtedy, gdy występuje określone zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="744ec-112">**Activity log events** - An alert can trigger on *every* event, or, only when a certain events occurs.</span></span> <span data-ttu-id="744ec-113">więcej informacji na temat alertów dotyczących działań w dzienniku toolearn [kliknij tutaj](monitoring-activity-log-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="744ec-113">toolearn more about activity log alerts [click here](monitoring-activity-log-alerts.md)</span></span>

<span data-ttu-id="744ec-114">Można skonfigurować hello metryki toodo alertów po, wyzwala:</span><span class="sxs-lookup"><span data-stu-id="744ec-114">You can configure a metric alert toodo hello following when it triggers:</span></span>

* <span data-ttu-id="744ec-115">Wyślij administratora usługi toohello powiadomienia e-mail i współadministratorzy</span><span class="sxs-lookup"><span data-stu-id="744ec-115">send email notifications toohello service administrator and co-administrators</span></span>
* <span data-ttu-id="744ec-116">Wyślij wiadomość e-mail tooadditional wiadomości e-mail, które określisz.</span><span class="sxs-lookup"><span data-stu-id="744ec-116">send email tooadditional emails that you specify.</span></span>
* <span data-ttu-id="744ec-117">Wywołanie elementu webhook</span><span class="sxs-lookup"><span data-stu-id="744ec-117">call a webhook</span></span>
* <span data-ttu-id="744ec-118">Uruchamia wykonywanie elementów runbook platformy Azure (tylko z hello portalu Azure)</span><span class="sxs-lookup"><span data-stu-id="744ec-118">start execution of an Azure runbook (only from hello Azure portal)</span></span>

<span data-ttu-id="744ec-119">Można skonfigurować i uzyskać informacje na temat przy użyciu reguły alertów</span><span class="sxs-lookup"><span data-stu-id="744ec-119">You can configure and get information about alert rules using</span></span>

* [<span data-ttu-id="744ec-120">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="744ec-120">Azure portal</span></span>](insights-alerts-portal.md)
* [<span data-ttu-id="744ec-121">PowerShell</span><span class="sxs-lookup"><span data-stu-id="744ec-121">PowerShell</span></span>](insights-alerts-powershell.md)
* [<span data-ttu-id="744ec-122">Interfejs wiersza polecenia (CLI)</span><span class="sxs-lookup"><span data-stu-id="744ec-122">command-line interface (CLI)</span></span>](insights-alerts-command-line-interface.md)
* [<span data-ttu-id="744ec-123">Interfejs API REST Azure monitora</span><span class="sxs-lookup"><span data-stu-id="744ec-123">Azure Monitor REST API</span></span>](https://msdn.microsoft.com/library/azure/dn931945.aspx)

<span data-ttu-id="744ec-124">Aby uzyskać dodatkowe informacje, zawsze można wpisać ```Get-Help``` , a następnie hello polecenia programu PowerShell, które chcesz uzyskać pomoc.</span><span class="sxs-lookup"><span data-stu-id="744ec-124">For additional information, you can always type ```Get-Help``` and then hello PowerShell command you want help on.</span></span>

## <a name="create-alert-rules-in-powershell"></a><span data-ttu-id="744ec-125">Tworzyć reguły alertów w programie PowerShell</span><span class="sxs-lookup"><span data-stu-id="744ec-125">Create alert rules in PowerShell</span></span>
1. <span data-ttu-id="744ec-126">Zaloguj się za tooAzure.</span><span class="sxs-lookup"><span data-stu-id="744ec-126">Log in tooAzure.</span></span>   

    ```PowerShell
    Login-AzureRmAccount

    ```
2. <span data-ttu-id="744ec-127">Pobranie listy subskrypcji powitania od posiadanego.</span><span class="sxs-lookup"><span data-stu-id="744ec-127">Get a list of hello subscriptions you have available.</span></span> <span data-ttu-id="744ec-128">Sprawdź, użytkownik pracuje z subskrypcją prawo hello.</span><span class="sxs-lookup"><span data-stu-id="744ec-128">Verify that you are working with hello right subscription.</span></span> <span data-ttu-id="744ec-129">Jeśli nie, ustaw prawo toohello jeden przy użyciu dane wyjściowe hello `Get-AzureRmSubscription`.</span><span class="sxs-lookup"><span data-stu-id="744ec-129">If not, set it toohello right one using hello output from `Get-AzureRmSubscription`.</span></span>

    ```PowerShell
    Get-AzureRmSubscription
    Get-AzureRmContext
    Set-AzureRmContext -SubscriptionId <subscriptionid>
    ```
3. <span data-ttu-id="744ec-130">toolist istniejących reguł dla grupy zasobów, hello Użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="744ec-130">toolist existing rules on a resource group, use hello following command:</span></span>

   ```PowerShell
   Get-AzureRmAlertRule -ResourceGroup <myresourcegroup> -DetailedOutput
   ```
4. <span data-ttu-id="744ec-131">toocreate regułę, należy toohave kilku ważnych informacji najpierw.</span><span class="sxs-lookup"><span data-stu-id="744ec-131">toocreate a rule, you need toohave several important pieces of information first.</span></span>

  * <span data-ttu-id="744ec-132">Witaj **identyfikator zasobu** hello zasobu ma tooset alert dla</span><span class="sxs-lookup"><span data-stu-id="744ec-132">hello **Resource ID** for hello resource you want tooset an alert for</span></span>
  * <span data-ttu-id="744ec-133">Witaj **definicji metryk** dostępne dla tego zasobu</span><span class="sxs-lookup"><span data-stu-id="744ec-133">hello **metric definitions** available for that resource</span></span>

     <span data-ttu-id="744ec-134">Jednym ze sposobów tooget hello identyfikator zasobu jest hello toouse portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="744ec-134">One way tooget hello Resource ID is toouse hello Azure portal.</span></span> <span data-ttu-id="744ec-135">Zakładając, że zasób hello został już utworzony, wybierz go w portalu hello.</span><span class="sxs-lookup"><span data-stu-id="744ec-135">Assuming hello resource is already created, select it in hello portal.</span></span> <span data-ttu-id="744ec-136">Następnie w bloku dalej hello, wybierz *właściwości* w obszarze hello *ustawienia* sekcji.</span><span class="sxs-lookup"><span data-stu-id="744ec-136">Then in hello next blade, select *Properties* under hello *Settings* section.</span></span> <span data-ttu-id="744ec-137">**Identyfikator ZASOBU** jest polem w następnym bloku hello.</span><span class="sxs-lookup"><span data-stu-id="744ec-137">**RESOURCE ID** is a field in hello next blade.</span></span> <span data-ttu-id="744ec-138">Innym sposobem jest toouse hello [Eksploratora zasobów Azure](https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="744ec-138">Another way is toouse hello [Azure Resource Explorer](https://resources.azure.com/).</span></span>

     <span data-ttu-id="744ec-139">Na przykład identyfikator zasobu dla aplikacji sieci web</span><span class="sxs-lookup"><span data-stu-id="744ec-139">An example Resource ID for a web app is</span></span>

     ```
     /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename
     ```

     <span data-ttu-id="744ec-140">Można użyć `Get-AzureRmMetricDefinition` tooview hello lista wszystkie definicje metryk dla określonego zasobu.</span><span class="sxs-lookup"><span data-stu-id="744ec-140">You can use `Get-AzureRmMetricDefinition` tooview hello list of all metric definitions for a specific resource.</span></span>

     ```PowerShell
     Get-AzureRmMetricDefinition -ResourceId <resource_id>
     ```

     <span data-ttu-id="744ec-141">Witaj poniższy przykład generuje tabeli z metryką hello nazwy i hello jednostki dla tego metryki.</span><span class="sxs-lookup"><span data-stu-id="744ec-141">hello following example generates a table with hello metric Name and hello Unit for that metric.</span></span>

     ```PowerShell
     Get-AzureRmMetricDefinition -ResourceId <resource_id> | Format-Table -Property Name,Unit

     ```
     <span data-ttu-id="744ec-142">Pełną listę dostępnych opcji Get AzureRmMetricDefinition jest dostępna, uruchamiając polecenie Get-MetricDefinitions.</span><span class="sxs-lookup"><span data-stu-id="744ec-142">A full list of available options for Get-AzureRmMetricDefinition is available by running Get-MetricDefinitions.</span></span>
5. <span data-ttu-id="744ec-143">powitania po przykład konfiguruje alert o zasobów witryny sieci web.</span><span class="sxs-lookup"><span data-stu-id="744ec-143">hello following example sets up an alert on a web site resource.</span></span> <span data-ttu-id="744ec-144">Wyzwalacze alertu Hello zawsze, gdy odbierze spójnie cały ruch do 5 minut i ponownie po otrzymaniu żaden ruch na 5 minut.</span><span class="sxs-lookup"><span data-stu-id="744ec-144">hello alert triggers whenever it consistently receives any traffic for 5 minutes and again when it receives no traffic for 5 minutes.</span></span>

    ```PowerShell
    Add-AzureRmMetricAlertRule -Name myMetricRuleWithWebhookAndEmail -Location "East US" -ResourceGroup myresourcegroup -TargetResourceId /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename -MetricName "BytesReceived" -Operator GreaterThan -Threshold 2 -WindowSize 00:05:00 -TimeAggregationOperator Total -Description "alert on any website activity"

    ```
6. <span data-ttu-id="744ec-145">toocreate elementu webhook lub wysyłania wiadomości e-mail podczas wyzwala alert, najpierw utworzyć hello poczty e-mail i/lub elementów webhook.</span><span class="sxs-lookup"><span data-stu-id="744ec-145">toocreate webhook or send email when an alert triggers, first create hello email and/or webhooks.</span></span> <span data-ttu-id="744ec-146">Od razu utworzyć regułę hello później z hello - tag akcje i pokazane na powitania poniższy przykład.</span><span class="sxs-lookup"><span data-stu-id="744ec-146">Then immediately create hello rule afterwards with hello -Actions tag and as shown in hello following example.</span></span> <span data-ttu-id="744ec-147">Nie można skojarzyć elementu webhook lub wiadomości e-mail przy użyciu reguły za pomocą programu PowerShell już utworzone.</span><span class="sxs-lookup"><span data-stu-id="744ec-147">You cannot associate webhook or emails with already created rules via PowerShell.</span></span>

    ```PowerShell
    $actionEmail = New-AzureRmAlertRuleEmail -CustomEmail myname@company.com
    $actionWebhook = New-AzureRmAlertRuleWebhook -ServiceUri https://www.contoso.com?token=mytoken

    Add-AzureRmMetricAlertRule -Name myMetricRuleWithWebhookAndEmail -Location "East US" -ResourceGroup myresourcegroup -TargetResourceId /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename -MetricName "BytesReceived" -Operator GreaterThan -Threshold 2 -WindowSize 00:05:00 -TimeAggregationOperator Total -Actions $actionEmail, $actionWebhook -Description "alert on any website activity"
    ```

7. <span data-ttu-id="744ec-148">tooverify czy alerty zostały utworzone prawidłowo analizując hello poszczególnych reguł.</span><span class="sxs-lookup"><span data-stu-id="744ec-148">tooverify that your alerts have been created properly by looking at hello individual rules.</span></span>

    ```PowerShell
    Get-AzureRmAlertRule -Name myMetricRuleWithWebhookAndEmail -ResourceGroup myresourcegroup -DetailedOutput

    Get-AzureRmAlertRule -Name myLogAlertRule -ResourceGroup myresourcegroup -DetailedOutput
    ```
8. <span data-ttu-id="744ec-149">Usuń alerty.</span><span class="sxs-lookup"><span data-stu-id="744ec-149">Delete your alerts.</span></span> <span data-ttu-id="744ec-150">Te polecenia usuwania reguł hello utworzonej wcześniej w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="744ec-150">These commands delete hello rules created previously in this article.</span></span>

    ```PowerShell
    Remove-AzureRmAlertRule -ResourceGroup myresourcegroup -Name myrule
    Remove-AzureRmAlertRule -ResourceGroup myresourcegroup -Name myMetricRuleWithWebhookAndEmail
    Remove-AzureRmAlertRule -ResourceGroup myresourcegroup -Name myLogAlertRule
    ```

## <a name="next-steps"></a><span data-ttu-id="744ec-151">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="744ec-151">Next steps</span></span>
* <span data-ttu-id="744ec-152">[Omówienie monitorowania Azure](monitoring-overview.md) tym hello typy informacji, można zbierać i monitorowania.</span><span class="sxs-lookup"><span data-stu-id="744ec-152">[Get an overview of Azure monitoring](monitoring-overview.md) including hello types of information you can collect and monitor.</span></span>
* <span data-ttu-id="744ec-153">Dowiedz się więcej o [konfigurowaniu elementów webhook w alertach](insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="744ec-153">Learn more about [configuring webhooks in alerts](insights-webhooks-alerts.md).</span></span>
* <span data-ttu-id="744ec-154">Dowiedz się więcej o [konfigurowania alertów na zdarzenia dziennika aktywności](monitoring-activity-log-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="744ec-154">Learn more about [configuring alerts on Activity log events](monitoring-activity-log-alerts.md).</span></span>
* <span data-ttu-id="744ec-155">Dowiedz się więcej o [elementów Runbook automatyzacji Azure](../automation/automation-starting-a-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="744ec-155">Learn more about [Azure Automation Runbooks](../automation/automation-starting-a-runbook.md).</span></span>
* <span data-ttu-id="744ec-156">Pobierz [omówienie zbierania dzienników diagnostycznych](monitoring-overview-of-diagnostic-logs.md) toocollect szczegółowe metryki wysokiej częstotliwości w usłudze.</span><span class="sxs-lookup"><span data-stu-id="744ec-156">Get an [overview of collecting diagnostic logs](monitoring-overview-of-diagnostic-logs.md) toocollect detailed high-frequency metrics on your service.</span></span>
* <span data-ttu-id="744ec-157">Pobierz [omówienie zbierania metryk](insights-how-to-customize-monitoring.md) toomake się, że usługa jest dostępna i elastyczny.</span><span class="sxs-lookup"><span data-stu-id="744ec-157">Get an [overview of metrics collection](insights-how-to-customize-monitoring.md) toomake sure your service is available and responsive.</span></span>
