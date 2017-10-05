---
title: "Odbierzesz alerty dziennika działania dotyczące powiadomień dotyczących usługi | Dokumentacja firmy Microsoft"
description: "Otrzymuj powiadomienia za pomocą programu SMS, wiadomości e-mail lub elementu webhook w przypadku wystąpienia usługi Azure."
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
ms.date: 03/31/2017
ms.author: johnkem
ms.openlocfilehash: bf6a98fd7e7e11764bef174f9efd0635fa7efe9a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="create-activity-log-alerts-on-service-notifications"></a><span data-ttu-id="4fdcc-103">Utwórz działanie alertów dziennika na powiadomień usługi</span><span class="sxs-lookup"><span data-stu-id="4fdcc-103">Create activity log alerts on service notifications</span></span>
## <a name="overview"></a><span data-ttu-id="4fdcc-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="4fdcc-104">Overview</span></span>
<span data-ttu-id="4fdcc-105">W tym artykule pokazano, jak skonfigurować alerty dziennika działania dotyczące powiadomień o kondycji usługi za pomocą portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="4fdcc-105">This article shows you how to set up activity log alerts for service health notifications by using the Azure portal.</span></span>  

<span data-ttu-id="4fdcc-106">Użytkownik otrzyma alert, gdy Azure wysyła powiadomienia o kondycji usługi do subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="4fdcc-106">You can receive an alert when Azure sends service health notifications to your Azure subscription.</span></span> <span data-ttu-id="4fdcc-107">Można skonfigurować alerty na podstawie:</span><span class="sxs-lookup"><span data-stu-id="4fdcc-107">You can configure the alert based on:</span></span>

- <span data-ttu-id="4fdcc-108">Klasa usługi kondycji powiadomienia (zdarzenia konserwacji, informacje, itp.).</span><span class="sxs-lookup"><span data-stu-id="4fdcc-108">The class of service health notification (incident, maintenance, information, etc.).</span></span>
- <span data-ttu-id="4fdcc-109">Usług, których to dotyczy.</span><span class="sxs-lookup"><span data-stu-id="4fdcc-109">The service(s) affected.</span></span>
- <span data-ttu-id="4fdcc-110">Regionów, których to dotyczy.</span><span class="sxs-lookup"><span data-stu-id="4fdcc-110">The region(s) affected.</span></span>
- <span data-ttu-id="4fdcc-111">Stan powiadomienia (aktywny lub rozwiązany).</span><span class="sxs-lookup"><span data-stu-id="4fdcc-111">The status of the notification (active vs. resolved).</span></span>
- <span data-ttu-id="4fdcc-112">Poziom powiadomienia (błąd informacyjny, ostrzeżenie,).</span><span class="sxs-lookup"><span data-stu-id="4fdcc-112">The level of the notifications (informational, warning, error).</span></span>

<span data-ttu-id="4fdcc-113">Można także skonfigurować kogo wysyłane alertu:</span><span class="sxs-lookup"><span data-stu-id="4fdcc-113">You also can configure who the alert should be sent to:</span></span>

- <span data-ttu-id="4fdcc-114">Wybierz istniejącą grupę akcji.</span><span class="sxs-lookup"><span data-stu-id="4fdcc-114">Select an existing action group.</span></span>
- <span data-ttu-id="4fdcc-115">Utwórz nową grupę akcję (która może służyć do następnych alertów).</span><span class="sxs-lookup"><span data-stu-id="4fdcc-115">Create a new action group (that can be used for future alerts).</span></span>

<span data-ttu-id="4fdcc-116">Aby dowiedzieć się więcej o grupach akcji, zobacz [Utwórz i Zarządzaj grupami akcji](monitoring-action-groups.md).</span><span class="sxs-lookup"><span data-stu-id="4fdcc-116">To learn more about action groups, see [Create and manage action groups](monitoring-action-groups.md).</span></span>

