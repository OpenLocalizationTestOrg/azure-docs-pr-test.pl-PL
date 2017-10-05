---
title: "Utwórz i Zarządzaj grupami akcji w portalu Azure | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie tworzenia i obsługi grup działań w portalu Azure."
author: anirudhcavale
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
ms.date: 05/15/2017
ms.author: ancav
ms.openlocfilehash: ea15705bf02d9773507c6cb59f2da4c1dd0f9d77
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="create-and-manage-action-groups-in-the-azure-portal"></a><span data-ttu-id="fd587-103">Utwórz i Zarządzaj grupami akcji w portalu Azure</span><span class="sxs-lookup"><span data-stu-id="fd587-103">Create and manage action groups in the Azure portal</span></span>
## <a name="overview"></a><span data-ttu-id="fd587-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="fd587-104">Overview</span></span> ##
<span data-ttu-id="fd587-105">W tym artykule przedstawiono sposób tworzenia i obsługi grup działań w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="fd587-105">This article shows you how to create and manage action groups in the Azure portal.</span></span>

<span data-ttu-id="fd587-106">Można skonfigurować listę akcji przy użyciu grup działań.</span><span class="sxs-lookup"><span data-stu-id="fd587-106">You can configure a list of actions with action groups.</span></span> <span data-ttu-id="fd587-107">Te grupy następnie mogą być używane podczas definiowania alertów dotyczących działań w dzienniku.</span><span class="sxs-lookup"><span data-stu-id="fd587-107">These groups then can be used when you define activity log alerts.</span></span> <span data-ttu-id="fd587-108">Następnie te grupy mogą być ponownie używane przez każdy alert dziennika aktywności, zdefiniowane przez użytkownika, zapewniając podjęcie te same akcje każdym razem, gdy zostanie wyzwolony alert dziennika aktywności.</span><span class="sxs-lookup"><span data-stu-id="fd587-108">These groups can then be reused by each activity log alert you define, ensuring that the same actions are taken each time the activity log alert is triggered.</span></span>

<span data-ttu-id="fd587-109">Grupy akcji może mieć maksymalnie 10 każdego typu akcji.</span><span class="sxs-lookup"><span data-stu-id="fd587-109">An action group can have up to 10 of each action type.</span></span> <span data-ttu-id="fd587-110">Każda akcja składa się z następującymi właściwościami:</span><span class="sxs-lookup"><span data-stu-id="fd587-110">Each action is made up of the following properties:</span></span>

* <span data-ttu-id="fd587-111">**Nazwa**: Unikatowy identyfikator grupy działań.</span><span class="sxs-lookup"><span data-stu-id="fd587-111">**Name**: A unique identifier within the action group.</span></span>  
* <span data-ttu-id="fd587-112">**Typ akcji**: Wyślij wiadomość SMS, Wyślij wiadomość e-mail lub wywołanie elementu webhook.</span><span class="sxs-lookup"><span data-stu-id="fd587-112">**Action type**: Send an SMS, send an email, or call a webhook.</span></span>  
* <span data-ttu-id="fd587-113">**Szczegóły**: odpowiadającego phone numer, adres e-mail lub identyfikator URI elementu webhook.</span><span class="sxs-lookup"><span data-stu-id="fd587-113">**Details**: The corresponding phone number, email address, or webhook URI.</span></span>

