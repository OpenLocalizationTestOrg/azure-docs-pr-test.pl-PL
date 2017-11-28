---
title: "Utwórz alerty dla usług Azure - Azure portal | Dokumentacja firmy Microsoft"
description: "Wyzwalacz wiadomości e-mail, powiadomienia, Wywołaj adresy URL witryny sieci Web (elementy webhook) lub automatyzacji po spełnieniu warunków, które określisz."
author: rboucher
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: f7457655-ced6-4102-a9dd-7ddf2265c0e2
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/23/2016
ms.author: robb
ms.openlocfilehash: 745a9c016bd037f1051025a2c5a468c3935e4550
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-metric-alerts-in-azure-monitor-for-azure-services---azure-portal"></a><span data-ttu-id="b8a2f-103">W monitorze Azure tworzyć alerty metryki dla usługi Azure - Azure portal</span><span class="sxs-lookup"><span data-stu-id="b8a2f-103">Create metric alerts in Azure Monitor for Azure services - Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b8a2f-104">Portal</span><span class="sxs-lookup"><span data-stu-id="b8a2f-104">Portal</span></span>](insights-alerts-portal.md)
> * [<span data-ttu-id="b8a2f-105">Program PowerShell</span><span class="sxs-lookup"><span data-stu-id="b8a2f-105">PowerShell</span></span>](insights-alerts-powershell.md)
> * [<span data-ttu-id="b8a2f-106">Interfejs wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="b8a2f-106">CLI</span></span>](insights-alerts-command-line-interface.md)
>
>

## <a name="overview"></a><span data-ttu-id="b8a2f-107">Omówienie</span><span class="sxs-lookup"><span data-stu-id="b8a2f-107">Overview</span></span>
<span data-ttu-id="b8a2f-108">W tym artykule przedstawiono sposób konfigurowania Azure metryki alertów za pomocą portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="b8a2f-108">This article shows you how to set up Azure metric alerts using the Azure portal.</span></span>   

<span data-ttu-id="b8a2f-109">Możesz otrzymywać alertu na podstawie metryki monitorowania lub zdarzenia na usługami Azure.</span><span class="sxs-lookup"><span data-stu-id="b8a2f-109">You can receive an alert based on monitoring metrics for, or events on, your Azure services.</span></span>

