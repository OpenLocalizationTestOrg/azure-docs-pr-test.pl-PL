---
title: "alerty aaaCreate dla usług Azure - Azure portal | Dokumentacja firmy Microsoft"
description: "Gdy są spełnione warunki hello wyzwolenia wiadomości e-mail, powiadomienia, adresy URL witryny sieci Web wywołania (elementy webhook) lub automatyzacji."
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
ms.openlocfilehash: 78d862d25255cda9fdfe347329e908a471c39846
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-metric-alerts-in-azure-monitor-for-azure-services---azure-portal"></a><span data-ttu-id="08e0f-103">W monitorze Azure tworzyć alerty metryki dla usługi Azure - Azure portal</span><span class="sxs-lookup"><span data-stu-id="08e0f-103">Create metric alerts in Azure Monitor for Azure services - Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="08e0f-104">Portal</span><span class="sxs-lookup"><span data-stu-id="08e0f-104">Portal</span></span>](insights-alerts-portal.md)
> * [<span data-ttu-id="08e0f-105">Program PowerShell</span><span class="sxs-lookup"><span data-stu-id="08e0f-105">PowerShell</span></span>](insights-alerts-powershell.md)
> * [<span data-ttu-id="08e0f-106">Interfejs wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="08e0f-106">CLI</span></span>](insights-alerts-command-line-interface.md)
>
>

## <a name="overview"></a><span data-ttu-id="08e0f-107">Omówienie</span><span class="sxs-lookup"><span data-stu-id="08e0f-107">Overview</span></span>
<span data-ttu-id="08e0f-108">W tym artykule opisano, jak tooset Azure metryki alerty za pomocą hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="08e0f-108">This article shows you how tooset up Azure metric alerts using hello Azure portal.</span></span>   

<span data-ttu-id="08e0f-109">Możesz otrzymywać alertu na podstawie metryki monitorowania lub zdarzenia na usługami Azure.</span><span class="sxs-lookup"><span data-stu-id="08e0f-109">You can receive an alert based on monitoring metrics for, or events on, your Azure services.</span></span>