<span data-ttu-id="fd587-114">Aby uzyskać informacje na temat sposobu konfigurowania grup akcji za pomocą szablonów usługi Azure Resource Manager, zobacz [szablony Menedżera zasobów grupy akcji](monitoring-create-action-group-with-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="fd587-114">For information on how to use Azure Resource Manager templates to configure action groups, see [Action group Resource Manager templates](monitoring-create-action-group-with-resource-manager-template.md).</span></span>

## <a name="create-an-action-group-by-using-the-azure-portal"></a><span data-ttu-id="fd587-115">Utwórz grupę akcji przy użyciu portalu Azure</span><span class="sxs-lookup"><span data-stu-id="fd587-115">Create an action group by using the Azure portal</span></span> ##
1. <span data-ttu-id="fd587-116">W [portal](https://portal.azure.com), wybierz pozycję **Monitor**.</span><span class="sxs-lookup"><span data-stu-id="fd587-116">In the [portal](https://portal.azure.com), select **Monitor**.</span></span> <span data-ttu-id="fd587-117">**Monitor** bloku konsoliduje wszystkich monitorowania ustawień i danych w jednym widoku.</span><span class="sxs-lookup"><span data-stu-id="fd587-117">The **Monitor** blade consolidates all your monitoring settings and data in one view.</span></span>

    ![Usługa "Monitora"](./media/monitoring-action-groups/home-monitor.png)
2. <span data-ttu-id="fd587-119">W **dziennik aktywności** zaznacz **grupy akcji**.</span><span class="sxs-lookup"><span data-stu-id="fd587-119">In the **Activity log** section, select **Action groups**.</span></span>

    ![Na karcie "Grup akcji"](./media/monitoring-action-groups/action-groups-blade.png)
3. <span data-ttu-id="fd587-121">Wybierz **Dodaj grupę akcji**, a następnie wypełnij pola.</span><span class="sxs-lookup"><span data-stu-id="fd587-121">Select **Add action group**, and fill in the fields.</span></span>

    ![Polecenie "Dodaj grupę akcji"](./media/monitoring-action-groups/add-action-group.png)
4. <span data-ttu-id="fd587-123">Wprowadź nazwę w **nazwy grupy akcji** i wprowadzić nazwę w **krótką nazwę** pole.</span><span class="sxs-lookup"><span data-stu-id="fd587-123">Enter a name in the **Action group name** box, and enter a name in the **Short name** box.</span></span> <span data-ttu-id="fd587-124">Krótka nazwa jest używana zamiast akcji Pełna nazwa grupy, podczas powiadomienia są wysyłane przy użyciu tej grupy.</span><span class="sxs-lookup"><span data-stu-id="fd587-124">The short name is used in place of a full action group name when notifications are sent using this group.</span></span>

      ![Okno dialogowe Dodawanie grupy akcji"](./media/monitoring-action-groups/action-group-define.png)

5. <span data-ttu-id="fd587-126">**Subskrypcji** polu autofills z Twojej bieżącej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="fd587-126">The **Subscription** box autofills with your current subscription.</span></span> <span data-ttu-id="fd587-127">Ta subskrypcja jest jeden, w którym jest zapisany grupy akcji.</span><span class="sxs-lookup"><span data-stu-id="fd587-127">This subscription is the one in which the action group is saved.</span></span>

6. <span data-ttu-id="fd587-128">Wybierz **grupy zasobów** w jest zapisywany grupy akcji.</span><span class="sxs-lookup"><span data-stu-id="fd587-128">Select the **Resource group** in which the action group is saved.</span></span>

7. <span data-ttu-id="fd587-129">Zdefiniuj listę działań, zapewniając każdej akcji:</span><span class="sxs-lookup"><span data-stu-id="fd587-129">Define a list of actions by providing each action's:</span></span>

    <span data-ttu-id="fd587-130">a.</span><span class="sxs-lookup"><span data-stu-id="fd587-130">a.</span></span> <span data-ttu-id="fd587-131">**Nazwa**: wprowadź unikatowy identyfikator dla tej akcji.</span><span class="sxs-lookup"><span data-stu-id="fd587-131">**Name**: Enter a unique identifier for this action.</span></span>

    <span data-ttu-id="fd587-132">b.</span><span class="sxs-lookup"><span data-stu-id="fd587-132">b.</span></span> <span data-ttu-id="fd587-133">**Typ akcji**: Wybierz SMS, wiadomości e-mail lub elementu webhook.</span><span class="sxs-lookup"><span data-stu-id="fd587-133">**Action Type**: Select SMS, email, or webhook.</span></span>

    <span data-ttu-id="fd587-134">c.</span><span class="sxs-lookup"><span data-stu-id="fd587-134">c.</span></span> <span data-ttu-id="fd587-135">**Szczegóły**: oparte na typ akcji, wprowadź numer telefonu, adres e-mail lub identyfikator URI elementu webhook.</span><span class="sxs-lookup"><span data-stu-id="fd587-135">**Details**: Based on the action type, enter a phone number, email address, or webhook URI.</span></span>

8. <span data-ttu-id="fd587-136">Wybierz **OK** można utworzyć grupy działań.</span><span class="sxs-lookup"><span data-stu-id="fd587-136">Select **OK** to create the action group.</span></span>

## <a name="manage-your-action-groups"></a><span data-ttu-id="fd587-137">Zarządzanie grupami akcji</span><span class="sxs-lookup"><span data-stu-id="fd587-137">Manage your action groups</span></span> ##
<span data-ttu-id="fd587-138">Po utworzeniu grupy akcji jest widoczna w **grupy akcji** sekcji **Monitor** bloku.</span><span class="sxs-lookup"><span data-stu-id="fd587-138">After you create an action group, it's visible in the **Action groups** section of the **Monitor** blade.</span></span> <span data-ttu-id="fd587-139">Wybierz grupę akcji, którą chcesz zarządzać, aby:</span><span class="sxs-lookup"><span data-stu-id="fd587-139">Select the action group you want to manage to:</span></span>

* <span data-ttu-id="fd587-140">Dodawanie, edytowanie lub usuwanie akcji.</span><span class="sxs-lookup"><span data-stu-id="fd587-140">Add, edit, or remove actions.</span></span>
* <span data-ttu-id="fd587-141">Usuwanie grupy działań.</span><span class="sxs-lookup"><span data-stu-id="fd587-141">Delete the action group.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fd587-142">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="fd587-142">Next steps</span></span> ##
* <span data-ttu-id="fd587-143">Dowiedz się więcej o [SMS alertów zachowanie](monitoring-sms-alert-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="fd587-143">Learn more about [SMS alert behavior](monitoring-sms-alert-behavior.md).</span></span>  
* <span data-ttu-id="fd587-144">Uzyskaj [zrozumienia schemat alertu elementu webhook dziennika aktywności](monitoring-activity-log-alerts-webhook.md).</span><span class="sxs-lookup"><span data-stu-id="fd587-144">Gain an [understanding of the activity log alert webhook schema](monitoring-activity-log-alerts-webhook.md).</span></span>  
* <span data-ttu-id="fd587-145">Dowiedz się więcej o [limitów szybkości](monitoring-alerts-rate-limiting.md) alertów.</span><span class="sxs-lookup"><span data-stu-id="fd587-145">Learn more about [rate limiting](monitoring-alerts-rate-limiting.md) on alerts.</span></span> 
* <span data-ttu-id="fd587-146">Pobierz [Przegląd alertów dotyczących działań w dzienniku](monitoring-overview-alerts.md)i dowiedzieć się, jak otrzymywać alerty.</span><span class="sxs-lookup"><span data-stu-id="fd587-146">Get an [overview of activity log alerts](monitoring-overview-alerts.md), and learn how to receive alerts.</span></span>  
* <span data-ttu-id="fd587-147">Dowiedz się, jak [skonfigurować alerty, gdy powiadomienie usługi kondycji jest przesyłana](monitoring-activity-log-alerts-on-service-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="fd587-147">Learn how to [configure alerts whenever a service health notification is posted](monitoring-activity-log-alerts-on-service-notifications.md).</span></span>
