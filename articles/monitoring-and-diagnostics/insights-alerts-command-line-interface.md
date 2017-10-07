---
title: "aaaCreate alerty dla usług Azure - CLI wieloplatformowych | Dokumentacja firmy Microsoft"
description: "Gdy są spełnione warunki hello wyzwolenia wiadomości e-mail, powiadomienia, adresy URL witryny sieci Web wywołania (elementy webhook) lub automatyzacji."
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
ms.openlocfilehash: e53701e5377a415038a69fbd32f1e5fc5fe99be9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-metric-alerts-in-azure-monitor-for-azure-services---cross-platform-cli"></a><span data-ttu-id="7385c-103">Tworzenie metryki alertów w monitorze Azure dla usług Azure - CLI między platformami</span><span class="sxs-lookup"><span data-stu-id="7385c-103">Create metric alerts in Azure Monitor for Azure services - Cross-platform CLI</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7385c-104">Portal</span><span class="sxs-lookup"><span data-stu-id="7385c-104">Portal</span></span>](insights-alerts-portal.md)
> * [<span data-ttu-id="7385c-105">Program PowerShell</span><span class="sxs-lookup"><span data-stu-id="7385c-105">PowerShell</span></span>](insights-alerts-powershell.md)
> * [<span data-ttu-id="7385c-106">Interfejs wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="7385c-106">CLI</span></span>](insights-alerts-command-line-interface.md)
>
>

## <a name="overview"></a><span data-ttu-id="7385c-107">Omówienie</span><span class="sxs-lookup"><span data-stu-id="7385c-107">Overview</span></span>
<span data-ttu-id="7385c-108">W tym artykule opisano, jak tooset Azure metryki alerty za pomocą hello wieloplatformowych interfejsu wiersza polecenia (CLI).</span><span class="sxs-lookup"><span data-stu-id="7385c-108">This article shows you how tooset up Azure metric alerts using hello cross-platform Command Line Interface (CLI).</span></span>

> [!NOTE]
> <span data-ttu-id="7385c-109">Azure Monitor jest nową nazwę hello proponowaną "Azure Insights" do 25 września 2016 r.</span><span class="sxs-lookup"><span data-stu-id="7385c-109">Azure Monitor is hello new name for what was called "Azure Insights" until Sept 25th, 2016.</span></span> <span data-ttu-id="7385c-110">Jednak hello przestrzeni nazw, dlatego poniższe polecenia hello nadal zawierać hello "insights".</span><span class="sxs-lookup"><span data-stu-id="7385c-110">However, hello namespaces and thus hello commands below still contain hello "insights".</span></span>
>
>

<span data-ttu-id="7385c-111">Możesz otrzymywać alertu na podstawie metryki monitorowania lub zdarzenia na usługami Azure.</span><span class="sxs-lookup"><span data-stu-id="7385c-111">You can receive an alert based on monitoring metrics for, or events on, your Azure services.</span></span>

