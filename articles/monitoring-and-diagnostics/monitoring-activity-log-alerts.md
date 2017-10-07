---
title: "alerty dziennika aktywności aaaCreate | Dokumentacja firmy Microsoft"
description: "Otrzymasz powiadomienie w wiadomości SMS, webhook i wiadomości e-mail po wystąpieniu określonego zdarzenia w dzienniku aktywności hello."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/03/2017
ms.author: johnkem
ms.openlocfilehash: ba0716cc12a0b3a0024ee5562a025f3f153f8982
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-activity-log-alerts"></a><span data-ttu-id="34b76-103">Utwórz działanie alertów dziennika</span><span class="sxs-lookup"><span data-stu-id="34b76-103">Create activity log alerts</span></span>

## <a name="overview"></a><span data-ttu-id="34b76-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="34b76-104">Overview</span></span>
<span data-ttu-id="34b76-105">Alerty dziennika aktywności są alerty, które aktywować po wystąpieniu nowego zdarzenia dziennika działania, który spełnia warunki hello określone w hello alertu.</span><span class="sxs-lookup"><span data-stu-id="34b76-105">Activity log alerts are alerts that activate when a new activity log event occurs that matches hello conditions specified in hello alert.</span></span> <span data-ttu-id="34b76-106">Są one zasobów platformy Azure, dlatego mogą być tworzone za pomocą szablonu usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="34b76-106">They are Azure resources, so they can be created by using an Azure Resource Manager template.</span></span> <span data-ttu-id="34b76-107">One również może być utworzona, zaktualizowany lub usunięty hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="34b76-107">They also can be created, updated, or deleted in hello Azure portal.</span></span> <span data-ttu-id="34b76-108">W tym artykule przedstawiono hello pojęć dotyczących alertów dotyczących działań w dzienniku.</span><span class="sxs-lookup"><span data-stu-id="34b76-108">This article introduces hello concepts behind activity log alerts.</span></span> <span data-ttu-id="34b76-109">Następnie pokaże Ci, jak toouse hello Azure portalu tooset się alert na zdarzenia dziennika aktywności.</span><span class="sxs-lookup"><span data-stu-id="34b76-109">It then shows you how toouse hello Azure portal tooset up an alert on activity log events.</span></span>

<span data-ttu-id="34b76-110">Zazwyczaj w celu utworzenia alertów dotyczących działań w dzienniku tooreceive powiadomienia po:</span><span class="sxs-lookup"><span data-stu-id="34b76-110">Typically, you create activity log alerts tooreceive notifications when:</span></span>

* <span data-ttu-id="34b76-111">Określone zmiany zostaną wprowadzone do zasobów w Twojej subskrypcji platformy Azure, często zakresie tooparticular grupy zasobów lub zasobów.</span><span class="sxs-lookup"><span data-stu-id="34b76-111">Specific changes occur on resources in your Azure subscription, often scoped tooparticular resource groups or resources.</span></span> <span data-ttu-id="34b76-112">Na przykład można toobe powiadomienia w przypadku maszyn wirtualnych w myProductionResourceGroup zostanie usunięty.</span><span class="sxs-lookup"><span data-stu-id="34b76-112">For example, you might want toobe notified when any virtual machine in myProductionResourceGroup is deleted.</span></span> <span data-ttu-id="34b76-113">Lub może być toobe powiadamiani, jeśli wszystkie nowe role są przypisywane tooa użytkownika w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="34b76-113">Or, you might want toobe notified if any new roles are assigned tooa user in your subscription.</span></span>
* <span data-ttu-id="34b76-114">Usługa kondycji zdarzenie.</span><span class="sxs-lookup"><span data-stu-id="34b76-114">A service health event occurs.</span></span> <span data-ttu-id="34b76-115">Usługa kondycji zdarzenia zawierają zgłaszania zdarzeń i obsługi zdarzeń tooresources w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="34b76-115">Service health events include notification of incidents and maintenance events that apply tooresources in your subscription.</span></span>

<span data-ttu-id="34b76-116">W obu przypadkach alert dziennika aktywności monitoruje tylko w przypadku zdarzeń w subskrypcji hello, w których hello tworzony jest alert.</span><span class="sxs-lookup"><span data-stu-id="34b76-116">In either case, an activity log alert monitors only for events in hello subscription in which hello alert is created.</span></span>

