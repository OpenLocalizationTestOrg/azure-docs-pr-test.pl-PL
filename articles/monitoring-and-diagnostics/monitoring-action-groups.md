---
title: "aaaCreate i Zarządzaj grupami akcji w hello portalu Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate grup działań w hello portalu Azure i zarządzanie nimi."
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
ms.openlocfilehash: 97e0b22bea7787fff6856f895a7e6256c177efd9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-action-groups-in-hello-azure-portal"></a><span data-ttu-id="bda24-103">Utwórz i Zarządzaj grupami akcji w hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="bda24-103">Create and manage action groups in hello Azure portal</span></span>
## <a name="overview"></a><span data-ttu-id="bda24-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="bda24-104">Overview</span></span> ##
<span data-ttu-id="bda24-105">W tym artykule opisano sposób toocreate grup działań w hello portalu Azure i zarządzanie nimi.</span><span class="sxs-lookup"><span data-stu-id="bda24-105">This article shows you how toocreate and manage action groups in hello Azure portal.</span></span>

<span data-ttu-id="bda24-106">Można skonfigurować listę akcji przy użyciu grup działań.</span><span class="sxs-lookup"><span data-stu-id="bda24-106">You can configure a list of actions with action groups.</span></span> <span data-ttu-id="bda24-107">Te grupy następnie mogą być używane podczas definiowania alertów dotyczących działań w dzienniku.</span><span class="sxs-lookup"><span data-stu-id="bda24-107">These groups then can be used when you define activity log alerts.</span></span> <span data-ttu-id="bda24-108">Następnie te grupy mogą być ponownie używane przez każdy alert dziennika aktywności, zdefiniowane przez użytkownika, zapewnienie, że powitalne same akcje podejmowane są zawsze, gdy zostanie wyzwolony alert dziennika aktywności hello.</span><span class="sxs-lookup"><span data-stu-id="bda24-108">These groups can then be reused by each activity log alert you define, ensuring that hello same actions are taken each time hello activity log alert is triggered.</span></span>

<span data-ttu-id="bda24-109">Grupy akcji może zawierać maksymalnie too10 każdego typu akcji.</span><span class="sxs-lookup"><span data-stu-id="bda24-109">An action group can have up too10 of each action type.</span></span> <span data-ttu-id="bda24-110">Każda akcja składa się z hello następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="bda24-110">Each action is made up of hello following properties:</span></span>

* <span data-ttu-id="bda24-111">**Nazwa**: Unikatowy identyfikator grupy hello akcji.</span><span class="sxs-lookup"><span data-stu-id="bda24-111">**Name**: A unique identifier within hello action group.</span></span>  
* <span data-ttu-id="bda24-112">**Typ akcji**: Wyślij wiadomość SMS, Wyślij wiadomość e-mail lub wywołanie elementu webhook.</span><span class="sxs-lookup"><span data-stu-id="bda24-112">**Action type**: Send an SMS, send an email, or call a webhook.</span></span>  
* <span data-ttu-id="bda24-113">**Szczegóły**: hello odpowiedni numer telefonu, adres e-mail lub identyfikator URI elementu webhook.</span><span class="sxs-lookup"><span data-stu-id="bda24-113">**Details**: hello corresponding phone number, email address, or webhook URI.</span></span>

