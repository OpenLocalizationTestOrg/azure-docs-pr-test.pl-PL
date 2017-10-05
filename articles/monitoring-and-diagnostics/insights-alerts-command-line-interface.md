---
title: "Utwórz alerty dla usług Azure - CLI wieloplatformowych | Dokumentacja firmy Microsoft"
description: "Wyzwalacz wiadomości e-mail, powiadomienia, Wywołaj adresy URL witryny sieci Web (elementy webhook) lub automatyzacji po spełnieniu warunków, które określisz."
author: rboucher
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 5c6a2d27-7dcc-4f89-8752-9bb31b05ff35
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: robb
ms.openlocfilehash: 92246a8da73a244a1c9a924bed55711d71a20fd8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-metric-alerts-in-azure-monitor-for-azure-services---cross-platform-cli"></a><span data-ttu-id="4f5c5-103">Tworzenie metryki alertów w monitorze Azure dla usług Azure - CLI między platformami</span><span class="sxs-lookup"><span data-stu-id="4f5c5-103">Create metric alerts in Azure Monitor for Azure services - Cross-platform CLI</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4f5c5-104">Portal</span><span class="sxs-lookup"><span data-stu-id="4f5c5-104">Portal</span></span>](insights-alerts-portal.md)
> * [<span data-ttu-id="4f5c5-105">Program PowerShell</span><span class="sxs-lookup"><span data-stu-id="4f5c5-105">PowerShell</span></span>](insights-alerts-powershell.md)
> * [<span data-ttu-id="4f5c5-106">Interfejs wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="4f5c5-106">CLI</span></span>](insights-alerts-command-line-interface.md)
>
>

## <a name="overview"></a><span data-ttu-id="4f5c5-107">Omówienie</span><span class="sxs-lookup"><span data-stu-id="4f5c5-107">Overview</span></span>
<span data-ttu-id="4f5c5-108">W tym artykule przedstawiono sposób konfigurowania Azure metryki alertów za pomocą interfejsu wiersza polecenia i platform (CLI).</span><span class="sxs-lookup"><span data-stu-id="4f5c5-108">This article shows you how to set up Azure metric alerts using the cross-platform Command Line Interface (CLI).</span></span>

> [!NOTE]
> <span data-ttu-id="4f5c5-109">Azure Monitor to nowa nazwa dla proponowaną "Azure Insights" do 25 września 2016 r.</span><span class="sxs-lookup"><span data-stu-id="4f5c5-109">Azure Monitor is the new name for what was called "Azure Insights" until Sept 25th, 2016.</span></span> <span data-ttu-id="4f5c5-110">Jednak przestrzenie nazw, dlatego poniższe polecenia nadal zawierają "insights".</span><span class="sxs-lookup"><span data-stu-id="4f5c5-110">However, the namespaces and thus the commands below still contain the "insights".</span></span>
>
>

<span data-ttu-id="4f5c5-111">Możesz otrzymywać alertu na podstawie metryki monitorowania lub zdarzenia na usługami Azure.</span><span class="sxs-lookup"><span data-stu-id="4f5c5-111">You can receive an alert based on monitoring metrics for, or events on, your Azure services.</span></span>

