---
title: "aaaReceive działania dziennika alerty w przypadku powiadomień dotyczących usługi | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: dd35e8f39d2a522efdae4dfed20779c992c1dd27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-activity-log-alerts-on-service-notifications"></a><span data-ttu-id="c713d-103">Utwórz działanie alertów dziennika na powiadomień usługi</span><span class="sxs-lookup"><span data-stu-id="c713d-103">Create activity log alerts on service notifications</span></span>
## <a name="overview"></a><span data-ttu-id="c713d-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="c713d-104">Overview</span></span>
<span data-ttu-id="c713d-105">W tym artykule opisano, jak tooset dziennika aktywności alerty dla powiadomień o kondycji usługi za pomocą hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="c713d-105">This article shows you how tooset up activity log alerts for service health notifications by using hello Azure portal.</span></span>  

<span data-ttu-id="c713d-106">Użytkownik otrzyma alert, gdy Azure wysyła tooyour powiadomienia o kondycji usługi subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c713d-106">You can receive an alert when Azure sends service health notifications tooyour Azure subscription.</span></span> <span data-ttu-id="c713d-107">Można skonfigurować alerty hello na podstawie:</span><span class="sxs-lookup"><span data-stu-id="c713d-107">You can configure hello alert based on:</span></span>

- <span data-ttu-id="c713d-108">Klasa Hello powiadomienia kondycji usługi (zdarzenia konserwacji, informacje, itp.).</span><span class="sxs-lookup"><span data-stu-id="c713d-108">hello class of service health notification (incident, maintenance, information, etc.).</span></span>
- <span data-ttu-id="c713d-109">Hello usług, których to dotyczy.</span><span class="sxs-lookup"><span data-stu-id="c713d-109">hello service(s) affected.</span></span>
- <span data-ttu-id="c713d-110">Witaj regionów, w których to dotyczy.</span><span class="sxs-lookup"><span data-stu-id="c713d-110">hello region(s) affected.</span></span>
- <span data-ttu-id="c713d-111">Stan Hello hello powiadomienia (aktywny lub rozwiązany).</span><span class="sxs-lookup"><span data-stu-id="c713d-111">hello status of hello notification (active vs. resolved).</span></span>
- <span data-ttu-id="c713d-112">poziom Hello hello powiadomienia (błąd informacyjny, ostrzeżenie,).</span><span class="sxs-lookup"><span data-stu-id="c713d-112">hello level of hello notifications (informational, warning, error).</span></span>

<span data-ttu-id="c713d-113">Można także skonfigurować kogo wysyłane hello alertu:</span><span class="sxs-lookup"><span data-stu-id="c713d-113">You also can configure who hello alert should be sent to:</span></span>

- <span data-ttu-id="c713d-114">Wybierz istniejącą grupę akcji.</span><span class="sxs-lookup"><span data-stu-id="c713d-114">Select an existing action group.</span></span>
- <span data-ttu-id="c713d-115">Utwórz nową grupę akcję (która może służyć do następnych alertów).</span><span class="sxs-lookup"><span data-stu-id="c713d-115">Create a new action group (that can be used for future alerts).</span></span>

<span data-ttu-id="c713d-116">toolearn więcej informacji na temat grup akcji, zobacz [Utwórz i Zarządzaj grupami akcji](monitoring-action-groups.md).</span><span class="sxs-lookup"><span data-stu-id="c713d-116">toolearn more about action groups, see [Create and manage action groups](monitoring-action-groups.md).</span></span>