<span data-ttu-id="bda24-114">Aby uzyskać informacje na temat toouse usługi Azure Resource Manager szablony tooconfigure akcji grupy, zobacz [szablony Menedżera zasobów grupy akcji](monitoring-create-action-group-with-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="bda24-114">For information on how toouse Azure Resource Manager templates tooconfigure action groups, see [Action group Resource Manager templates](monitoring-create-action-group-with-resource-manager-template.md).</span></span>

## <a name="create-an-action-group-by-using-hello-azure-portal"></a><span data-ttu-id="bda24-115">Utwórz grupy akcji, używając hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="bda24-115">Create an action group by using hello Azure portal</span></span> ##
1. <span data-ttu-id="bda24-116">W hello [portal](https://portal.azure.com), wybierz pozycję **Monitor**.</span><span class="sxs-lookup"><span data-stu-id="bda24-116">In hello [portal](https://portal.azure.com), select **Monitor**.</span></span> <span data-ttu-id="bda24-117">Witaj **Monitor** bloku konsoliduje wszystkich monitorowania ustawień i danych w jednym widoku.</span><span class="sxs-lookup"><span data-stu-id="bda24-117">hello **Monitor** blade consolidates all your monitoring settings and data in one view.</span></span>

    ![Witaj "Monitora" usługi](./media/monitoring-action-groups/home-monitor.png)
2. <span data-ttu-id="bda24-119">W hello **dziennik aktywności** zaznacz **grupy akcji**.</span><span class="sxs-lookup"><span data-stu-id="bda24-119">In hello **Activity log** section, select **Action groups**.</span></span>

    ![Witaj "Akcji grupy" karta](./media/monitoring-action-groups/action-groups-blade.png)
3. <span data-ttu-id="bda24-121">Wybierz **Dodaj grupę akcji**i wypełnij pola hello.</span><span class="sxs-lookup"><span data-stu-id="bda24-121">Select **Add action group**, and fill in hello fields.</span></span>

    ![Witaj polecenie "Dodaj grupę akcji"](./media/monitoring-action-groups/add-action-group.png)
4. <span data-ttu-id="bda24-123">Wprowadź nazwę w hello **nazwy grupy akcji** i wpisz nazwę w hello **krótką nazwę** pole.</span><span class="sxs-lookup"><span data-stu-id="bda24-123">Enter a name in hello **Action group name** box, and enter a name in hello **Short name** box.</span></span> <span data-ttu-id="bda24-124">Krótka nazwa Hello jest używany zamiast akcji pełną nazwę grupy, podczas powiadomienia są wysyłane przy użyciu tej grupy.</span><span class="sxs-lookup"><span data-stu-id="bda24-124">hello short name is used in place of a full action group name when notifications are sent using this group.</span></span>

      ![okno dialogowe Hello Dodawanie grupy akcji"](./media/monitoring-action-groups/action-group-define.png)

5. <span data-ttu-id="bda24-126">Witaj **subskrypcji** polu autofills z Twojej bieżącej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="bda24-126">hello **Subscription** box autofills with your current subscription.</span></span> <span data-ttu-id="bda24-127">Ta subskrypcja jest hello jedną grupy akcji hello, do której jest zapisywany.</span><span class="sxs-lookup"><span data-stu-id="bda24-127">This subscription is hello one in which hello action group is saved.</span></span>

6. <span data-ttu-id="bda24-128">Wybierz hello **grupy zasobów** w akcję hello jest zapisywana grupy.</span><span class="sxs-lookup"><span data-stu-id="bda24-128">Select hello **Resource group** in which hello action group is saved.</span></span>

7. <span data-ttu-id="bda24-129">Zdefiniuj listę działań, zapewniając każdej akcji:</span><span class="sxs-lookup"><span data-stu-id="bda24-129">Define a list of actions by providing each action's:</span></span>

    <span data-ttu-id="bda24-130">a.</span><span class="sxs-lookup"><span data-stu-id="bda24-130">a.</span></span> <span data-ttu-id="bda24-131">**Nazwa**: wprowadź unikatowy identyfikator dla tej akcji.</span><span class="sxs-lookup"><span data-stu-id="bda24-131">**Name**: Enter a unique identifier for this action.</span></span>

    <span data-ttu-id="bda24-132">b.</span><span class="sxs-lookup"><span data-stu-id="bda24-132">b.</span></span> <span data-ttu-id="bda24-133">**Typ akcji**: Wybierz SMS, wiadomości e-mail lub elementu webhook.</span><span class="sxs-lookup"><span data-stu-id="bda24-133">**Action Type**: Select SMS, email, or webhook.</span></span>

    <span data-ttu-id="bda24-134">c.</span><span class="sxs-lookup"><span data-stu-id="bda24-134">c.</span></span> <span data-ttu-id="bda24-135">**Szczegóły**: oparte na typ akcji hello, wprowadź numer telefonu, adres e-mail lub identyfikator URI elementu webhook.</span><span class="sxs-lookup"><span data-stu-id="bda24-135">**Details**: Based on hello action type, enter a phone number, email address, or webhook URI.</span></span>

8. <span data-ttu-id="bda24-136">Wybierz **OK** toocreate hello akcji grupy.</span><span class="sxs-lookup"><span data-stu-id="bda24-136">Select **OK** toocreate hello action group.</span></span>

## <a name="manage-your-action-groups"></a><span data-ttu-id="bda24-137">Zarządzanie grupami akcji</span><span class="sxs-lookup"><span data-stu-id="bda24-137">Manage your action groups</span></span> ##
<span data-ttu-id="bda24-138">Po utworzeniu grupy akcji nie jest widoczna hello **grupy akcji** sekcji hello **Monitor** bloku.</span><span class="sxs-lookup"><span data-stu-id="bda24-138">After you create an action group, it's visible in hello **Action groups** section of hello **Monitor** blade.</span></span> <span data-ttu-id="bda24-139">Wybierz grupę akcji hello, który ma toomanage do:</span><span class="sxs-lookup"><span data-stu-id="bda24-139">Select hello action group you want toomanage to:</span></span>

* <span data-ttu-id="bda24-140">Dodawanie, edytowanie lub usuwanie akcji.</span><span class="sxs-lookup"><span data-stu-id="bda24-140">Add, edit, or remove actions.</span></span>
* <span data-ttu-id="bda24-141">Usuwanie grupy akcji hello.</span><span class="sxs-lookup"><span data-stu-id="bda24-141">Delete hello action group.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bda24-142">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="bda24-142">Next steps</span></span> ##
* <span data-ttu-id="bda24-143">Dowiedz się więcej o [SMS alertów zachowanie](monitoring-sms-alert-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="bda24-143">Learn more about [SMS alert behavior](monitoring-sms-alert-behavior.md).</span></span>  
* <span data-ttu-id="bda24-144">Uzyskaj [zrozumienia schemat alertu elementu webhook dziennika aktywności hello](monitoring-activity-log-alerts-webhook.md).</span><span class="sxs-lookup"><span data-stu-id="bda24-144">Gain an [understanding of hello activity log alert webhook schema](monitoring-activity-log-alerts-webhook.md).</span></span>  
* <span data-ttu-id="bda24-145">Dowiedz się więcej o [limitów szybkości](monitoring-alerts-rate-limiting.md) alertów.</span><span class="sxs-lookup"><span data-stu-id="bda24-145">Learn more about [rate limiting](monitoring-alerts-rate-limiting.md) on alerts.</span></span> 
* <span data-ttu-id="bda24-146">Pobierz [Przegląd alertów dotyczących działań w dzienniku](monitoring-overview-alerts.md)i Dowiedz się, jak tooreceive alertów.</span><span class="sxs-lookup"><span data-stu-id="bda24-146">Get an [overview of activity log alerts](monitoring-overview-alerts.md), and learn how tooreceive alerts.</span></span>  
* <span data-ttu-id="bda24-147">Dowiedz się, jak za[skonfigurować alerty, gdy powiadomienie usługi kondycji jest przesyłana](monitoring-activity-log-alerts-on-service-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="bda24-147">Learn how too[configure alerts whenever a service health notification is posted](monitoring-activity-log-alerts-on-service-notifications.md).</span></span>