<span data-ttu-id="4fdcc-117">Aby uzyskać informacje na temat konfigurowania alertów powiadomień kondycji usługi przy użyciu szablonów usługi Azure Resource Manager, zobacz [szablonów Resource Manager](monitoring-create-activity-log-alerts-with-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="4fdcc-117">For information on how to configure service health notification alerts by using Azure Resource Manager templates, see [Resource Manager templates](monitoring-create-activity-log-alerts-with-resource-manager-template.md).</span></span>

## <a name="create-an-alert-on-a-service-health-notification-for-a-new-action-group-by-using-the-azure-portal"></a><span data-ttu-id="4fdcc-118">Utwórz alert na powiadomienia usługi kondycji dla nowej grupy akcji przy użyciu portalu Azure</span><span class="sxs-lookup"><span data-stu-id="4fdcc-118">Create an alert on a service health notification for a new action group by using the Azure portal</span></span>
1. <span data-ttu-id="4fdcc-119">W [portal](https://portal.azure.com), wybierz pozycję **Monitor**.</span><span class="sxs-lookup"><span data-stu-id="4fdcc-119">In the [portal](https://portal.azure.com), select **Monitor**.</span></span>

    ![Usługa "Monitora"](./media/monitoring-activity-log-alerts-on-service-notifications/home-monitor.png)

2. <span data-ttu-id="4fdcc-121">W **dziennik aktywności** zaznacz **alerty**.</span><span class="sxs-lookup"><span data-stu-id="4fdcc-121">In the **Activity log** section, select **Alerts**.</span></span>

    ![Karta "Alertów"](./media/monitoring-activity-log-alerts-on-service-notifications/alerts-blades.png)

3. <span data-ttu-id="4fdcc-123">Wybierz **alert dziennika aktywności Dodaj**, a następnie wypełnij pola.</span><span class="sxs-lookup"><span data-stu-id="4fdcc-123">Select **Add activity log alert**, and fill in the fields.</span></span>

    ![Polecenie "Dodaj działanie dziennika alert"](./media/monitoring-activity-log-alerts-on-service-notifications/add-activity-log-alert.png)

4. <span data-ttu-id="4fdcc-125">Wprowadź nazwę w **nazwa alertu dziennika aktywności** polu i podaj **opis**.</span><span class="sxs-lookup"><span data-stu-id="4fdcc-125">Enter a name in the **Activity log alert name** box, and provide a **Description**.</span></span>

    ![Okno dialogowe "Dodaj alert dziennika aktywności"](./media/monitoring-activity-log-alerts-on-service-notifications/activity-log-alert-service-notification-new-action-group.png)

5. <span data-ttu-id="4fdcc-127">**Subskrypcji** polu autofills z Twojej bieżącej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="4fdcc-127">The **Subscription** box autofills with your current subscription.</span></span> <span data-ttu-id="4fdcc-128">Ta subskrypcja służy do zapisania alert dziennika aktywności.</span><span class="sxs-lookup"><span data-stu-id="4fdcc-128">This subscription is used to save the activity log alert.</span></span> <span data-ttu-id="4fdcc-129">Zasób alertu jest wdrażana dla tej subskrypcji i monitorować zdarzenia w dzienniku aktywności.</span><span class="sxs-lookup"><span data-stu-id="4fdcc-129">The alert resource is deployed to this subscription and monitors events in the activity log for it.</span></span>

6. <span data-ttu-id="4fdcc-130">Wybierz **grupy zasobów** w jest tworzony zasób alertu.</span><span class="sxs-lookup"><span data-stu-id="4fdcc-130">Select the **Resource group** in which the alert resource is created.</span></span> <span data-ttu-id="4fdcc-131">Nie jest to grupa zasobów, który jest monitorowany przez alert.</span><span class="sxs-lookup"><span data-stu-id="4fdcc-131">This isn't the resource group that's monitored by the alert.</span></span> <span data-ttu-id="4fdcc-132">Zamiast tego jest grupy zasobów, w którym znajduje się zasób alertu.</span><span class="sxs-lookup"><span data-stu-id="4fdcc-132">Instead, it's the resource group where the alert resource is located.</span></span>

7. <span data-ttu-id="4fdcc-133">W **kategorii zdarzeń** wybierz opcję **kondycja usługi**.</span><span class="sxs-lookup"><span data-stu-id="4fdcc-133">In the **Event category** box, select **Service Health**.</span></span> <span data-ttu-id="4fdcc-134">Opcjonalnie wybierz **usługi**, **Region**, **typu**, **stan**, i **poziom** z powiadomień o kondycji usługi, które chcesz otrzymywać.</span><span class="sxs-lookup"><span data-stu-id="4fdcc-134">Optionally, select the **Service**, **Region**, **Type**, **Status**, and **Level** of service health notifications that you want to receive.</span></span>

8. <span data-ttu-id="4fdcc-135">W obszarze **alertów za pośrednictwem**, wybierz pozycję **nowy** przycisku grupy akcji.</span><span class="sxs-lookup"><span data-stu-id="4fdcc-135">Under **Alert via**, select the **New** action group button.</span></span> <span data-ttu-id="4fdcc-136">Wprowadź nazwę w **nazwy grupy akcji** i wprowadzić nazwę w **krótką nazwę** pole.</span><span class="sxs-lookup"><span data-stu-id="4fdcc-136">Enter a name in the **Action group name** box, and enter a name in the **Short name** box.</span></span> <span data-ttu-id="4fdcc-137">Krótka nazwa odwołuje się do powiadomień wysyłanych po zgłoszeniu tego alertu.</span><span class="sxs-lookup"><span data-stu-id="4fdcc-137">The short name is referenced in the notifications that are sent when this alert fires.</span></span>

9. <span data-ttu-id="4fdcc-138">Zdefiniować listę odbiornikami, zapewniając odbiorcy:</span><span class="sxs-lookup"><span data-stu-id="4fdcc-138">Define a list of receivers by providing the receiver's:</span></span>

    <span data-ttu-id="4fdcc-139">a.</span><span class="sxs-lookup"><span data-stu-id="4fdcc-139">a.</span></span> <span data-ttu-id="4fdcc-140">**Nazwa**: Wprowadź nazwę odbiorcy, aliasu lub identyfikator.</span><span class="sxs-lookup"><span data-stu-id="4fdcc-140">**Name**: Enter the receiver’s name, alias, or identifier.</span></span>

    <span data-ttu-id="4fdcc-141">b.</span><span class="sxs-lookup"><span data-stu-id="4fdcc-141">b.</span></span> <span data-ttu-id="4fdcc-142">**Typ akcji**: Wybierz SMS, wiadomości e-mail lub elementu webhook.</span><span class="sxs-lookup"><span data-stu-id="4fdcc-142">**Action Type**: Select SMS, email, or webhook.</span></span>

    <span data-ttu-id="4fdcc-143">c.</span><span class="sxs-lookup"><span data-stu-id="4fdcc-143">c.</span></span> <span data-ttu-id="4fdcc-144">**Szczegóły**: oparte na wybrany typ akcji, wprowadź numer telefonu, adres e-mail lub identyfikator URI elementu webhook.</span><span class="sxs-lookup"><span data-stu-id="4fdcc-144">**Details**: Based on the action type chosen, enter a phone number, email address, or webhook URI.</span></span>

10. <span data-ttu-id="4fdcc-145">Wybierz **OK** można utworzyć alertu.</span><span class="sxs-lookup"><span data-stu-id="4fdcc-145">Select **OK** to create the alert.</span></span>

<span data-ttu-id="4fdcc-146">W ciągu kilku minut alert jest aktywny i rozpoczyna się do wyzwalania na podstawie wybranych warunków, które zostały określone podczas tworzenia.</span><span class="sxs-lookup"><span data-stu-id="4fdcc-146">Within a few minutes, the alert is active and begins to trigger based on the conditions you specified during creation.</span></span>

<span data-ttu-id="4fdcc-147">Uzyskać informacji o schemacie elementu webhook dla alertów dotyczących działań w dzienniku, zobacz [elementów Webhook dla działania Azure rejestrowania alertów](monitoring-activity-log-alerts-webhook.md).</span><span class="sxs-lookup"><span data-stu-id="4fdcc-147">For information on the webhook schema for activity log alerts, see [Webhooks for Azure activity log alerts](monitoring-activity-log-alerts-webhook.md).</span></span>

>[!NOTE]
><span data-ttu-id="4fdcc-148">Do ponownego użycia istniejącej grupy akcji dla wszystkich przyszłych definicji alertu jest grupa akcji zdefiniowane w tych krokach.</span><span class="sxs-lookup"><span data-stu-id="4fdcc-148">The action group defined in these steps is reusable as an existing action group for all future alert definitions.</span></span>
>
>

## <a name="create-an-alert-on-a-service-health-notification-for-an-existing-action-group-by-using-the-azure-portal"></a><span data-ttu-id="4fdcc-149">Utwórz alert na powiadomienia usługi kondycji dla istniejącej grupy akcji przy użyciu portalu Azure</span><span class="sxs-lookup"><span data-stu-id="4fdcc-149">Create an alert on a service health notification for an existing action group by using the Azure portal</span></span>

1. <span data-ttu-id="4fdcc-150">Wykonaj kroki od 1 do 7 w poprzedniej sekcji, aby utworzyć powiadomienia usługi kondycji.</span><span class="sxs-lookup"><span data-stu-id="4fdcc-150">Follow steps 1 through 7 in the previous section to create your service health notification.</span></span> 

2. <span data-ttu-id="4fdcc-151">W obszarze **alertów za pośrednictwem**, wybierz pozycję **istniejące** przycisku grupy akcji.</span><span class="sxs-lookup"><span data-stu-id="4fdcc-151">Under **Alert via**, select the **Existing** action group button.</span></span> <span data-ttu-id="4fdcc-152">Wybierz grupę odpowiednią akcję.</span><span class="sxs-lookup"><span data-stu-id="4fdcc-152">Select the appropriate action group.</span></span>

3. <span data-ttu-id="4fdcc-153">Wybierz **OK** można utworzyć alertu.</span><span class="sxs-lookup"><span data-stu-id="4fdcc-153">Select **OK** to create the alert.</span></span>

<span data-ttu-id="4fdcc-154">W ciągu kilku minut alert jest aktywny i rozpoczyna się do wyzwalania na podstawie wybranych warunków, które zostały określone podczas tworzenia.</span><span class="sxs-lookup"><span data-stu-id="4fdcc-154">Within a few minutes, the alert is active and begins to trigger based on the conditions you specified during creation.</span></span>

## <a name="manage-your-alerts"></a><span data-ttu-id="4fdcc-155">Zarządzanie alertami</span><span class="sxs-lookup"><span data-stu-id="4fdcc-155">Manage your alerts</span></span>

<span data-ttu-id="4fdcc-156">Po utworzeniu alertu nie jest widoczna **alerty** sekcji **Monitor** bloku.</span><span class="sxs-lookup"><span data-stu-id="4fdcc-156">After you create an alert, it's visible in the **Alerts** section of the **Monitor** blade.</span></span> <span data-ttu-id="4fdcc-157">Wybierz alert, który ma być zarządzany do:</span><span class="sxs-lookup"><span data-stu-id="4fdcc-157">Select the alert you want to manage to:</span></span>

* <span data-ttu-id="4fdcc-158">Czy chcesz go edytować.</span><span class="sxs-lookup"><span data-stu-id="4fdcc-158">Edit it.</span></span>
* <span data-ttu-id="4fdcc-159">Usuń go.</span><span class="sxs-lookup"><span data-stu-id="4fdcc-159">Delete it.</span></span>
* <span data-ttu-id="4fdcc-160">Wyłącz lub włącz go, jeśli chcesz tymczasowo zatrzymać lub wznowić odbieranie powiadomień o alercie.</span><span class="sxs-lookup"><span data-stu-id="4fdcc-160">Disable or enable it, if you want to temporarily stop or resume receiving notifications for the alert.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4fdcc-161">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="4fdcc-161">Next steps</span></span>
- <span data-ttu-id="4fdcc-162">Dowiedz się więcej o [usługi powiadomień o kondycji](monitoring-service-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="4fdcc-162">Learn about [service health notifications](monitoring-service-notifications.md).</span></span>
- <span data-ttu-id="4fdcc-163">Dowiedz się więcej o [limitów szybkości powiadomień](monitoring-alerts-rate-limiting.md).</span><span class="sxs-lookup"><span data-stu-id="4fdcc-163">Learn about [notification rate limiting](monitoring-alerts-rate-limiting.md).</span></span>
- <span data-ttu-id="4fdcc-164">Przegląd [schemat alertu elementu webhook dziennika aktywności](monitoring-activity-log-alerts-webhook.md).</span><span class="sxs-lookup"><span data-stu-id="4fdcc-164">Review the [activity log alert webhook schema](monitoring-activity-log-alerts-webhook.md).</span></span>
- <span data-ttu-id="4fdcc-165">Pobierz [Przegląd alertów dotyczących działań w dzienniku](monitoring-overview-alerts.md)i dowiedzieć się, jak otrzymywać alerty.</span><span class="sxs-lookup"><span data-stu-id="4fdcc-165">Get an [overview of activity log alerts](monitoring-overview-alerts.md), and learn how to receive alerts.</span></span> 
- <span data-ttu-id="4fdcc-166">Dowiedz się więcej o [grupy akcji](monitoring-action-groups.md).</span><span class="sxs-lookup"><span data-stu-id="4fdcc-166">Learn more about [action groups](monitoring-action-groups.md).</span></span>