* <span data-ttu-id="b8a2f-110">**Wartości metryki** — uruchamia alert, gdy wartość określonej metryki przekracza próg przypisać w żadnym kierunku.</span><span class="sxs-lookup"><span data-stu-id="b8a2f-110">**Metric values** - The alert triggers when the value of a specified metric crosses a threshold you assign in either direction.</span></span> <span data-ttu-id="b8a2f-111">Oznacza to, że oba wyzwala po spełnieniu warunku zostanie najpierw i następnie później podczas warunku jest już spełniane.</span><span class="sxs-lookup"><span data-stu-id="b8a2f-111">That is, it triggers both when the condition is first met and then afterwards when that condition is no longer being met.</span></span>    
* <span data-ttu-id="b8a2f-112">**Zdarzenia dziennika aktywności** — alert może wyzwolić na *co* zdarzenia lub tylko wtedy, gdy występuje określone zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="b8a2f-112">**Activity log events** - An alert can trigger on *every* event, or, only when a certain events occurs.</span></span> <span data-ttu-id="b8a2f-113">Aby dowiedzieć się więcej o alertach dziennika aktywności [kliknij tutaj](monitoring-activity-log-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="b8a2f-113">To learn more about activity log alerts [click here](monitoring-activity-log-alerts.md)</span></span>

<span data-ttu-id="b8a2f-114">Można skonfigurować metryki alert do wyzwala, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="b8a2f-114">You can configure a metric alert to do the following when it triggers:</span></span>

* <span data-ttu-id="b8a2f-115">wysyłanie powiadomień e-mail do administratora usługi i współadministratorzy</span><span class="sxs-lookup"><span data-stu-id="b8a2f-115">send email notifications to the service administrator and co-administrators</span></span>
* <span data-ttu-id="b8a2f-116">Wyślij wiadomość e-mail do dodatkowych wiadomości e-mail przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="b8a2f-116">send email to additional emails that you specify.</span></span>
* <span data-ttu-id="b8a2f-117">Wywołanie elementu webhook</span><span class="sxs-lookup"><span data-stu-id="b8a2f-117">call a webhook</span></span>
* <span data-ttu-id="b8a2f-118">Uruchamia wykonywanie elementów runbook platformy Azure (tylko z portalu Azure)</span><span class="sxs-lookup"><span data-stu-id="b8a2f-118">start execution of an Azure runbook (only from the Azure portal)</span></span>

<span data-ttu-id="b8a2f-119">Można skonfigurować i uzyskać informacje na temat metryki reguły alertów za pomocą</span><span class="sxs-lookup"><span data-stu-id="b8a2f-119">You can configure and get information about metric alert rules using</span></span>

* [<span data-ttu-id="b8a2f-120">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="b8a2f-120">Azure portal</span></span>](insights-alerts-portal.md)
* [<span data-ttu-id="b8a2f-121">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b8a2f-121">PowerShell</span></span>](insights-alerts-powershell.md)
* [<span data-ttu-id="b8a2f-122">Interfejs wiersza polecenia (CLI)</span><span class="sxs-lookup"><span data-stu-id="b8a2f-122">command-line interface (CLI)</span></span>](insights-alerts-command-line-interface.md)
* [<span data-ttu-id="b8a2f-123">Interfejs API REST Azure monitora</span><span class="sxs-lookup"><span data-stu-id="b8a2f-123">Azure Monitor REST API</span></span>](https://msdn.microsoft.com/library/azure/dn931945.aspx)

## <a name="create-an-alert-rule-on-a-metric-with-the-azure-portal"></a><span data-ttu-id="b8a2f-124">Tworzenie reguły alertu na Metryka z portalu Azure</span><span class="sxs-lookup"><span data-stu-id="b8a2f-124">Create an alert rule on a metric with the Azure portal</span></span>
1. <span data-ttu-id="b8a2f-125">W [portal](https://portal.azure.com/)zasobów planuje się monitorowanie Znajdź i zaznacz go.</span><span class="sxs-lookup"><span data-stu-id="b8a2f-125">In the [portal](https://portal.azure.com/), locate the resource you are interested in monitoring and select it.</span></span>

2. <span data-ttu-id="b8a2f-126">Wybierz **alerty** lub **reguły alertów** w sekcji monitorowanie.</span><span class="sxs-lookup"><span data-stu-id="b8a2f-126">Select **Alerts** or **Alert rules** under the MONITORING section.</span></span> <span data-ttu-id="b8a2f-127">Tekst i ikona mogą się nieco różnić dla różnych zasobów.</span><span class="sxs-lookup"><span data-stu-id="b8a2f-127">The text and icon may vary slightly for different resources.</span></span>  

    ![Monitorowanie](./media/insights-alerts-portal/AlertRulesButton.png)

3. <span data-ttu-id="b8a2f-129">Wybierz **Dodaj alert** poleceń i wypełnij pola.</span><span class="sxs-lookup"><span data-stu-id="b8a2f-129">Select the **Add alert** command and fill in the fields.</span></span>

    ![Dodawanie alertu](./media/insights-alerts-portal/AddAlertOnlyParamsPage.png)

4. <span data-ttu-id="b8a2f-131">**Nazwa** alertu reguły, a następnie wybierz pozycję **opis**, który pokazuje również w wiadomości e-mail z powiadomieniem.</span><span class="sxs-lookup"><span data-stu-id="b8a2f-131">**Name** your alert rule, and choose a **Description**, which also shows in notification emails.</span></span>

5. <span data-ttu-id="b8a2f-132">Wybierz **Metryka** chcesz monitorować, a następnie wybierz pozycję **warunku** i **próg** wartość metryki.</span><span class="sxs-lookup"><span data-stu-id="b8a2f-132">Select the **Metric** you want to monitor, then choose a **Condition** and **Threshold** value for the metric.</span></span> <span data-ttu-id="b8a2f-133">Również wybrana **okres** czas, przez który metryki reguły muszą zostać spełnione przed wyzwalaczy alertu.</span><span class="sxs-lookup"><span data-stu-id="b8a2f-133">Also chose the **Period** of time that the metric rule must be satisfied before the alert triggers.</span></span> <span data-ttu-id="b8a2f-134">Tak na przykład jeśli używasz okres "PT5M" i alertu szuka procesora CPU przekracza 80%, alert jest wyzwalane po procesora CPU było stale powyżej 80% 5 minut.</span><span class="sxs-lookup"><span data-stu-id="b8a2f-134">So for example, if you use the period "PT5M" and your alert looks for CPU above 80%, the alert triggers when the CPU has been consistently above 80% for 5 minutes.</span></span> <span data-ttu-id="b8a2f-135">W momencie to pierwszy wyzwalacz, ponownie uruchamia to, gdy Procesora pozostaje poniżej 80% 5 minut.</span><span class="sxs-lookup"><span data-stu-id="b8a2f-135">Once the first trigger occurs, it again triggers when the CPU stays below 80% for 5 minutes.</span></span> <span data-ttu-id="b8a2f-136">Pomiar Procesora występuje co minutę.</span><span class="sxs-lookup"><span data-stu-id="b8a2f-136">The CPU measurement occurs every 1 minute.</span></span>   

6. <span data-ttu-id="b8a2f-137">Sprawdź **E-mail właścicieli...**  Jeśli chcesz, aby administratorzy i współadministratorzy w celu przesłania pocztą e-mail po zgłoszeniu alertu.</span><span class="sxs-lookup"><span data-stu-id="b8a2f-137">Check **Email owners...** if you want administrators and co-administrators to be emailed when the alert fires.</span></span>

7. <span data-ttu-id="b8a2f-138">Jeśli chcesz, dodatkowe wiadomości e-mail, aby otrzymać powiadomienie po zgłoszeniu alertu, dodaj je w **email(s) dodatkowe administratora** pola.</span><span class="sxs-lookup"><span data-stu-id="b8a2f-138">If you want additional emails to receive a notification when the alert fires, add them in the **Additional Administrator email(s)** field.</span></span> <span data-ttu-id="b8a2f-139">Wiele wiadomości e-mail należy rozdzielić średnikami -  *email@contoso.com;email2@contoso.com*</span><span class="sxs-lookup"><span data-stu-id="b8a2f-139">Separate multiple emails with semi-colons - *email@contoso.com;email2@contoso.com*</span></span>

8. <span data-ttu-id="b8a2f-140">Umieść w prawidłowym identyfikatorem URI w **Webhook** jeśli ma ona wywoływana po zgłoszeniu alertu.</span><span class="sxs-lookup"><span data-stu-id="b8a2f-140">Put in a valid URI in the **Webhook** field if you want it called when the alert fires.</span></span>

9. <span data-ttu-id="b8a2f-141">Jeśli używasz usługi Automatyzacja Azure, możesz wybrać element Runbook do uruchomienia po zgłoszeniu alertu.</span><span class="sxs-lookup"><span data-stu-id="b8a2f-141">If you use Azure Automation, you can select a Runbook to be run when the alert fires.</span></span>

10. <span data-ttu-id="b8a2f-142">Wybierz **OK** po zakończeniu można utworzyć alertu.</span><span class="sxs-lookup"><span data-stu-id="b8a2f-142">Select **OK** when done to create the alert.</span></span>   

<span data-ttu-id="b8a2f-143">W ciągu kilku minut alert jest aktywny i wyzwala w sposób opisany wcześniej.</span><span class="sxs-lookup"><span data-stu-id="b8a2f-143">Within a few minutes, the alert is active and triggers as previously described.</span></span>

## <a name="managing-your-alerts"></a><span data-ttu-id="b8a2f-144">Zarządzanie alertami</span><span class="sxs-lookup"><span data-stu-id="b8a2f-144">Managing your alerts</span></span>
<span data-ttu-id="b8a2f-145">Po utworzeniu alertu, zostanie ona wybrana oraz:</span><span class="sxs-lookup"><span data-stu-id="b8a2f-145">Once you have created an alert, you can select it and:</span></span>

* <span data-ttu-id="b8a2f-146">Wyświetl wykres przedstawiający próg metryki i rzeczywistymi wartościami z poprzedniego dnia.</span><span class="sxs-lookup"><span data-stu-id="b8a2f-146">View a graph showing the metric threshold and the actual values from the previous day.</span></span>
* <span data-ttu-id="b8a2f-147">Edytuj lub usuń go.</span><span class="sxs-lookup"><span data-stu-id="b8a2f-147">Edit or delete it.</span></span>
* <span data-ttu-id="b8a2f-148">**Wyłącz** lub **włączyć** go, jeśli chcesz tymczasowo zatrzymać lub wznowić odbieranie powiadomień dla tego alertu.</span><span class="sxs-lookup"><span data-stu-id="b8a2f-148">**Disable** or **Enable** it if you want to temporarily stop or resume receiving notifications for that alert.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b8a2f-149">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b8a2f-149">Next steps</span></span>
* <span data-ttu-id="b8a2f-150">[Omówienie monitorowania Azure](monitoring-overview.md) w tym typy informacji, można zbierać i monitorowania.</span><span class="sxs-lookup"><span data-stu-id="b8a2f-150">[Get an overview of Azure monitoring](monitoring-overview.md) including the types of information you can collect and monitor.</span></span>
* <span data-ttu-id="b8a2f-151">Dowiedz się więcej o [konfigurowaniu elementów webhook w alertach](insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="b8a2f-151">Learn more about [configuring webhooks in alerts](insights-webhooks-alerts.md).</span></span>
* <span data-ttu-id="b8a2f-152">Dowiedz się więcej o [konfigurowania alertów na zdarzenia dziennika aktywności](monitoring-activity-log-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="b8a2f-152">Learn more about [configuring alerts on Activity log events](monitoring-activity-log-alerts.md).</span></span>
* <span data-ttu-id="b8a2f-153">Dowiedz się więcej o [elementów Runbook automatyzacji Azure](../automation/automation-starting-a-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="b8a2f-153">Learn more about [Azure Automation Runbooks](../automation/automation-starting-a-runbook.md).</span></span>
* <span data-ttu-id="b8a2f-154">Pobierz [Przegląd dzienników diagnostycznych](monitoring-overview-of-diagnostic-logs.md) i zbieranie szczegółowych metryki wysokiej częstotliwości w usłudze.</span><span class="sxs-lookup"><span data-stu-id="b8a2f-154">Get an [overview of diagnostic logs](monitoring-overview-of-diagnostic-logs.md) and collect detailed high-frequency metrics on your service.</span></span>
* <span data-ttu-id="b8a2f-155">Pobierz [omówienie zbierania metryk](insights-how-to-customize-monitoring.md) się upewnić, że usługa jest dostępna i elastyczny.</span><span class="sxs-lookup"><span data-stu-id="b8a2f-155">Get an [overview of metrics collection](insights-how-to-customize-monitoring.md) to make sure your service is available and responsive.</span></span>