* <span data-ttu-id="7385c-112">**Wartości metryki** — Witaj alertu wyzwalacze, jeśli wartość hello określonej metryki przecina próg przypisać w żadnym kierunku.</span><span class="sxs-lookup"><span data-stu-id="7385c-112">**Metric values** - hello alert triggers when hello value of a specified metric crosses a threshold you assign in either direction.</span></span> <span data-ttu-id="7385c-113">Oznacza to, że oba wyzwala kiedy najpierw zostanie spełniony warunek hello i następnie później podczas warunku jest już spełniane.</span><span class="sxs-lookup"><span data-stu-id="7385c-113">That is, it triggers both when hello condition is first met and then afterwards when that condition is no longer being met.</span></span>    
* <span data-ttu-id="7385c-114">**Zdarzenia dziennika aktywności** — alert może wyzwolić na *co* zdarzenia lub tylko wtedy, gdy występuje określone zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="7385c-114">**Activity log events** - An alert can trigger on *every* event, or, only when a certain events occurs.</span></span> <span data-ttu-id="7385c-115">więcej informacji na temat alertów dotyczących działań w dzienniku toolearn [kliknij tutaj](monitoring-activity-log-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="7385c-115">toolearn more about activity log alerts [click here](monitoring-activity-log-alerts.md)</span></span>

<span data-ttu-id="7385c-116">Można skonfigurować hello metryki toodo alertów po, wyzwala:</span><span class="sxs-lookup"><span data-stu-id="7385c-116">You can configure a metric alert toodo hello following when it triggers:</span></span>

* <span data-ttu-id="7385c-117">Wyślij administratora usługi toohello powiadomienia e-mail i współadministratorzy</span><span class="sxs-lookup"><span data-stu-id="7385c-117">send email notifications toohello service administrator and co-administrators</span></span>
* <span data-ttu-id="7385c-118">Wyślij wiadomość e-mail tooadditional wiadomości e-mail, które określisz.</span><span class="sxs-lookup"><span data-stu-id="7385c-118">send email tooadditional emails that you specify.</span></span>
* <span data-ttu-id="7385c-119">Wywołanie elementu webhook</span><span class="sxs-lookup"><span data-stu-id="7385c-119">call a webhook</span></span>
* <span data-ttu-id="7385c-120">Uruchamia wykonywanie elementów runbook platformy Azure (tylko z portalu Azure w tej chwili hello)</span><span class="sxs-lookup"><span data-stu-id="7385c-120">start execution of an Azure runbook (only from hello Azure portal at this time)</span></span>

<span data-ttu-id="7385c-121">Można skonfigurować i uzyskać informacje na temat metryki reguły alertów za pomocą</span><span class="sxs-lookup"><span data-stu-id="7385c-121">You can configure and get information about metric alert rules using</span></span>

* [<span data-ttu-id="7385c-122">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="7385c-122">Azure portal</span></span>](insights-alerts-portal.md)
* [<span data-ttu-id="7385c-123">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7385c-123">PowerShell</span></span>](insights-alerts-powershell.md)
* [<span data-ttu-id="7385c-124">Interfejs wiersza polecenia (CLI)</span><span class="sxs-lookup"><span data-stu-id="7385c-124">command-line interface (CLI)</span></span>](insights-alerts-command-line-interface.md)
* [<span data-ttu-id="7385c-125">Interfejs API REST Azure monitora</span><span class="sxs-lookup"><span data-stu-id="7385c-125">Azure Monitor REST API</span></span>](https://msdn.microsoft.com/library/azure/dn931945.aspx)

<span data-ttu-id="7385c-126">Zawsze może odbierać pomocy dla poleceń, wpisując polecenie i odkładanie — pomoc na końcu hello.</span><span class="sxs-lookup"><span data-stu-id="7385c-126">You can always receive help for commands by typing a command and putting -help at hello end.</span></span> <span data-ttu-id="7385c-127">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="7385c-127">For example:</span></span>

    ```console
    azure insights alerts -help
    azure insights alerts actions email create -help
    ```

## <a name="create-alert-rules-using-hello-cli"></a><span data-ttu-id="7385c-128">Tworzyć reguły alertów za pomocą hello interfejsu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="7385c-128">Create alert rules using hello CLI</span></span>
1. <span data-ttu-id="7385c-129">Wykonaj hello warunki wstępne i tooAzure logowania.</span><span class="sxs-lookup"><span data-stu-id="7385c-129">Perform hello Prerequisites and login tooAzure.</span></span> <span data-ttu-id="7385c-130">Zobacz [przykłady interfejsu wiersza polecenia Azure Monitor](insights-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="7385c-130">See [Azure Monitor CLI samples](insights-cli-samples.md).</span></span> <span data-ttu-id="7385c-131">Krótko mówiąc Zainstaluj hello interfejsu wiersza polecenia i uruchom następujące polecenia.</span><span class="sxs-lookup"><span data-stu-id="7385c-131">In short, install hello CLI and run these commands.</span></span> <span data-ttu-id="7385c-132">One się zalogować, Pokaż subskrypcję, a przygotowanie toorun poleceń Azure monitora.</span><span class="sxs-lookup"><span data-stu-id="7385c-132">They get you logged in, show what subscription you are using, and prepare you toorun Azure Monitor commands.</span></span>

    ```console
    azure login
    azure account show
    azure config mode arm

    ```

2. <span data-ttu-id="7385c-133">toolist istniejących reguł dla grupy zasobów, użyj powitania po formularza **insights azure alerty reguły listy** *[opcje] &lt;grupa zasobów&gt;*</span><span class="sxs-lookup"><span data-stu-id="7385c-133">toolist existing rules on a resource group, use hello following form **azure insights alerts rule list** *[options] &lt;resourceGroup&gt;*</span></span>

   ```console
   azure insights alerts rule list myresourcegroupname

   ```
3. <span data-ttu-id="7385c-134">toocreate regułę, należy toohave kilku ważnych informacji najpierw.</span><span class="sxs-lookup"><span data-stu-id="7385c-134">toocreate a rule, you need toohave several important pieces of information first.</span></span>
  * <span data-ttu-id="7385c-135">Witaj **identyfikator zasobu** hello zasobu ma tooset alert dla</span><span class="sxs-lookup"><span data-stu-id="7385c-135">hello **Resource ID** for hello resource you want tooset an alert for</span></span>
  * <span data-ttu-id="7385c-136">Witaj **definicji metryk** dostępne dla tego zasobu</span><span class="sxs-lookup"><span data-stu-id="7385c-136">hello **metric definitions** available for that resource</span></span>

     <span data-ttu-id="7385c-137">Jednym ze sposobów tooget hello identyfikator zasobu jest hello toouse portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="7385c-137">One way tooget hello Resource ID is toouse hello Azure portal.</span></span> <span data-ttu-id="7385c-138">Zakładając, że zasób hello został już utworzony, wybierz go w portalu hello.</span><span class="sxs-lookup"><span data-stu-id="7385c-138">Assuming hello resource is already created, select it in hello portal.</span></span> <span data-ttu-id="7385c-139">Następnie w bloku dalej hello, wybierz *właściwości* w obszarze hello *ustawienia* sekcji.</span><span class="sxs-lookup"><span data-stu-id="7385c-139">Then in hello next blade, select *Properties* under hello *Settings* section.</span></span> <span data-ttu-id="7385c-140">Witaj *identyfikator ZASOBU* jest polem w następnym bloku hello.</span><span class="sxs-lookup"><span data-stu-id="7385c-140">hello *RESOURCE ID* is a field in hello next blade.</span></span> <span data-ttu-id="7385c-141">Innym sposobem jest toouse hello [Eksploratora zasobów Azure](https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="7385c-141">Another way is toouse hello [Azure Resource Explorer](https://resources.azure.com/).</span></span>

     <span data-ttu-id="7385c-142">Identyfikator zasobu przykład dla aplikacji sieci web jest</span><span class="sxs-lookup"><span data-stu-id="7385c-142">An example resource id for a web app is</span></span>

     ```console
     /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename
     ```

     <span data-ttu-id="7385c-143">tooget listę hello dostępne metryki i jednostki dla tych metryki, np. hello poprzedniego zasobu hello Użyj następującego polecenia interfejsu wiersza polecenia:</span><span class="sxs-lookup"><span data-stu-id="7385c-143">tooget a list of hello available metrics and units for those metrics for hello previous resource example, use hello following CLI command:</span></span>  

     ```console
     azure insights metrics list /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename PT1M
     ```

     <span data-ttu-id="7385c-144">*PT1M* jest hello szczegółowości miary dostępne hello (1-minutowy).</span><span class="sxs-lookup"><span data-stu-id="7385c-144">*PT1M* is hello granularity of hello available measurement (1-minute intervals).</span></span> <span data-ttu-id="7385c-145">Przy użyciu różnych szczegółowości zapewnia różne opcje metryki.</span><span class="sxs-lookup"><span data-stu-id="7385c-145">Using different granularities gives you different metric options.</span></span>
4. <span data-ttu-id="7385c-146">toocreate metryki na podstawie reguły alertu, polecenie hello następującej postaci:</span><span class="sxs-lookup"><span data-stu-id="7385c-146">toocreate a metric-based alert rule, use a command of hello following form:</span></span>

    <span data-ttu-id="7385c-147">**Azure insights metryki zestaw reguł alertów** *[opcje] &lt;ruleName&gt; &lt;lokalizacji&gt; &lt;resourceGroup&gt; &lt;Rozmiar_okna&gt; &lt;operator&gt; &lt;próg&gt; &lt;element targetResourceId&gt; &lt;metricName&gt; &lt;timeAggregationOperator&gt;*</span><span class="sxs-lookup"><span data-stu-id="7385c-147">**azure insights alerts rule metric set** *[options] &lt;ruleName&gt; &lt;location&gt; &lt;resourceGroup&gt; &lt;windowSize&gt; &lt;operator&gt; &lt;threshold&gt; &lt;targetResourceId&gt; &lt;metricName&gt; &lt;timeAggregationOperator&gt;*</span></span>

    <span data-ttu-id="7385c-148">powitania po przykład konfiguruje alert o zasobów witryny sieci web.</span><span class="sxs-lookup"><span data-stu-id="7385c-148">hello following example sets up an alert on a web site resource.</span></span> <span data-ttu-id="7385c-149">Wyzwalacze alertu Hello zawsze, gdy odbierze spójnie cały ruch do 5 minut i ponownie po otrzymaniu żaden ruch na 5 minut.</span><span class="sxs-lookup"><span data-stu-id="7385c-149">hello alert triggers whenever it consistently receives any traffic for 5 minutes and again when it receives no traffic for 5 minutes.</span></span>

    ```console
    azure insights alerts rule metric set myrule eastus myreasourcegroup PT5M GreaterThan 2 /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename BytesReceived Total

    ```
5. <span data-ttu-id="7385c-150">toocreate elementu webhook lub Wyślij wiadomość e-mail po zgłoszeniu alertu metryki, najpierw utwórz hello poczty e-mail i/lub elementów webhook.</span><span class="sxs-lookup"><span data-stu-id="7385c-150">toocreate webhook or send email when a metric alert fires, first create hello email and/or webhooks.</span></span> <span data-ttu-id="7385c-151">Od razu utworzyć regułę hello później.</span><span class="sxs-lookup"><span data-stu-id="7385c-151">Then create hello rule immediately afterwards.</span></span> <span data-ttu-id="7385c-152">Nie można skojarzyć elementu webhook lub wiadomości e-mail przy użyciu już utworzone przy użyciu interfejsu wiersza polecenia hello reguły.</span><span class="sxs-lookup"><span data-stu-id="7385c-152">You cannot associate webhook or emails with already created rules using hello CLI.</span></span>

    ```console
    azure insights alerts actions email create --customEmails myemail@contoso.com

    azure insights alerts actions webhook create https://www.contoso.com

    azure insights alerts rule metric set myrulewithwebhookandemail eastus myreasourcegroup PT5M GreaterThan 2 /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename BytesReceived Total
    ```

6. <span data-ttu-id="7385c-153">Aby sprawdzić, czy alerty zostały utworzone prawidłowo analizując poszczególnych reguł.</span><span class="sxs-lookup"><span data-stu-id="7385c-153">You can verify that your alerts have been created properly by looking at an individual rule.</span></span>

    ```console
    azure insights alerts rule list myresourcegroup --ruleName myrule
    ```
7. <span data-ttu-id="7385c-154">reguły toodelete polecenie hello formularza:</span><span class="sxs-lookup"><span data-stu-id="7385c-154">toodelete rules, use a command of hello form:</span></span>

    <span data-ttu-id="7385c-155">**szczegółowe informacje, Usuń regułę alertów** [opcje] &lt;resourceGroup&gt; &lt;ruleName&gt;</span><span class="sxs-lookup"><span data-stu-id="7385c-155">**insights alerts rule delete** [options] &lt;resourceGroup&gt; &lt;ruleName&gt;</span></span>

    <span data-ttu-id="7385c-156">Te polecenia usuwania reguł hello utworzony wcześniej w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="7385c-156">These commands delete hello rules previously created in this article.</span></span>

    ```console
    azure insights alerts rule delete myresourcegroup myrule
    azure insights alerts rule delete myresourcegroup myrulewithwebhookandemail
    azure insights alerts rule delete myresourcegroup myActivityLogRule
    ```

## <a name="next-steps"></a><span data-ttu-id="7385c-157">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="7385c-157">Next steps</span></span>
* <span data-ttu-id="7385c-158">[Omówienie monitorowania Azure](monitoring-overview.md) tym hello typy informacji, można zbierać i monitorowania.</span><span class="sxs-lookup"><span data-stu-id="7385c-158">[Get an overview of Azure monitoring](monitoring-overview.md) including hello types of information you can collect and monitor.</span></span>
* <span data-ttu-id="7385c-159">Dowiedz się więcej o [konfigurowaniu elementów webhook w alertach](insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="7385c-159">Learn more about [configuring webhooks in alerts](insights-webhooks-alerts.md).</span></span>
* <span data-ttu-id="7385c-160">Dowiedz się więcej o [konfigurowania alertów na zdarzenia dziennika aktywności](monitoring-activity-log-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="7385c-160">Learn more about [configuring alerts on Activity log events](monitoring-activity-log-alerts.md).</span></span>
* <span data-ttu-id="7385c-161">Dowiedz się więcej o [elementów Runbook automatyzacji Azure](../automation/automation-starting-a-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="7385c-161">Learn more about [Azure Automation Runbooks](../automation/automation-starting-a-runbook.md).</span></span>
* <span data-ttu-id="7385c-162">Pobierz [omówienie zbierania dzienników diagnostycznych](monitoring-overview-of-diagnostic-logs.md) toocollect szczegółowe metryki wysokiej częstotliwości w usłudze.</span><span class="sxs-lookup"><span data-stu-id="7385c-162">Get an [overview of collecting diagnostic logs](monitoring-overview-of-diagnostic-logs.md) toocollect detailed high-frequency metrics on your service.</span></span>
* <span data-ttu-id="7385c-163">Pobierz [omówienie zbierania metryk](insights-how-to-customize-monitoring.md) toomake się, że usługa jest dostępna i elastyczny.</span><span class="sxs-lookup"><span data-stu-id="7385c-163">Get an [overview of metrics collection](insights-how-to-customize-monitoring.md) toomake sure your service is available and responsive.</span></span>