<span data-ttu-id="34b76-117">Możesz skonfigurować alert dziennika działania na podstawie żadnych najwyższego poziomu właściwości w obiekcie JSON hello zdarzenia dziennika aktywności.</span><span class="sxs-lookup"><span data-stu-id="34b76-117">You can configure an activity log alert based on any top-level property in hello JSON object for an activity log event.</span></span> <span data-ttu-id="34b76-118">Jednak portalu hello przedstawia najbardziej typowe opcje hello:</span><span class="sxs-lookup"><span data-stu-id="34b76-118">However, hello portal shows hello most common options:</span></span>

- <span data-ttu-id="34b76-119">**Kategoria**: administracyjne, usługa kondycji, skalowania automatycznego i zalecenia.</span><span class="sxs-lookup"><span data-stu-id="34b76-119">**Category**: Administrative, Service Health, Autoscale, and Recommendation.</span></span> <span data-ttu-id="34b76-120">Aby uzyskać więcej informacji, zobacz [omówienie dziennik aktywności platformy Azure hello](./monitoring-overview-activity-logs.md#categories-in-the-activity-log).</span><span class="sxs-lookup"><span data-stu-id="34b76-120">For more information, see [Overview of hello Azure activity log](./monitoring-overview-activity-logs.md#categories-in-the-activity-log).</span></span> <span data-ttu-id="34b76-121">toolearn więcej informacji na temat zdarzenia kondycji usługi, zobacz [odbierzesz alerty dziennika działania dotyczące powiadomień dotyczących usługi](./monitoring-activity-log-alerts-on-service-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="34b76-121">toolearn more about service health events, see [Receive activity log alerts on service notifications](./monitoring-activity-log-alerts-on-service-notifications.md).</span></span>
- <span data-ttu-id="34b76-122">**Grupa zasobów**</span><span class="sxs-lookup"><span data-stu-id="34b76-122">**Resource group**</span></span>
- <span data-ttu-id="34b76-123">**Zasób**</span><span class="sxs-lookup"><span data-stu-id="34b76-123">**Resource**</span></span>
- <span data-ttu-id="34b76-124">**Typ zasobu**</span><span class="sxs-lookup"><span data-stu-id="34b76-124">**Resource type**</span></span>
- <span data-ttu-id="34b76-125">**Nazwa operacji**: Nazwa operacji hello kontroli dostępu opartej na roli Menedżera zasobów.</span><span class="sxs-lookup"><span data-stu-id="34b76-125">**Operation name**: hello Resource Manager Role-Based Access Control operation name.</span></span>
- <span data-ttu-id="34b76-126">**Poziom**: hello poziom ważności zdarzenia hello (pełne, informacyjny, ostrzeżenie, błąd lub krytyczny).</span><span class="sxs-lookup"><span data-stu-id="34b76-126">**Level**: hello severity level of hello event (Verbose, Informational, Warning, Error, or Critical).</span></span>
- <span data-ttu-id="34b76-127">**Stan**: hello stan hello zdarzeń, zwykle uruchomiona, nie powiodło się lub zakończyło się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="34b76-127">**Status**: hello status of hello event, typically Started, Failed, or Succeeded.</span></span>
- <span data-ttu-id="34b76-128">**Zdarzenie inicjowane przez**: hello znanej także jako "wywołującego."</span><span class="sxs-lookup"><span data-stu-id="34b76-128">**Event initiated by**: Also known as hello "caller."</span></span> <span data-ttu-id="34b76-129">adres e-mail Hello lub identyfikator hello użytkownika, który wykonał operację hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="34b76-129">hello email address or Azure Active Directory identifier of hello user who performed hello operation.</span></span>

>[!NOTE]
><span data-ttu-id="34b76-130">Należy określić co najmniej dwóch hello poprzedzające kryteria alertu o jeden jest hello kategorii.</span><span class="sxs-lookup"><span data-stu-id="34b76-130">You must specify at least two of hello preceding criteria in your alert, with one being hello category.</span></span> <span data-ttu-id="34b76-131">Nie można utworzyć alertu, który uaktywnia każdorazowego zdarzenie jest tworzone w dziennikach działania hello.</span><span class="sxs-lookup"><span data-stu-id="34b76-131">You may not create an alert that activates every time an event is created in hello activity logs.</span></span>
>
>

<span data-ttu-id="34b76-132">Po aktywowaniu alert dziennika aktywności używa akcji grupy toogenerate akcje lub powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="34b76-132">When an activity log alert is activated, it uses an action group toogenerate actions or notifications.</span></span> <span data-ttu-id="34b76-133">Grupy akcji jest zestawem wielokrotnego użytku odbiorców powiadomień, takie jak adresy e-mail, numerów telefonów adresy URL elementu webhook lub wiadomości SMS.</span><span class="sxs-lookup"><span data-stu-id="34b76-133">An action group is a reusable set of notification receivers, such as email addresses, webhook URLs, or SMS phone numbers.</span></span> <span data-ttu-id="34b76-134">odbiorniki Hello mogą być przywoływane z wielu toocentralize alertów i grupy kanałów powiadomień.</span><span class="sxs-lookup"><span data-stu-id="34b76-134">hello receivers can be referenced from multiple alerts toocentralize and group your notification channels.</span></span> <span data-ttu-id="34b76-135">Podczas definiowania alertu dziennika aktywności, dostępne są dwie opcje.</span><span class="sxs-lookup"><span data-stu-id="34b76-135">When you define your activity log alert, you have two options.</span></span> <span data-ttu-id="34b76-136">Możesz:</span><span class="sxs-lookup"><span data-stu-id="34b76-136">You can:</span></span>

* <span data-ttu-id="34b76-137">Użyj istniejącej grupy działań w alertu dziennika aktywności.</span><span class="sxs-lookup"><span data-stu-id="34b76-137">Use an existing action group in your activity log alert.</span></span> 
* <span data-ttu-id="34b76-138">Utwórz nową grupę akcji.</span><span class="sxs-lookup"><span data-stu-id="34b76-138">Create a new action group.</span></span> 

<span data-ttu-id="34b76-139">toolearn więcej informacji na temat grup akcji, zobacz [Utwórz i Zarządzaj grupami akcji w portalu Azure hello](monitoring-action-groups.md).</span><span class="sxs-lookup"><span data-stu-id="34b76-139">toolearn more about action groups, see [Create and manage action groups in hello Azure portal](monitoring-action-groups.md).</span></span>

<span data-ttu-id="34b76-140">toolearn więcej informacji na temat powiadomień o kondycji usługi, zobacz [odbierzesz alerty dziennika działania dotyczące powiadomień o kondycji usługi](monitoring-activity-log-alerts-on-service-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="34b76-140">toolearn more about service health notifications, see [Receive activity log alerts on service health notifications](monitoring-activity-log-alerts-on-service-notifications.md).</span></span>

## <a name="create-an-alert-on-an-activity-log-event-with-a-new-action-group-by-using-hello-azure-portal"></a><span data-ttu-id="34b76-141">Utwórz alert na zdarzenie dziennika działania z nową grupą akcji przy użyciu hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="34b76-141">Create an alert on an activity log event with a new action group by using hello Azure portal</span></span>
1. <span data-ttu-id="34b76-142">W hello [portal](https://portal.azure.com), wybierz pozycję **Monitor**.</span><span class="sxs-lookup"><span data-stu-id="34b76-142">In hello [portal](https://portal.azure.com), select **Monitor**.</span></span>

    ![Witaj "Monitora" usługi](./media/monitoring-activity-log-alerts/home-monitor.png)
2. <span data-ttu-id="34b76-144">W hello **dziennik aktywności** zaznacz **alerty**.</span><span class="sxs-lookup"><span data-stu-id="34b76-144">In hello **Activity log** section, select **Alerts**.</span></span>

    ![Karta "Alertów" Hello](./media/monitoring-activity-log-alerts/alerts-blades.png)
3. <span data-ttu-id="34b76-146">Wybierz **alert dziennika aktywności Dodaj**, a następnie wypełnij pola hello.</span><span class="sxs-lookup"><span data-stu-id="34b76-146">Select **Add activity log alert**, and fill in hello fields.</span></span>

4. <span data-ttu-id="34b76-147">Wprowadź nazwę w hello **nazwa alertu dziennika aktywności** i wybierz **opis**.</span><span class="sxs-lookup"><span data-stu-id="34b76-147">Enter a name in hello **Activity log alert name** box, and select a **Description**.</span></span>

    ![Witaj polecenie "Dodaj alert dziennika aktywności"](./media/monitoring-activity-log-alerts/add-activity-log-alert.png)

5. <span data-ttu-id="34b76-149">Witaj **subskrypcji** polu autofills z Twojej bieżącej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="34b76-149">hello **Subscription** box autofills with your current subscription.</span></span> <span data-ttu-id="34b76-150">Ta subskrypcja jest hello jedną grupy akcji hello, do której jest zapisywany.</span><span class="sxs-lookup"><span data-stu-id="34b76-150">This subscription is hello one in which hello action group is saved.</span></span> <span data-ttu-id="34b76-151">zasób alertu Hello jest wdrożony toothis subskrypcji i monitory działania zdarzenia dziennika z niego.</span><span class="sxs-lookup"><span data-stu-id="34b76-151">hello alert resource is deployed toothis subscription and monitors activity log events from it.</span></span>

    ![okno dialogowe "Dodaj alert dziennika aktywności" Hello](./media/monitoring-activity-log-alerts/activity-log-alert-new-action-group.png)

6. <span data-ttu-id="34b76-153">Wybierz hello **grupy zasobów** w których hello alertu zasób został utworzony.</span><span class="sxs-lookup"><span data-stu-id="34b76-153">Select hello **Resource group** in which hello alert resource is created.</span></span> <span data-ttu-id="34b76-154">To nie jest hello grupy zasobów, które monitorują hello alertu.</span><span class="sxs-lookup"><span data-stu-id="34b76-154">This is not hello resource group that's monitored by hello alert.</span></span> <span data-ttu-id="34b76-155">Zamiast tego jest hello grupy zasobów, gdzie znajduje się zasób alertu hello.</span><span class="sxs-lookup"><span data-stu-id="34b76-155">Instead, it's hello resource group where hello alert resource is located.</span></span>

7. <span data-ttu-id="34b76-156">Opcjonalnie wybierz **kategorii zdarzeń** toomodify hello dodatkowe filtry, które są wyświetlane.</span><span class="sxs-lookup"><span data-stu-id="34b76-156">Optionally, select an **Event category** toomodify hello additional filters that are shown.</span></span> <span data-ttu-id="34b76-157">Zdarzenia administracyjne są następujące filtry hello **grupy zasobów**, **zasobów**, **typu zasobu**, **nazwy operacji**, **Poziom**, **stan**, i **zdarzenie inicjowane przez**.</span><span class="sxs-lookup"><span data-stu-id="34b76-157">For Administrative events, hello filters include **Resource group**, **Resource**, **Resource type**, **Operation name**, **Level**, **Status**, and **Event initiated by**.</span></span> <span data-ttu-id="34b76-158">Identyfikuje te zdarzenia, które należy monitorować ten alert.</span><span class="sxs-lookup"><span data-stu-id="34b76-158">These values identify which events this alert should monitor.</span></span>

    >[!NOTE]
    ><span data-ttu-id="34b76-159">Należy określić co najmniej jeden z hello poprzedzające kryteria alertu.</span><span class="sxs-lookup"><span data-stu-id="34b76-159">You must specify at least one of hello preceding criteria in your alert.</span></span> <span data-ttu-id="34b76-160">Nie można utworzyć alertu, który uaktywnia każdorazowego zdarzenie jest tworzone w dziennikach działania hello.</span><span class="sxs-lookup"><span data-stu-id="34b76-160">You may not create an alert that activates every time an event is created in hello activity logs.</span></span>
    >
    >

8. <span data-ttu-id="34b76-161">Wprowadź nazwę w hello **nazwy grupy akcji** i wpisz nazwę w hello **krótką nazwę** pole.</span><span class="sxs-lookup"><span data-stu-id="34b76-161">Enter a name in hello **Action group name** box, and enter a name in hello **Short name** box.</span></span> <span data-ttu-id="34b76-162">Krótka nazwa Hello jest używany zamiast akcji pełną nazwę grupy, podczas powiadomienia są wysyłane przy użyciu tej grupy.</span><span class="sxs-lookup"><span data-stu-id="34b76-162">hello short name is used in place of a full action group name when notifications are sent using this group.</span></span>

9.  <span data-ttu-id="34b76-163">Zdefiniuj listę działań przez zapewnienie hello akcji:</span><span class="sxs-lookup"><span data-stu-id="34b76-163">Define a list of actions by providing hello action’s:</span></span>

    <span data-ttu-id="34b76-164">a.</span><span class="sxs-lookup"><span data-stu-id="34b76-164">a.</span></span> <span data-ttu-id="34b76-165">**Nazwa**: Wprowadź nazwę, alias lub identyfikator akcji hello.</span><span class="sxs-lookup"><span data-stu-id="34b76-165">**Name**: Enter hello action’s name, alias, or identifier.</span></span>

    <span data-ttu-id="34b76-166">b.</span><span class="sxs-lookup"><span data-stu-id="34b76-166">b.</span></span> <span data-ttu-id="34b76-167">**Typ akcji**: Wybierz SMS, wiadomości e-mail lub elementu webhook.</span><span class="sxs-lookup"><span data-stu-id="34b76-167">**Action Type**: Select SMS, email, or webhook.</span></span>

    <span data-ttu-id="34b76-168">c.</span><span class="sxs-lookup"><span data-stu-id="34b76-168">c.</span></span> <span data-ttu-id="34b76-169">**Szczegóły**: oparte na typ akcji hello, wprowadź numer telefonu, adres e-mail lub identyfikator URI elementu webhook.</span><span class="sxs-lookup"><span data-stu-id="34b76-169">**Details**: Based on hello action type, enter a phone number, email address, or webhook URI.</span></span>

10. <span data-ttu-id="34b76-170">Wybierz **OK** toocreate hello alertu.</span><span class="sxs-lookup"><span data-stu-id="34b76-170">Select **OK** toocreate hello alert.</span></span>

<span data-ttu-id="34b76-171">Hello alert zajmuje kilka minut toofully propagacji i stanie się aktywne.</span><span class="sxs-lookup"><span data-stu-id="34b76-171">hello alert takes a few minutes toofully propagate and then become active.</span></span> <span data-ttu-id="34b76-172">Uruchamia go, gdy nowe zdarzenia spełniających kryteria alertu hello.</span><span class="sxs-lookup"><span data-stu-id="34b76-172">It triggers when new events match hello alert's criteria.</span></span>

<span data-ttu-id="34b76-173">Aby uzyskać więcej informacji, zobacz [schematu elementu webhook hello omówienie używane w alertach dziennika aktywności](monitoring-activity-log-alerts-webhook.md).</span><span class="sxs-lookup"><span data-stu-id="34b76-173">For more information, see [Understand hello webhook schema used in activity log alerts](monitoring-activity-log-alerts-webhook.md).</span></span>

>[!NOTE]
><span data-ttu-id="34b76-174">Grupa akcji Hello zdefiniowane w tych kroków znajduje się do ponownego użycia istniejącej grupy akcji dla wszystkich przyszłych definicji alertu.</span><span class="sxs-lookup"><span data-stu-id="34b76-174">hello action group defined in these steps is reusable as an existing action group for all future alert definitions.</span></span>
>
>

## <a name="create-an-alert-on-an-activity-log-event-for-an-existing-action-group-by-using-hello-azure-portal"></a><span data-ttu-id="34b76-175">Utwórz alert na działania dziennika zdarzeń dla istniejącej grupy akcji przy użyciu hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="34b76-175">Create an alert on an activity log event for an existing action group by using hello Azure portal</span></span>
1. <span data-ttu-id="34b76-176">Wykonaj kroki od 1 do 7 w hello poprzedniej sekcji toocreate alertu dziennika aktywności.</span><span class="sxs-lookup"><span data-stu-id="34b76-176">Follow steps 1 through 7 in hello previous section toocreate your activity log alert.</span></span>

2. <span data-ttu-id="34b76-177">W obszarze **powiadomienia za pośrednictwem**, wybierz pozycję hello **istniejące** przycisku grupy akcji.</span><span class="sxs-lookup"><span data-stu-id="34b76-177">Under **Notify via**, select hello **Existing** action group button.</span></span> <span data-ttu-id="34b76-178">Wybierz istniejącą grupę akcji z listy hello.</span><span class="sxs-lookup"><span data-stu-id="34b76-178">Select an existing action group from hello list.</span></span>

3. <span data-ttu-id="34b76-179">Wybierz **OK** toocreate hello alertu.</span><span class="sxs-lookup"><span data-stu-id="34b76-179">Select **OK** toocreate hello alert.</span></span>

<span data-ttu-id="34b76-180">Hello alert zajmuje kilka minut toofully propagacji i stanie się aktywne.</span><span class="sxs-lookup"><span data-stu-id="34b76-180">hello alert takes a few minutes toofully propagate and then become active.</span></span> <span data-ttu-id="34b76-181">Uruchamia go, gdy nowe zdarzenia spełniających kryteria alertu hello.</span><span class="sxs-lookup"><span data-stu-id="34b76-181">It triggers when new events match hello alert's criteria.</span></span>

## <a name="manage-your-alerts"></a><span data-ttu-id="34b76-182">Zarządzanie alertami</span><span class="sxs-lookup"><span data-stu-id="34b76-182">Manage your alerts</span></span>

<span data-ttu-id="34b76-183">Po utworzeniu alertu jest widoczna w sekcji alerty hello hello Monitor bloku.</span><span class="sxs-lookup"><span data-stu-id="34b76-183">After you create an alert, it's visible in hello Alerts section of hello Monitor blade.</span></span> <span data-ttu-id="34b76-184">Wybierz alert hello, który ma toomanage do:</span><span class="sxs-lookup"><span data-stu-id="34b76-184">Select hello alert you want toomanage to:</span></span>

* <span data-ttu-id="34b76-185">Czy chcesz go edytować.</span><span class="sxs-lookup"><span data-stu-id="34b76-185">Edit it.</span></span>
* <span data-ttu-id="34b76-186">Usuń go.</span><span class="sxs-lookup"><span data-stu-id="34b76-186">Delete it.</span></span>
* <span data-ttu-id="34b76-187">Wyłączone lub włączone, jeśli chcesz zatrzymać tootemporarily lub wznowić odbieranie powiadomień o alercie hello.</span><span class="sxs-lookup"><span data-stu-id="34b76-187">Disable or enable it, if you want tootemporarily stop or resume receiving notifications for hello alert.</span></span>

## <a name="next-steps"></a><span data-ttu-id="34b76-188">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="34b76-188">Next steps</span></span>
- <span data-ttu-id="34b76-189">Pobierz [Przegląd alertów](monitoring-overview-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="34b76-189">Get an [overview of alerts](monitoring-overview-alerts.md).</span></span>
- <span data-ttu-id="34b76-190">Dowiedz się więcej o [limitów szybkości powiadomień](monitoring-alerts-rate-limiting.md).</span><span class="sxs-lookup"><span data-stu-id="34b76-190">Learn about [notification rate limiting](monitoring-alerts-rate-limiting.md).</span></span>
- <span data-ttu-id="34b76-191">Przejrzyj hello [schemat alertu elementu webhook dziennika aktywności](monitoring-activity-log-alerts-webhook.md).</span><span class="sxs-lookup"><span data-stu-id="34b76-191">Review hello [activity log alert webhook schema](monitoring-activity-log-alerts-webhook.md).</span></span>
- <span data-ttu-id="34b76-192">Dowiedz się więcej o [grupy akcji](monitoring-action-groups.md).</span><span class="sxs-lookup"><span data-stu-id="34b76-192">Learn more about [action groups](monitoring-action-groups.md).</span></span>  
- <span data-ttu-id="34b76-193">Dowiedz się więcej o [usługi powiadomień o kondycji](monitoring-service-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="34b76-193">Learn about [service health notifications](monitoring-service-notifications.md).</span></span>
- <span data-ttu-id="34b76-194">Utwórz [działania logowania alertu toomonitor wszystkie operacje aparat skalowania automatycznego na subskrypcję](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert).</span><span class="sxs-lookup"><span data-stu-id="34b76-194">Create an [activity log alert toomonitor all autoscale engine operations on your subscription](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert).</span></span>
- <span data-ttu-id="34b76-195">Utwórz [aktywności logowania alertu toomonitor wszystkie operacje w/skali skalowalnych w poziomie skalowania automatycznego nie powiodło się w ramach subskrypcji](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert).</span><span class="sxs-lookup"><span data-stu-id="34b76-195">Create an [activity log alert toomonitor all failed autoscale scale-in/scale-out operations on your subscription](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert).</span></span>
