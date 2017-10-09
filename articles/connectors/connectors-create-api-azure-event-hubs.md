---
title: "aaaSet Monitor zdarzeń w usłudze Azure Event Hubs dla usługi Azure Logic Apps | Dokumentacja firmy Microsoft"
description: "Monitorowanie zdarzeń tooreceive strumieni danych i wysyłania zdarzeń dla usługi Azure Logic Apps w usłudze Azure Event Hubs"
services: logic-apps
keywords: "strumień danych, monitor zdarzeń, usługa event hubs"
author: ecfan
manager: anneta
editor: 
documentationcenter: 
tags: connectors
ms.assetid: 
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/31/2017
ms.author: estfan; LADocs
ms.openlocfilehash: 4aad2c2ac1134b4d4d440019b4773559e49be122
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-receive-and-send-events-with-hello-event-hubs-connector"></a><span data-ttu-id="901ad-104">Monitorowanie, odbierania i wysyłania zdarzeń z łącznikiem usługi Event Hubs hello</span><span class="sxs-lookup"><span data-stu-id="901ad-104">Monitor, receive, and send events with hello Event Hubs connector</span></span>

<span data-ttu-id="901ad-105">tooset Monitor zdarzeń, aby aplikację logiki można wykrywać zdarzenia, zdarzenia są rejestrowane i wysyłać zdarzenia, Połącz tooan [Azure Event Hub](https://azure.microsoft.com/services/event-hubs) z aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="901ad-105">tooset up an event monitor so that your logic app can detect events, receive events, and send events, connect tooan [Azure Event Hub](https://azure.microsoft.com/services/event-hubs) from your logic app.</span></span> <span data-ttu-id="901ad-106">Dowiedz się więcej o [Azure Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md).</span><span class="sxs-lookup"><span data-stu-id="901ad-106">Learn more about [Azure Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md).</span></span>

## <a name="requirements"></a><span data-ttu-id="901ad-107">Wymagania</span><span class="sxs-lookup"><span data-stu-id="901ad-107">Requirements</span></span>

* <span data-ttu-id="901ad-108">Masz toohave [centra zdarzeń w przestrzeni nazw i Centrum zdarzeń](../event-hubs/event-hubs-create.md) na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="901ad-108">You have toohave an [Event Hubs namespace and Event Hub](../event-hubs/event-hubs-create.md) in Azure.</span></span> <span data-ttu-id="901ad-109">Dowiedz się [jak toocreate centra zdarzeń w przestrzeni nazw i Centrum zdarzeń](../event-hubs/event-hubs-create.md).</span><span class="sxs-lookup"><span data-stu-id="901ad-109">Learn [how toocreate an Event Hubs namespace and Event Hub](../event-hubs/event-hubs-create.md).</span></span> 

* <span data-ttu-id="901ad-110">toouse [każdy łącznik](https://docs.microsoft.com/azure/connectors/apis-list) w aplikacji logiki, masz toocreate aplikacji logiki najpierw.</span><span class="sxs-lookup"><span data-stu-id="901ad-110">toouse [any connector](https://docs.microsoft.com/azure/connectors/apis-list) in your logic app, you have toocreate a logic app first.</span></span> <span data-ttu-id="901ad-111">Dowiedz się [jak toocreate aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="901ad-111">Learn [how toocreate a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

<a name="permissions-connection-string"></a>
## <a name="check-event-hubs-namespace-permissions-and-find-hello-connection-string"></a><span data-ttu-id="901ad-112">Sprawdź uprawnienia przestrzeni nazw usługi Event Hubs i Znajdź parametry połączenia hello</span><span class="sxs-lookup"><span data-stu-id="901ad-112">Check Event Hubs namespace permissions and find hello connection string</span></span>

<span data-ttu-id="901ad-113">Dla Twojego tooaccess aplikacji logiki dowolnej usługi, masz toocreate [ *połączenia* ](./connectors-overview.md) między logiki aplikacji i hello usługi, jeśli nie jest jeszcze.</span><span class="sxs-lookup"><span data-stu-id="901ad-113">For your logic app tooaccess any service, you have toocreate a [*connection*](./connectors-overview.md) between your logic app and hello service, if you haven't already.</span></span> <span data-ttu-id="901ad-114">To połączenie autoryzuje danych tooaccess aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="901ad-114">This connection authorizes your logic app tooaccess data.</span></span>
<span data-ttu-id="901ad-115">Dla Twojego tooaccess aplikacji logiki Centrum zdarzeń, masz toohave **Zarządzaj** uprawnienia i hello parametry połączenia dla przestrzeni nazw usługi Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="901ad-115">For your logic app tooaccess your Event Hub, you have toohave **Manage** permissions and hello connection string for your Event Hubs namespace.</span></span>

<span data-ttu-id="901ad-116">toocheck swoje uprawnienia i get hello parametrów połączenia, wykonaj następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="901ad-116">toocheck your permissions and get hello connection string, follow these steps.</span></span>

1.  <span data-ttu-id="901ad-117">Zaloguj się toohello [portalu Azure](https://portal.azure.com "portalu Azure").</span><span class="sxs-lookup"><span data-stu-id="901ad-117">Sign in toohello [Azure portal](https://portal.azure.com "Azure portal").</span></span> 

2.  <span data-ttu-id="901ad-118">Przejdź do usługi Event Hubs tooyour *przestrzeni nazw*, nie hello określonym Centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="901ad-118">Go tooyour Event Hubs *namespace*, not hello specific Event Hub.</span></span> <span data-ttu-id="901ad-119">W bloku przestrzeni nazw hello w obszarze **ustawienia**, wybierz **zasady dostępu współużytkowanego**.</span><span class="sxs-lookup"><span data-stu-id="901ad-119">On hello namespace blade, under **Settings**, choose **Shared access policies**.</span></span> <span data-ttu-id="901ad-120">W obszarze **oświadczeń**, sprawdź, czy masz **Zarządzaj** uprawnienia dla tej przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="901ad-120">Under **Claims**, check that you have **Manage** permissions for that namespace.</span></span>

    ![Zarządzaj uprawnieniami dla przestrzeni nazw Centrum zdarzeń](./media/connectors-create-api-azure-event-hubs/event-hubs-namespace.png)

3.  <span data-ttu-id="901ad-122">Wybierz parametry połączenia hello toocopy dla przestrzeni nazw usługi Event Hubs hello **RootManageSharedAccessKey**.</span><span class="sxs-lookup"><span data-stu-id="901ad-122">toocopy hello connection string for hello Event Hubs namespace, choose **RootManageSharedAccessKey**.</span></span> <span data-ttu-id="901ad-123">Następny tooyour podstawowego klucza parametry połączenia, kliknij przycisk Kopiuj hello.</span><span class="sxs-lookup"><span data-stu-id="901ad-123">Next tooyour primary key connection string, choose hello copy button.</span></span>

    ![Skopiuj parametry połączenia w przestrzeni nazw usługi Event Hubs](media/connectors-create-api-azure-event-hubs/find-event-hub-namespace-connection-string.png)

    > [!TIP]
    > <span data-ttu-id="901ad-125">tooconfirm czy ciąg połączenia jest skojarzony z przestrzeni nazw usługi Event Hubs lub z określonym Centrum zdarzeń, sprawdź ciąg połączenia hello hello `EntityPath` parametru.</span><span class="sxs-lookup"><span data-stu-id="901ad-125">tooconfirm whether your connection string is associated with your Event Hubs namespace or with a specific Event Hub, check hello connection string for hello `EntityPath` parameter.</span></span> <span data-ttu-id="901ad-126">Możesz znaleźć tego parametru, ciąg połączenia hello jest przeznaczony dla określonego Centrum zdarzeń "entity" i nie jest toouse poprawny ciąg hello z aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="901ad-126">If you find this parameter, hello connection string is for a specific Event Hub "entity", and is not hello correct string toouse with your logic app.</span></span>

4.  <span data-ttu-id="901ad-127">Teraz po wyświetleniu monitu o poświadczenia, po dodaniu usługi Event Hubs wyzwalacza lub akcji tooyour logikę aplikacji, możesz połączyć tooyour centra zdarzeń w przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="901ad-127">Now when you're prompted for credentials after adding an Event Hubs trigger or action tooyour logic app, you can connect tooyour Event Hubs namespace.</span></span> <span data-ttu-id="901ad-128">Nadaj nazwę połączenia, wprowadź parametry połączenia hello, który został skopiowany, a wybierz **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="901ad-128">Give your connection a name, enter hello connection string that you copied, and choose **Create**.</span></span>

    ![Wprowadź parametry połączenia dla przestrzeni nazw usługi Event Hubs](./media/connectors-create-api-azure-event-hubs/event-hubs-connection.png)

    <span data-ttu-id="901ad-130">Po utworzeniu połączenia, nazwa połączenia hello powinna pojawić się w wyzwalacza usługi Event Hubs hello lub akcji.</span><span class="sxs-lookup"><span data-stu-id="901ad-130">After you create your connection, hello connection name should appear in hello Event Hubs trigger or action.</span></span> 
    <span data-ttu-id="901ad-131">Następnie możesz nadal z hello inne czynności w aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="901ad-131">You can then continue with hello other steps in your logic app.</span></span>

    ![Połączenia nazw centra zdarzeń utworzony](./media/connectors-create-api-azure-event-hubs/event-hubs-connection-created.png)

## <a name="start-workflow-when-your-event-hub-receives-new-events"></a><span data-ttu-id="901ad-133">Uruchamianie przepływu pracy w Centrum zdarzeń odebrania nowych zdarzeń</span><span class="sxs-lookup"><span data-stu-id="901ad-133">Start workflow when your Event Hub receives new events</span></span>

<span data-ttu-id="901ad-134">A [ *wyzwalacza* ](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts) jest zdarzeniem, która uruchamia przepływ pracy w aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="901ad-134">A [*trigger*](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts) is an event that starts a workflow in your logic app.</span></span> <span data-ttu-id="901ad-135">Aby uruchomić przepływ pracy, gdy nowe zdarzenia są wysyłane tooyour Centrum zdarzeń, wykonaj następujące kroki dodawania hello wyzwalacz, który wykryje to zdarzenie.</span><span class="sxs-lookup"><span data-stu-id="901ad-135">To start a workflow when new events are sent tooyour Event Hub, follow these steps for adding hello trigger that detects this event.</span></span>

1.  <span data-ttu-id="901ad-136">W hello [portalu Azure](https://portal.azure.com "portalu Azure"), przejdź do istniejących aplikacji logiki tooyour lub tworzenie aplikacji logiki puste.</span><span class="sxs-lookup"><span data-stu-id="901ad-136">In hello [Azure portal](https://portal.azure.com "Azure portal"), go tooyour existing logic app or create a blank logic app.</span></span>

2.  <span data-ttu-id="901ad-137">W polu wyszukiwania hello na powitania projektanta aplikacji logiki, wprowadź `event hubs` filtru.</span><span class="sxs-lookup"><span data-stu-id="901ad-137">In hello search box for hello Logic App Designer, enter `event hubs` for your filter.</span></span> <span data-ttu-id="901ad-138">Wybierz ten wyzwalacz: **podczas zdarzenia są dostępne w Centrum zdarzeń**</span><span class="sxs-lookup"><span data-stu-id="901ad-138">Select this trigger: **When events are available in Event Hub**</span></span>

    ![Wybierz wyzwalacz po odbiera nowych zdarzeń w Centrum zdarzeń](./media/connectors-create-api-azure-event-hubs/find-event-hubs-trigger.png)

    <span data-ttu-id="901ad-140">Jeśli nie masz już przestrzeń nazw usługi Event Hubs tooyour połączenie, zostanie wyświetlony monit toocreate teraz tego połączenia.</span><span class="sxs-lookup"><span data-stu-id="901ad-140">If you don't already have a connection tooyour Event Hubs namespace, you're prompted toocreate this connection now.</span></span> <span data-ttu-id="901ad-141">Nadaj nazwę połączenia, a następnie wprowadź hello parametry połączenia dla przestrzeni nazw usługi Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="901ad-141">Give your connection a name, and enter hello connection string for your Event Hubs namespace.</span></span> 
    <span data-ttu-id="901ad-142">Dowiedz się, jeśli to konieczne, [jak toofind parametrów połączenia](#permissions-connection-string).</span><span class="sxs-lookup"><span data-stu-id="901ad-142">If necessary, learn [how toofind your connection string](#permissions-connection-string).</span></span>

    ![Wprowadź parametry połączenia dla przestrzeni nazw usługi Event Hubs](./media/connectors-create-api-azure-event-hubs/event-hubs-connection.png)

    <span data-ttu-id="901ad-144">Po utworzeniu połączenia hello hello ustawienia hello **podczas zdarzenia w dostępnych w Centrum zdarzeń** wyzwalacza są wyświetlane.</span><span class="sxs-lookup"><span data-stu-id="901ad-144">After you create hello connection, hello settings for hello **When an event in available in an Event Hub** trigger appear.</span></span>

    ![Ustawienia wyzwalacza po odbiera nowych zdarzeń w Centrum zdarzeń](./media/connectors-create-api-azure-event-hubs/event-hubs-trigger.png)

3.  <span data-ttu-id="901ad-146">Wprowadź lub wybierz nazwę hello hello Centrum zdarzeń, które mają toomonitor.</span><span class="sxs-lookup"><span data-stu-id="901ad-146">Enter or select hello name for hello Event Hub that you want toomonitor.</span></span> <span data-ttu-id="901ad-147">Wybierz hello częstotliwość i interwał częstotliwość hello toocheck Centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="901ad-147">Select hello frequency and interval for how often you want toocheck hello Event Hub.</span></span>

    > [!TIP]
    > <span data-ttu-id="901ad-148">toooptionally zaznacz grupy odbiorców do odczytywania zdarzeń, wybierz polecenie **Pokaż zaawansowane opcje**.</span><span class="sxs-lookup"><span data-stu-id="901ad-148">toooptionally select a consumer group for reading events, choose **Show advanced options**.</span></span> 

    ![Określ Centrum zdarzeń lub grupy odbiorców](./media/connectors-create-api-azure-event-hubs/event-hubs-trigger-details.png)

    <span data-ttu-id="901ad-150">Teraz skonfigurowaniu toostart wyzwalacz przepływu pracy aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="901ad-150">You've now set up a trigger toostart a workflow for your logic app.</span></span> 
    <span data-ttu-id="901ad-151">Aplikację logiki sprawdza, czy hello określony na podstawie harmonogramu hello, które można ustawić Centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="901ad-151">Your logic app checks hello specified Event Hub based on hello schedule that you set.</span></span> 
    <span data-ttu-id="901ad-152">Jeśli aplikacji znajdzie nowe zdarzenia w hello Centrum zdarzeń, wyzwalacz hello wykonuje inne operacje i wyzwalaczy aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="901ad-152">If your app finds new events in hello Event Hub, hello trigger runs other actions or triggers in your logic app.</span></span>

## <a name="send-events-tooyour-event-hub-from-your-logic-app"></a><span data-ttu-id="901ad-153">Wysyłanie zdarzeń tooyour Centrum zdarzeń z aplikacji logiki</span><span class="sxs-lookup"><span data-stu-id="901ad-153">Send events tooyour Event Hub from your logic app</span></span>

<span data-ttu-id="901ad-154">[*Akcja*](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts) to zadanie wykonywane przez przepływ pracy aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="901ad-154">An [*action*](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts) is a task performed by your logic app workflow.</span></span> <span data-ttu-id="901ad-155">Po dodaniu aplikacji logiki wyzwalacza tooyour, można dodać operacji tooperform akcji z danych wygenerowanych przez tego wyzwalacza.</span><span class="sxs-lookup"><span data-stu-id="901ad-155">After you add a trigger tooyour logic app, you can add an action tooperform operations with data generated by that trigger.</span></span> <span data-ttu-id="901ad-156">toosend tooyour zdarzeń Centrum zdarzeń z aplikacji logiki, wykonaj następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="901ad-156">toosend an event tooyour Event Hub from your logic app, follow these steps.</span></span>

1.  <span data-ttu-id="901ad-157">W Projektancie aplikacji logiki, zgodnie z wyzwalaczem aplikacji logiki, wybierz **nowy krok** > **Dodaj akcję**.</span><span class="sxs-lookup"><span data-stu-id="901ad-157">In Logic App Designer, under your logic app trigger, choose **New step** > **Add an action**.</span></span>

    ![Wybierz pozycję "Nowy krok", następnie "Dodaj akcję"](./media/connectors-create-api-azure-event-hubs/add-action.png)

    <span data-ttu-id="901ad-159">Teraz można znaleźć i wybrać tooperform akcji.</span><span class="sxs-lookup"><span data-stu-id="901ad-159">Now you can find and select an action tooperform.</span></span> 
    <span data-ttu-id="901ad-160">Chociaż można wybrać żadnych akcji, na przykład chcemy hello centra zdarzeń w akcji toosend zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="901ad-160">Although you can select any action, for this example, we want hello Event Hubs action toosend events.</span></span>

2.  <span data-ttu-id="901ad-161">W polu wyszukiwania hello, wprowadź `event hubs` filtru.</span><span class="sxs-lookup"><span data-stu-id="901ad-161">In hello search box, enter `event hubs` for your filter.</span></span>
<span data-ttu-id="901ad-162">Wybierz tę akcję: **wysyłania zdarzeń**</span><span class="sxs-lookup"><span data-stu-id="901ad-162">Select this action: **Send event**</span></span>

    ![Wybierz opcję "Event Hubs — wysyłanie zdarzeń" akcji](./media/connectors-create-api-azure-event-hubs/find-event-hubs-action.png)

3.  <span data-ttu-id="901ad-164">Wprowadź szczegóły hello wymagane dla hello zdarzenia, takie jak nazwa hello hello Centrum zdarzeń, w którym ma toosend hello zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="901ad-164">Enter hello required details for hello event, such as hello name for hello Event Hub where you want toosend hello event.</span></span> <span data-ttu-id="901ad-165">Wprowadź inne opcjonalne szczegóły dotyczące zdarzenia hello, takie jak zawartość dla tego zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="901ad-165">Enter any other optional details about hello event, such as content for that event.</span></span>

    > [!TIP]
    > <span data-ttu-id="901ad-166">toooptionally Określ hello partycji Centrum zdarzeń, gdy toosend hello zdarzenia, wybierz **Pokaż zaawansowane opcje**.</span><span class="sxs-lookup"><span data-stu-id="901ad-166">toooptionally specify hello Event Hub partition where toosend hello event, choose **Show advanced options**.</span></span> 

    ![Wprowadź nazwę Centrum zdarzeń i szczegóły zdarzenia opcjonalne](./media/connectors-create-api-azure-event-hubs/event-hubs-send-event-action.png)

6.  <span data-ttu-id="901ad-168">Zapisz zmiany.</span><span class="sxs-lookup"><span data-stu-id="901ad-168">Save your changes.</span></span>

    ![Zapisywanie aplikacji logiki](./media/connectors-create-api-azure-event-hubs/save-logic-app.png)

    <span data-ttu-id="901ad-170">Teraz skonfigurowaniu zdarzenia toosend akcji z aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="901ad-170">You've now set up an action toosend events from your logic app.</span></span> 

## <a name="connector-specific-details"></a><span data-ttu-id="901ad-171">Szczegóły dotyczące łącznika</span><span class="sxs-lookup"><span data-stu-id="901ad-171">Connector-specific details</span></span>

<span data-ttu-id="901ad-172">Wyświetl wszystkie wyzwalacze i akcje zdefiniowane w hello swagger i zobacz też żadnych limitów w hello [szczegóły łącznika](/connectors/eventhubs/).</span><span class="sxs-lookup"><span data-stu-id="901ad-172">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/eventhubs/).</span></span> 

## <a name="get-help"></a><span data-ttu-id="901ad-173">Uzyskiwanie pomocy</span><span class="sxs-lookup"><span data-stu-id="901ad-173">Get help</span></span>

<span data-ttu-id="901ad-174">pytania tooask, odpowiadanie na pytania i robią innych użytkowników usługi Azure Logic Apps, zobacz odwiedź hello [forum usługi Azure Logic Apps](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span><span class="sxs-lookup"><span data-stu-id="901ad-174">tooask questions, answer questions, and see what other Azure Logic Apps users are doing, visit hello [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>

<span data-ttu-id="901ad-175">toohelp poprawy Logic Apps i łącznikami, Zagłosuj lub Prześlij pomysłów na powitania [witrynę opinii użytkowników Logic Apps](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="901ad-175">toohelp improve Logic Apps and connectors, vote on or submit ideas at hello [Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="901ad-176">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="901ad-176">Next steps</span></span>

*  [<span data-ttu-id="901ad-177">Znajdź inne łączniki dla usługi Azure Logic apps</span><span class="sxs-lookup"><span data-stu-id="901ad-177">Find other connectors for Azure Logic apps</span></span>](./apis-list.md)