<span data-ttu-id="c713d-117">Aby uzyskać informacji na temat sposobu powiadomienia kondycji usługi tooconfigure alerty przy użyciu szablonów usługi Azure Resource Manager, zobacz [szablonów Resource Manager](monitoring-create-activity-log-alerts-with-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="c713d-117">For information on how tooconfigure service health notification alerts by using Azure Resource Manager templates, see [Resource Manager templates](monitoring-create-activity-log-alerts-with-resource-manager-template.md).</span></span>

## <a name="create-an-alert-on-a-service-health-notification-for-a-new-action-group-by-using-hello-azure-portal"></a><span data-ttu-id="c713d-118">Utwórz alert na powiadomienia kondycji usługi dla nowej grupy akcji przy użyciu hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="c713d-118">Create an alert on a service health notification for a new action group by using hello Azure portal</span></span>
1. <span data-ttu-id="c713d-119">W hello [portal](https://portal.azure.com), wybierz pozycję **Monitor**.</span><span class="sxs-lookup"><span data-stu-id="c713d-119">In hello [portal](https://portal.azure.com), select **Monitor**.</span></span>

    ![Witaj "Monitora" usługi](./media/monitoring-activity-log-alerts-on-service-notifications/home-monitor.png)

2. <span data-ttu-id="c713d-121">W hello **dziennik aktywności** zaznacz **alerty**.</span><span class="sxs-lookup"><span data-stu-id="c713d-121">In hello **Activity log** section, select **Alerts**.</span></span>

    ![Karta "Alertów" Hello](./media/monitoring-activity-log-alerts-on-service-notifications/alerts-blades.png)

3. <span data-ttu-id="c713d-123">Wybierz **alert dziennika aktywności Dodaj**, a następnie wypełnij pola hello.</span><span class="sxs-lookup"><span data-stu-id="c713d-123">Select **Add activity log alert**, and fill in hello fields.</span></span>

    ![Witaj polecenie "Dodaj alert dziennika aktywności"](./media/monitoring-activity-log-alerts-on-service-notifications/add-activity-log-alert.png)

4. <span data-ttu-id="c713d-125">Wprowadź nazwę w hello **nazwa alertu dziennika aktywności** polu i podaj **opis**.</span><span class="sxs-lookup"><span data-stu-id="c713d-125">Enter a name in hello **Activity log alert name** box, and provide a **Description**.</span></span>

    ![okno dialogowe "Dodaj alert dziennika aktywności" Hello](./media/monitoring-activity-log-alerts-on-service-notifications/activity-log-alert-service-notification-new-action-group.png)

5. <span data-ttu-id="c713d-127">Witaj **subskrypcji** polu autofills z Twojej bieżącej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="c713d-127">hello **Subscription** box autofills with your current subscription.</span></span> <span data-ttu-id="c713d-128">Ta subskrypcja jest alert dziennika aktywności hello toosave używane.</span><span class="sxs-lookup"><span data-stu-id="c713d-128">This subscription is used toosave hello activity log alert.</span></span> <span data-ttu-id="c713d-129">zasób alertu Hello jest wdrożone toothis subskrypcji i monitory zdarzeń w dzienniku aktywności hello dla niego.</span><span class="sxs-lookup"><span data-stu-id="c713d-129">hello alert resource is deployed toothis subscription and monitors events in hello activity log for it.</span></span>

6. <span data-ttu-id="c713d-130">Wybierz hello **grupy zasobów** w których hello alertu zasób został utworzony.</span><span class="sxs-lookup"><span data-stu-id="c713d-130">Select hello **Resource group** in which hello alert resource is created.</span></span> <span data-ttu-id="c713d-131">Nie jest to hello grupy zasobów, które monitorują hello alertu.</span><span class="sxs-lookup"><span data-stu-id="c713d-131">This isn't hello resource group that's monitored by hello alert.</span></span> <span data-ttu-id="c713d-132">Zamiast tego jest hello grupy zasobów, gdzie znajduje się zasób alertu hello.</span><span class="sxs-lookup"><span data-stu-id="c713d-132">Instead, it's hello resource group where hello alert resource is located.</span></span>

7. <span data-ttu-id="c713d-133">W hello **kategorii zdarzeń** wybierz opcję **kondycja usługi**.</span><span class="sxs-lookup"><span data-stu-id="c713d-133">In hello **Event category** box, select **Service Health**.</span></span> <span data-ttu-id="c713d-134">Opcjonalnie wybierz hello **usługi**, **Region**, **typu**, **stan**, i **poziom** usługi powiadomienia o kondycji, które mają tooreceive.</span><span class="sxs-lookup"><span data-stu-id="c713d-134">Optionally, select hello **Service**, **Region**, **Type**, **Status**, and **Level** of service health notifications that you want tooreceive.</span></span>

8. <span data-ttu-id="c713d-135">W obszarze **alertów za pośrednictwem**, wybierz pozycję hello **nowy** przycisku grupy akcji.</span><span class="sxs-lookup"><span data-stu-id="c713d-135">Under **Alert via**, select hello **New** action group button.</span></span> <span data-ttu-id="c713d-136">Wprowadź nazwę w hello **nazwy grupy akcji** i wpisz nazwę w hello **krótką nazwę** pole.</span><span class="sxs-lookup"><span data-stu-id="c713d-136">Enter a name in hello **Action group name** box, and enter a name in hello **Short name** box.</span></span> <span data-ttu-id="c713d-137">Krótka nazwa Hello odwołuje się do hello powiadomienia, które są wysyłane po zgłoszeniu tego alertu.</span><span class="sxs-lookup"><span data-stu-id="c713d-137">hello short name is referenced in hello notifications that are sent when this alert fires.</span></span>

9. <span data-ttu-id="c713d-138">Zdefiniuj listy odbiorców zapewniając odbiornika hello:</span><span class="sxs-lookup"><span data-stu-id="c713d-138">Define a list of receivers by providing hello receiver's:</span></span>

    <span data-ttu-id="c713d-139">a.</span><span class="sxs-lookup"><span data-stu-id="c713d-139">a.</span></span> <span data-ttu-id="c713d-140">**Nazwa**: Wprowadź nazwę odbiornika hello, alias lub identyfikator.</span><span class="sxs-lookup"><span data-stu-id="c713d-140">**Name**: Enter hello receiver’s name, alias, or identifier.</span></span>

    <span data-ttu-id="c713d-141">b.</span><span class="sxs-lookup"><span data-stu-id="c713d-141">b.</span></span> <span data-ttu-id="c713d-142">**Typ akcji**: Wybierz SMS, wiadomości e-mail lub elementu webhook.</span><span class="sxs-lookup"><span data-stu-id="c713d-142">**Action Type**: Select SMS, email, or webhook.</span></span>

    <span data-ttu-id="c713d-143">c.</span><span class="sxs-lookup"><span data-stu-id="c713d-143">c.</span></span> <span data-ttu-id="c713d-144">**Szczegóły**: oparte na wybrany typ akcji hello, wprowadź numer telefonu, adres e-mail lub identyfikator URI elementu webhook.</span><span class="sxs-lookup"><span data-stu-id="c713d-144">**Details**: Based on hello action type chosen, enter a phone number, email address, or webhook URI.</span></span>

10. <span data-ttu-id="c713d-145">Wybierz **OK** toocreate hello alertu.</span><span class="sxs-lookup"><span data-stu-id="c713d-145">Select **OK** toocreate hello alert.</span></span>

<span data-ttu-id="c713d-146">W ciągu kilku minut hello alert jest aktywny i rozpoczyna się tootrigger na podstawie hello warunków, które zostały określone podczas tworzenia.</span><span class="sxs-lookup"><span data-stu-id="c713d-146">Within a few minutes, hello alert is active and begins tootrigger based on hello conditions you specified during creation.</span></span>

<span data-ttu-id="c713d-147">Aby uzyskać informacje na powitania schematu elementu webhook dla alertów dotyczących działań w dzienniku, zobacz [elementów Webhook dla działania Azure rejestrowania alertów](monitoring-activity-log-alerts-webhook.md).</span><span class="sxs-lookup"><span data-stu-id="c713d-147">For information on hello webhook schema for activity log alerts, see [Webhooks for Azure activity log alerts](monitoring-activity-log-alerts-webhook.md).</span></span>

>[!NOTE]
><span data-ttu-id="c713d-148">Grupa akcji Hello zdefiniowane w tych kroków znajduje się do ponownego użycia istniejącej grupy akcji dla wszystkich przyszłych definicji alertu.</span><span class="sxs-lookup"><span data-stu-id="c713d-148">hello action group defined in these steps is reusable as an existing action group for all future alert definitions.</span></span>
>
>

## <a name="create-an-alert-on-a-service-health-notification-for-an-existing-action-group-by-using-hello-azure-portal"></a><span data-ttu-id="c713d-149">Utwórz alert na powiadomienia usługi kondycji dla istniejącej grupy akcji przy użyciu hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="c713d-149">Create an alert on a service health notification for an existing action group by using hello Azure portal</span></span>

1. <span data-ttu-id="c713d-150">Wykonaj kroki od 1 do 7 w hello poprzedniej sekcji toocreate powiadomienia usługi kondycji.</span><span class="sxs-lookup"><span data-stu-id="c713d-150">Follow steps 1 through 7 in hello previous section toocreate your service health notification.</span></span> 

2. <span data-ttu-id="c713d-151">W obszarze **alertów za pośrednictwem**, wybierz pozycję hello **istniejące** przycisku grupy akcji.</span><span class="sxs-lookup"><span data-stu-id="c713d-151">Under **Alert via**, select hello **Existing** action group button.</span></span> <span data-ttu-id="c713d-152">Wybierz grupę odpowiednią akcję hello.</span><span class="sxs-lookup"><span data-stu-id="c713d-152">Select hello appropriate action group.</span></span>

3. <span data-ttu-id="c713d-153">Wybierz **OK** toocreate hello alertu.</span><span class="sxs-lookup"><span data-stu-id="c713d-153">Select **OK** toocreate hello alert.</span></span>

<span data-ttu-id="c713d-154">W ciągu kilku minut hello alert jest aktywny i rozpoczyna się tootrigger na podstawie hello warunków, które zostały określone podczas tworzenia.</span><span class="sxs-lookup"><span data-stu-id="c713d-154">Within a few minutes, hello alert is active and begins tootrigger based on hello conditions you specified during creation.</span></span>

## <a name="manage-your-alerts"></a><span data-ttu-id="c713d-155">Zarządzanie alertami</span><span class="sxs-lookup"><span data-stu-id="c713d-155">Manage your alerts</span></span>

<span data-ttu-id="c713d-156">Po utworzeniu alertu nie jest widoczna hello **alerty** sekcji hello **Monitor** bloku.</span><span class="sxs-lookup"><span data-stu-id="c713d-156">After you create an alert, it's visible in hello **Alerts** section of hello **Monitor** blade.</span></span> <span data-ttu-id="c713d-157">Wybierz alert hello, który ma toomanage do:</span><span class="sxs-lookup"><span data-stu-id="c713d-157">Select hello alert you want toomanage to:</span></span>

* <span data-ttu-id="c713d-158">Czy chcesz go edytować.</span><span class="sxs-lookup"><span data-stu-id="c713d-158">Edit it.</span></span>
* <span data-ttu-id="c713d-159">Usuń go.</span><span class="sxs-lookup"><span data-stu-id="c713d-159">Delete it.</span></span>
* <span data-ttu-id="c713d-160">Wyłączone lub włączone, jeśli chcesz zatrzymać tootemporarily lub wznowić odbieranie powiadomień o alercie hello.</span><span class="sxs-lookup"><span data-stu-id="c713d-160">Disable or enable it, if you want tootemporarily stop or resume receiving notifications for hello alert.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c713d-161">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c713d-161">Next steps</span></span>
- <span data-ttu-id="c713d-162">Dowiedz się więcej o [usługi powiadomień o kondycji](monitoring-service-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="c713d-162">Learn about [service health notifications](monitoring-service-notifications.md).</span></span>
- <span data-ttu-id="c713d-163">Dowiedz się więcej o [limitów szybkości powiadomień](monitoring-alerts-rate-limiting.md).</span><span class="sxs-lookup"><span data-stu-id="c713d-163">Learn about [notification rate limiting](monitoring-alerts-rate-limiting.md).</span></span>
- <span data-ttu-id="c713d-164">Przejrzyj hello [schemat alertu elementu webhook dziennika aktywności](monitoring-activity-log-alerts-webhook.md).</span><span class="sxs-lookup"><span data-stu-id="c713d-164">Review hello [activity log alert webhook schema](monitoring-activity-log-alerts-webhook.md).</span></span>
- <span data-ttu-id="c713d-165">Pobierz [Przegląd alertów dotyczących działań w dzienniku](monitoring-overview-alerts.md)i Dowiedz się, jak tooreceive alertów.</span><span class="sxs-lookup"><span data-stu-id="c713d-165">Get an [overview of activity log alerts](monitoring-overview-alerts.md), and learn how tooreceive alerts.</span></span> 
- <span data-ttu-id="c713d-166">Dowiedz się więcej o [grupy akcji](monitoring-action-groups.md).</span><span class="sxs-lookup"><span data-stu-id="c713d-166">Learn more about [action groups](monitoring-action-groups.md).</span></span>