* <span data-ttu-id="08e0f-110">**Wartości metryki** — Witaj alertu wyzwalacze, jeśli wartość hello określonej metryki przecina próg przypisać w żadnym kierunku.</span><span class="sxs-lookup"><span data-stu-id="08e0f-110">**Metric values** - hello alert triggers when hello value of a specified metric crosses a threshold you assign in either direction.</span></span> <span data-ttu-id="08e0f-111">Oznacza to, że oba wyzwala kiedy najpierw zostanie spełniony warunek hello i następnie później podczas warunku jest już spełniane.</span><span class="sxs-lookup"><span data-stu-id="08e0f-111">That is, it triggers both when hello condition is first met and then afterwards when that condition is no longer being met.</span></span>    
* <span data-ttu-id="08e0f-112">**Zdarzenia dziennika aktywności** — alert może wyzwolić na *co* zdarzenia lub tylko wtedy, gdy występuje określone zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="08e0f-112">**Activity log events** - An alert can trigger on *every* event, or, only when a certain events occurs.</span></span> <span data-ttu-id="08e0f-113">więcej informacji na temat alertów dotyczących działań w dzienniku toolearn [kliknij tutaj](monitoring-activity-log-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="08e0f-113">toolearn more about activity log alerts [click here](monitoring-activity-log-alerts.md)</span></span>

<span data-ttu-id="08e0f-114">Można skonfigurować hello metryki toodo alertów po, wyzwala:</span><span class="sxs-lookup"><span data-stu-id="08e0f-114">You can configure a metric alert toodo hello following when it triggers:</span></span>

* <span data-ttu-id="08e0f-115">Wyślij administratora usługi toohello powiadomienia e-mail i współadministratorzy</span><span class="sxs-lookup"><span data-stu-id="08e0f-115">send email notifications toohello service administrator and co-administrators</span></span>
* <span data-ttu-id="08e0f-116">Wyślij wiadomość e-mail tooadditional wiadomości e-mail, które określisz.</span><span class="sxs-lookup"><span data-stu-id="08e0f-116">send email tooadditional emails that you specify.</span></span>
* <span data-ttu-id="08e0f-117">Wywołanie elementu webhook</span><span class="sxs-lookup"><span data-stu-id="08e0f-117">call a webhook</span></span>
* <span data-ttu-id="08e0f-118">Uruchamia wykonywanie elementów runbook platformy Azure (tylko z hello portalu Azure)</span><span class="sxs-lookup"><span data-stu-id="08e0f-118">start execution of an Azure runbook (only from hello Azure portal)</span></span>

<span data-ttu-id="08e0f-119">Można skonfigurować i uzyskać informacje na temat metryki reguły alertów za pomocą</span><span class="sxs-lookup"><span data-stu-id="08e0f-119">You can configure and get information about metric alert rules using</span></span>

* [<span data-ttu-id="08e0f-120">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="08e0f-120">Azure portal</span></span>](insights-alerts-portal.md)
* [<span data-ttu-id="08e0f-121">PowerShell</span><span class="sxs-lookup"><span data-stu-id="08e0f-121">PowerShell</span></span>](insights-alerts-powershell.md)
* [<span data-ttu-id="08e0f-122">Interfejs wiersza polecenia (CLI)</span><span class="sxs-lookup"><span data-stu-id="08e0f-122">command-line interface (CLI)</span></span>](insights-alerts-command-line-interface.md)
* [<span data-ttu-id="08e0f-123">Interfejs API REST Azure monitora</span><span class="sxs-lookup"><span data-stu-id="08e0f-123">Azure Monitor REST API</span></span>](https://msdn.microsoft.com/library/azure/dn931945.aspx)

## <a name="create-an-alert-rule-on-a-metric-with-hello-azure-portal"></a><span data-ttu-id="08e0f-124">Tworzenie reguły alertu na Metryka z hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="08e0f-124">Create an alert rule on a metric with hello Azure portal</span></span>
1. <span data-ttu-id="08e0f-125">W hello [portal](https://portal.azure.com/)planuje się monitorowanie zasobów hello Znajdź i zaznacz go.</span><span class="sxs-lookup"><span data-stu-id="08e0f-125">In hello [portal](https://portal.azure.com/), locate hello resource you are interested in monitoring and select it.</span></span>

2. <span data-ttu-id="08e0f-126">Wybierz **alerty** lub **reguły alertów** w sekcji monitorowanie hello.</span><span class="sxs-lookup"><span data-stu-id="08e0f-126">Select **Alerts** or **Alert rules** under hello MONITORING section.</span></span> <span data-ttu-id="08e0f-127">Ikona i tekst Hello mogą się nieco różnić dla różnych zasobów.</span><span class="sxs-lookup"><span data-stu-id="08e0f-127">hello text and icon may vary slightly for different resources.</span></span>  

    ![Monitorowanie](./media/insights-alerts-portal/AlertRulesButton.png)

3. <span data-ttu-id="08e0f-129">Wybierz hello **Dodaj alert** poleceń i wypełnij pola hello.</span><span class="sxs-lookup"><span data-stu-id="08e0f-129">Select hello **Add alert** command and fill in hello fields.</span></span>

    ![Dodawanie alertu](./media/insights-alerts-portal/AddAlertOnlyParamsPage.png)

4. <span data-ttu-id="08e0f-131">**Nazwa** alertu reguły, a następnie wybierz pozycję **opis**, który pokazuje również w wiadomości e-mail z powiadomieniem.</span><span class="sxs-lookup"><span data-stu-id="08e0f-131">**Name** your alert rule, and choose a **Description**, which also shows in notification emails.</span></span>

5. <span data-ttu-id="08e0f-132">Wybierz hello **Metryka** toomonitor, a następnie wybierz **warunku** i **próg** wartość metryki hello.</span><span class="sxs-lookup"><span data-stu-id="08e0f-132">Select hello **Metric** you want toomonitor, then choose a **Condition** and **Threshold** value for hello metric.</span></span> <span data-ttu-id="08e0f-133">Również wybrana hello **okres** hello metryki czasu reguły muszą zostać spełnione przed hello wyzwalaczy alertu.</span><span class="sxs-lookup"><span data-stu-id="08e0f-133">Also chose hello **Period** of time that hello metric rule must be satisfied before hello alert triggers.</span></span> <span data-ttu-id="08e0f-134">Tak na przykład jeśli używasz okres hello "PT5M" i alertu szuka procesora CPU przekracza 80%, hello alert jest wyzwalane po hello procesora CPU było stale powyżej 80% 5 minut.</span><span class="sxs-lookup"><span data-stu-id="08e0f-134">So for example, if you use hello period "PT5M" and your alert looks for CPU above 80%, hello alert triggers when hello CPU has been consistently above 80% for 5 minutes.</span></span> <span data-ttu-id="08e0f-135">W momencie hello pierwszy wyzwalacz, ponownie uruchamia to, gdy hello Procesora pozostaje poniżej 80% 5 minut.</span><span class="sxs-lookup"><span data-stu-id="08e0f-135">Once hello first trigger occurs, it again triggers when hello CPU stays below 80% for 5 minutes.</span></span> <span data-ttu-id="08e0f-136">Hello pomiaru Procesora występuje co minutę.</span><span class="sxs-lookup"><span data-stu-id="08e0f-136">hello CPU measurement occurs every 1 minute.</span></span>   

6. <span data-ttu-id="08e0f-137">Sprawdź **E-mail właścicieli...**  Jeśli chcesz, aby administratorzy i współadministratorzy toobe pocztą e-mail po hello uruchamiany alertu.</span><span class="sxs-lookup"><span data-stu-id="08e0f-137">Check **Email owners...** if you want administrators and co-administrators toobe emailed when hello alert fires.</span></span>

7. <span data-ttu-id="08e0f-138">Jeśli chcesz, dodatkowe wiadomości e-mail tooreceive powiadomienie, gdy hello alertu, należy dodać je w hello **email(s) dodatkowe administratora** pola.</span><span class="sxs-lookup"><span data-stu-id="08e0f-138">If you want additional emails tooreceive a notification when hello alert fires, add them in hello **Additional Administrator email(s)** field.</span></span> <span data-ttu-id="08e0f-139">Wiele wiadomości e-mail należy rozdzielić średnikami -  *email@contoso.com;email2@contoso.com*</span><span class="sxs-lookup"><span data-stu-id="08e0f-139">Separate multiple emails with semi-colons - *email@contoso.com;email2@contoso.com*</span></span>

8. <span data-ttu-id="08e0f-140">Umieść w prawidłowym identyfikatorem URI w hello **Webhook** pole Jeśli ma ona wywoływana po hello uruchamiany alertu.</span><span class="sxs-lookup"><span data-stu-id="08e0f-140">Put in a valid URI in hello **Webhook** field if you want it called when hello alert fires.</span></span>

9. <span data-ttu-id="08e0f-141">Jeśli używasz usługi Automatyzacja Azure, możesz wybrać toobe elementu Runbook, uruchom po zgłoszeniu alertu hello.</span><span class="sxs-lookup"><span data-stu-id="08e0f-141">If you use Azure Automation, you can select a Runbook toobe run when hello alert fires.</span></span>

10. <span data-ttu-id="08e0f-142">Wybierz **OK** po done toocreate hello alertu.</span><span class="sxs-lookup"><span data-stu-id="08e0f-142">Select **OK** when done toocreate hello alert.</span></span>   

<span data-ttu-id="08e0f-143">W ciągu kilku minut hello alert jest aktywny i wyzwala w sposób opisany wcześniej.</span><span class="sxs-lookup"><span data-stu-id="08e0f-143">Within a few minutes, hello alert is active and triggers as previously described.</span></span>

## <a name="managing-your-alerts"></a><span data-ttu-id="08e0f-144">Zarządzanie alertami</span><span class="sxs-lookup"><span data-stu-id="08e0f-144">Managing your alerts</span></span>
<span data-ttu-id="08e0f-145">Po utworzeniu alertu, zostanie ona wybrana oraz:</span><span class="sxs-lookup"><span data-stu-id="08e0f-145">Once you have created an alert, you can select it and:</span></span>

* <span data-ttu-id="08e0f-146">Wyświetl wykres przedstawiający hello próg metryki i hello rzeczywistymi wartościami z hello poprzedniego dnia.</span><span class="sxs-lookup"><span data-stu-id="08e0f-146">View a graph showing hello metric threshold and hello actual values from hello previous day.</span></span>
* <span data-ttu-id="08e0f-147">Edytuj lub usuń go.</span><span class="sxs-lookup"><span data-stu-id="08e0f-147">Edit or delete it.</span></span>
* <span data-ttu-id="08e0f-148">**Wyłącz** lub **włączyć** go, jeśli chcesz zatrzymać tootemporarily lub wznowić odbieranie powiadomień dla tego alertu.</span><span class="sxs-lookup"><span data-stu-id="08e0f-148">**Disable** or **Enable** it if you want tootemporarily stop or resume receiving notifications for that alert.</span></span>

## <a name="next-steps"></a><span data-ttu-id="08e0f-149">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="08e0f-149">Next steps</span></span>
* <span data-ttu-id="08e0f-150">[Omówienie monitorowania Azure](monitoring-overview.md) tym hello typy informacji, można zbierać i monitorowania.</span><span class="sxs-lookup"><span data-stu-id="08e0f-150">[Get an overview of Azure monitoring](monitoring-overview.md) including hello types of information you can collect and monitor.</span></span>
* <span data-ttu-id="08e0f-151">Dowiedz się więcej o [konfigurowaniu elementów webhook w alertach](insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="08e0f-151">Learn more about [configuring webhooks in alerts](insights-webhooks-alerts.md).</span></span>
* <span data-ttu-id="08e0f-152">Dowiedz się więcej o [konfigurowania alertów na zdarzenia dziennika aktywności](monitoring-activity-log-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="08e0f-152">Learn more about [configuring alerts on Activity log events](monitoring-activity-log-alerts.md).</span></span>
* <span data-ttu-id="08e0f-153">Dowiedz się więcej o [elementów Runbook automatyzacji Azure](../automation/automation-starting-a-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="08e0f-153">Learn more about [Azure Automation Runbooks](../automation/automation-starting-a-runbook.md).</span></span>
* <span data-ttu-id="08e0f-154">Pobierz [Przegląd dzienników diagnostycznych](monitoring-overview-of-diagnostic-logs.md) i zbieranie szczegółowych metryki wysokiej częstotliwości w usłudze.</span><span class="sxs-lookup"><span data-stu-id="08e0f-154">Get an [overview of diagnostic logs](monitoring-overview-of-diagnostic-logs.md) and collect detailed high-frequency metrics on your service.</span></span>
* <span data-ttu-id="08e0f-155">Pobierz [omówienie zbierania metryk](insights-how-to-customize-monitoring.md) toomake się, że usługa jest dostępna i elastyczny.</span><span class="sxs-lookup"><span data-stu-id="08e0f-155">Get an [overview of metrics collection](insights-how-to-customize-monitoring.md) toomake sure your service is available and responsive.</span></span>