* <span data-ttu-id="4f5c5-112">**Wartości metryki** — uruchamia alert, gdy wartość określonej metryki przekracza próg przypisać w żadnym kierunku.</span><span class="sxs-lookup"><span data-stu-id="4f5c5-112">**Metric values** - The alert triggers when the value of a specified metric crosses a threshold you assign in either direction.</span></span> <span data-ttu-id="4f5c5-113">Oznacza to, że oba wyzwala po spełnieniu warunku zostanie najpierw i następnie później podczas warunku jest już spełniane.</span><span class="sxs-lookup"><span data-stu-id="4f5c5-113">That is, it triggers both when the condition is first met and then afterwards when that condition is no longer being met.</span></span>    
* <span data-ttu-id="4f5c5-114">**Zdarzenia dziennika aktywności** — alert może wyzwolić na *co* zdarzenia lub tylko wtedy, gdy występuje określone zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="4f5c5-114">**Activity log events** - An alert can trigger on *every* event, or, only when a certain events occurs.</span></span> <span data-ttu-id="4f5c5-115">Aby dowiedzieć się więcej o alertach dziennika aktywności [kliknij tutaj](monitoring-activity-log-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="4f5c5-115">To learn more about activity log alerts [click here](monitoring-activity-log-alerts.md)</span></span>

<span data-ttu-id="4f5c5-116">Można skonfigurować metryki alert do wyzwala, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="4f5c5-116">You can configure a metric alert to do the following when it triggers:</span></span>

* <span data-ttu-id="4f5c5-117">wysyłanie powiadomień e-mail do administratora usługi i współadministratorzy</span><span class="sxs-lookup"><span data-stu-id="4f5c5-117">send email notifications to the service administrator and co-administrators</span></span>
* <span data-ttu-id="4f5c5-118">Wyślij wiadomość e-mail do dodatkowych wiadomości e-mail przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="4f5c5-118">send email to additional emails that you specify.</span></span>
* <span data-ttu-id="4f5c5-119">Wywołanie elementu webhook</span><span class="sxs-lookup"><span data-stu-id="4f5c5-119">call a webhook</span></span>
* <span data-ttu-id="4f5c5-120">Uruchamia wykonywanie elementów runbook platformy Azure (tylko z portalu Azure w tej chwili)</span><span class="sxs-lookup"><span data-stu-id="4f5c5-120">start execution of an Azure runbook (only from the Azure portal at this time)</span></span>

<span data-ttu-id="4f5c5-121">Można skonfigurować i uzyskać informacje na temat metryki reguły alertów za pomocą</span><span class="sxs-lookup"><span data-stu-id="4f5c5-121">You can configure and get information about metric alert rules using</span></span>

* [<span data-ttu-id="4f5c5-122">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="4f5c5-122">Azure portal</span></span>](insights-alerts-portal.md)
* [<span data-ttu-id="4f5c5-123">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4f5c5-123">PowerShell</span></span>](insights-alerts-powershell.md)
* [<span data-ttu-id="4f5c5-124">Interfejs wiersza polecenia (CLI)</span><span class="sxs-lookup"><span data-stu-id="4f5c5-124">command-line interface (CLI)</span></span>](insights-alerts-command-line-interface.md)
* [<span data-ttu-id="4f5c5-125">Interfejs API REST Azure monitora</span><span class="sxs-lookup"><span data-stu-id="4f5c5-125">Azure Monitor REST API</span></span>](https://msdn.microsoft.com/library/azure/dn931945.aspx)

<span data-ttu-id="4f5c5-126">Zawsze może odbierać pomocy dla poleceń, wpisując polecenie i odkładanie — pomoc na końcu.</span><span class="sxs-lookup"><span data-stu-id="4f5c5-126">You can always receive help for commands by typing a command and putting -help at the end.</span></span> <span data-ttu-id="4f5c5-127">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="4f5c5-127">For example:</span></span>

    ```console
    azure insights alerts -help
    azure insights alerts actions email create -help
    ```

## <a name="create-alert-rules-using-the-cli"></a><span data-ttu-id="4f5c5-128">Tworzyć reguły alertów za pomocą interfejsu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="4f5c5-128">Create alert rules using the CLI</span></span>
1. <span data-ttu-id="4f5c5-129">Wykonaj warunki wstępne i logowania do platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="4f5c5-129">Perform the Prerequisites and login to Azure.</span></span> <span data-ttu-id="4f5c5-130">Zobacz [przykłady interfejsu wiersza polecenia Azure Monitor](insights-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="4f5c5-130">See [Azure Monitor CLI samples](insights-cli-samples.md).</span></span> <span data-ttu-id="4f5c5-131">Krótko mówiąc instalowanie interfejsu wiersza polecenia i uruchom następujące polecenia.</span><span class="sxs-lookup"><span data-stu-id="4f5c5-131">In short, install the CLI and run these commands.</span></span> <span data-ttu-id="4f5c5-132">Ona się zalogować, Pokaż subskrypcję, a przygotowanie do uruchomienia poleceń Azure monitora.</span><span class="sxs-lookup"><span data-stu-id="4f5c5-132">They get you logged in, show what subscription you are using, and prepare you to run Azure Monitor commands.</span></span>

    ```console
    azure login
    azure account show
    azure config mode arm

    ```

2. <span data-ttu-id="4f5c5-133">Aby wyświetlić listę istniejących reguł dla grupy zasobów, użyj następującej składni **insights azure alerty reguły listy** *[opcje] &lt;grupa zasobów&gt;*</span><span class="sxs-lookup"><span data-stu-id="4f5c5-133">To list existing rules on a resource group, use the following form **azure insights alerts rule list** *[options] &lt;resourceGroup&gt;*</span></span>

   ```console
   azure insights alerts rule list myresourcegroupname

   ```
3. <span data-ttu-id="4f5c5-134">Aby utworzyć regułę, musisz mieć najpierw kilku ważnych informacji.</span><span class="sxs-lookup"><span data-stu-id="4f5c5-134">To create a rule, you need to have several important pieces of information first.</span></span>
  * <span data-ttu-id="4f5c5-135">**Identyfikator zasobu** dla zasobu, aby ustawić alert dla</span><span class="sxs-lookup"><span data-stu-id="4f5c5-135">The **Resource ID** for the resource you want to set an alert for</span></span>
  * <span data-ttu-id="4f5c5-136">**Definicji metryk** dostępne dla tego zasobu</span><span class="sxs-lookup"><span data-stu-id="4f5c5-136">The **metric definitions** available for that resource</span></span>

     <span data-ttu-id="4f5c5-137">Jednym ze sposobów Pobierz identyfikator zasobu jest korzystanie z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="4f5c5-137">One way to get the Resource ID is to use the Azure portal.</span></span> <span data-ttu-id="4f5c5-138">Zakładając, że zasób został już utworzony, wybierz go w portalu.</span><span class="sxs-lookup"><span data-stu-id="4f5c5-138">Assuming the resource is already created, select it in the portal.</span></span> <span data-ttu-id="4f5c5-139">Następnie w bloku dalej wybierz *właściwości* w obszarze *ustawienia* sekcji.</span><span class="sxs-lookup"><span data-stu-id="4f5c5-139">Then in the next blade, select *Properties* under the *Settings* section.</span></span> <span data-ttu-id="4f5c5-140">*Identyfikator ZASOBU* jest polem w następnym bloku.</span><span class="sxs-lookup"><span data-stu-id="4f5c5-140">The *RESOURCE ID* is a field in the next blade.</span></span> <span data-ttu-id="4f5c5-141">Innym sposobem jest użycie [Eksploratora zasobów Azure](https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="4f5c5-141">Another way is to use the [Azure Resource Explorer](https://resources.azure.com/).</span></span>

     <span data-ttu-id="4f5c5-142">Identyfikator zasobu przykład dla aplikacji sieci web jest</span><span class="sxs-lookup"><span data-stu-id="4f5c5-142">An example resource id for a web app is</span></span>

     ```console
     /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename
     ```

     <span data-ttu-id="4f5c5-143">Aby uzyskać listę dostępnych metryk i jednostki dla tych metryk w poprzednim przykładzie zasobów, użyj następującego polecenia interfejsu wiersza polecenia:</span><span class="sxs-lookup"><span data-stu-id="4f5c5-143">To get a list of the available metrics and units for those metrics for the previous resource example, use the following CLI command:</span></span>  

     ```console
     azure insights metrics list /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename PT1M
     ```

     <span data-ttu-id="4f5c5-144">*PT1M* jest stopień szczegółowości miary dostępne (1-minutowy).</span><span class="sxs-lookup"><span data-stu-id="4f5c5-144">*PT1M* is the granularity of the available measurement (1-minute intervals).</span></span> <span data-ttu-id="4f5c5-145">Przy użyciu różnych szczegółowości zapewnia różne opcje metryki.</span><span class="sxs-lookup"><span data-stu-id="4f5c5-145">Using different granularities gives you different metric options.</span></span>
4. <span data-ttu-id="4f5c5-146">Aby utworzyć regułę alertu metryki, użyj polecenia mają następującą postać:</span><span class="sxs-lookup"><span data-stu-id="4f5c5-146">To create a metric-based alert rule, use a command of the following form:</span></span>

    <span data-ttu-id="4f5c5-147">**Azure insights metryki zestaw reguł alertów** *[opcje] &lt;ruleName&gt; &lt;lokalizacji&gt; &lt;resourceGroup&gt; &lt;Rozmiar_okna&gt; &lt;operator&gt; &lt;próg&gt; &lt;element targetResourceId&gt; &lt;metricName&gt; &lt;timeAggregationOperator&gt;*</span><span class="sxs-lookup"><span data-stu-id="4f5c5-147">**azure insights alerts rule metric set** *[options] &lt;ruleName&gt; &lt;location&gt; &lt;resourceGroup&gt; &lt;windowSize&gt; &lt;operator&gt; &lt;threshold&gt; &lt;targetResourceId&gt; &lt;metricName&gt; &lt;timeAggregationOperator&gt;*</span></span>

    <span data-ttu-id="4f5c5-148">Poniższy przykład powoduje ustawienie alertu dla zasobu witryny sieci web.</span><span class="sxs-lookup"><span data-stu-id="4f5c5-148">The following example sets up an alert on a web site resource.</span></span> <span data-ttu-id="4f5c5-149">Wyzwalacze alertu zawsze, gdy odbierze spójnie cały ruch do 5 minut i ponownie po otrzymaniu żaden ruch na 5 minut.</span><span class="sxs-lookup"><span data-stu-id="4f5c5-149">The alert triggers whenever it consistently receives any traffic for 5 minutes and again when it receives no traffic for 5 minutes.</span></span>

    ```console
    azure insights alerts rule metric set myrule eastus myreasourcegroup PT5M GreaterThan 2 /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename BytesReceived Total

    ```
5. <span data-ttu-id="4f5c5-150">Aby utworzyć elementu webhook lub Wyślij wiadomość e-mail po zgłoszeniu alertu metryki, należy najpierw utworzyć wiadomości e-mail i/lub elementów webhook.</span><span class="sxs-lookup"><span data-stu-id="4f5c5-150">To create webhook or send email when a metric alert fires, first create the email and/or webhooks.</span></span> <span data-ttu-id="4f5c5-151">Od razu utworzyć regułę później.</span><span class="sxs-lookup"><span data-stu-id="4f5c5-151">Then create the rule immediately afterwards.</span></span> <span data-ttu-id="4f5c5-152">Nie można skojarzyć elementu webhook lub wiadomości e-mail przy użyciu już utworzone zasady przy użyciu interfejsu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="4f5c5-152">You cannot associate webhook or emails with already created rules using the CLI.</span></span>

    ```console
    azure insights alerts actions email create --customEmails myemail@contoso.com

    azure insights alerts actions webhook create https://www.contoso.com

    azure insights alerts rule metric set myrulewithwebhookandemail eastus myreasourcegroup PT5M GreaterThan 2 /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename BytesReceived Total
    ```

6. <span data-ttu-id="4f5c5-153">Aby sprawdzić, czy alerty zostały utworzone prawidłowo analizując poszczególnych reguł.</span><span class="sxs-lookup"><span data-stu-id="4f5c5-153">You can verify that your alerts have been created properly by looking at an individual rule.</span></span>

    ```console
    azure insights alerts rule list myresourcegroup --ruleName myrule
    ```
7. <span data-ttu-id="4f5c5-154">Aby usunąć zasady, użyj polecenia formularza:</span><span class="sxs-lookup"><span data-stu-id="4f5c5-154">To delete rules, use a command of the form:</span></span>

    <span data-ttu-id="4f5c5-155">**szczegółowe informacje, Usuń regułę alertów** [opcje] &lt;resourceGroup&gt; &lt;ruleName&gt;</span><span class="sxs-lookup"><span data-stu-id="4f5c5-155">**insights alerts rule delete** [options] &lt;resourceGroup&gt; &lt;ruleName&gt;</span></span>

    <span data-ttu-id="4f5c5-156">Te polecenia usuwania reguł utworzonych wcześniej w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="4f5c5-156">These commands delete the rules previously created in this article.</span></span>

    ```console
    azure insights alerts rule delete myresourcegroup myrule
    azure insights alerts rule delete myresourcegroup myrulewithwebhookandemail
    azure insights alerts rule delete myresourcegroup myActivityLogRule
    ```

## <a name="next-steps"></a><span data-ttu-id="4f5c5-157">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="4f5c5-157">Next steps</span></span>
* <span data-ttu-id="4f5c5-158">[Omówienie monitorowania Azure](monitoring-overview.md) w tym typy informacji, można zbierać i monitorowania.</span><span class="sxs-lookup"><span data-stu-id="4f5c5-158">[Get an overview of Azure monitoring](monitoring-overview.md) including the types of information you can collect and monitor.</span></span>
* <span data-ttu-id="4f5c5-159">Dowiedz się więcej o [konfigurowaniu elementów webhook w alertach](insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="4f5c5-159">Learn more about [configuring webhooks in alerts](insights-webhooks-alerts.md).</span></span>
* <span data-ttu-id="4f5c5-160">Dowiedz się więcej o [konfigurowania alertów na zdarzenia dziennika aktywności](monitoring-activity-log-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="4f5c5-160">Learn more about [configuring alerts on Activity log events](monitoring-activity-log-alerts.md).</span></span>
* <span data-ttu-id="4f5c5-161">Dowiedz się więcej o [elementów Runbook automatyzacji Azure](../automation/automation-starting-a-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="4f5c5-161">Learn more about [Azure Automation Runbooks](../automation/automation-starting-a-runbook.md).</span></span>
* <span data-ttu-id="4f5c5-162">Pobierz [omówienie zbierania dzienników diagnostycznych](monitoring-overview-of-diagnostic-logs.md) zbierania szczegółowych o dużej częstotliwości metryk usługi.</span><span class="sxs-lookup"><span data-stu-id="4f5c5-162">Get an [overview of collecting diagnostic logs](monitoring-overview-of-diagnostic-logs.md) to collect detailed high-frequency metrics on your service.</span></span>
* <span data-ttu-id="4f5c5-163">Pobierz [omówienie zbierania metryk](insights-how-to-customize-monitoring.md) się upewnić, że usługa jest dostępna i elastyczny.</span><span class="sxs-lookup"><span data-stu-id="4f5c5-163">Get an [overview of metrics collection](insights-how-to-customize-monitoring.md) to make sure your service is available and responsive.</span></span>
