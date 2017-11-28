---
title: "Łącznik programu Outlook pakietu Office 365 hello aaaAdd w aplikacjach logiki | Dokumentacja firmy Microsoft"
description: "Tworzenie aplikacji logiki z usługi Office 365 łącznika tooenable interakcji z usługą Office 365. Na przykład: tworzenie, edytowanie i aktualizowanie kontakty i elementy kalendarza."
services: 
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: b2f6cc2c-bba2-493a-b0ba-841785462a80
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 10/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 86a573c9c54701de3d3f0500d19eaf545e0710ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-office-365-outlook-connector"></a><span data-ttu-id="b1b28-104">Rozpoczynanie pracy z hello łącznika programu Outlook pakietu Office 365</span><span class="sxs-lookup"><span data-stu-id="b1b28-104">Get started with hello Office 365 Outlook connector</span></span>
<span data-ttu-id="b1b28-105">Łącznik programu Outlook pakietu Office 365 Hello umożliwia interakcję z programu Outlook w usłudze Office 365.</span><span class="sxs-lookup"><span data-stu-id="b1b28-105">hello Office 365 Outlook connector enables interaction with Outlook in Office 365.</span></span> <span data-ttu-id="b1b28-106">Użyj tego łącznika toocreate, edycji i kontakty aktualizacji i elementy kalendarza i również get, wysyłania i Odpowiedz tooemail.</span><span class="sxs-lookup"><span data-stu-id="b1b28-106">Use this connector toocreate, edit, and update contacts and calendar items, and also get, send, and reply tooemail.</span></span>

<span data-ttu-id="b1b28-107">W programie Outlook pakietu Office 365 możesz:</span><span class="sxs-lookup"><span data-stu-id="b1b28-107">With Office 365 Outlook, you:</span></span>

* <span data-ttu-id="b1b28-108">Tworzenie przepływu pracy przy użyciu funkcji poczty e-mail i kalendarza hello w ramach usługi Office 365.</span><span class="sxs-lookup"><span data-stu-id="b1b28-108">Build your workflow using hello email and calendar features within Office 365.</span></span> 
* <span data-ttu-id="b1b28-109">Użyj wyzwala toostart do przepływu pracy, gdy istnieje nową wiadomość e-mail po zaktualizowaniu elementu kalendarza i inne.</span><span class="sxs-lookup"><span data-stu-id="b1b28-109">Use triggers toostart your workflow when there is a new email, when a calendar item is updated, and more.</span></span>
* <span data-ttu-id="b1b28-110">Użyj akcji toosend wiadomości e-mail, Utwórz nowe zdarzenie kalendarza i inne.</span><span class="sxs-lookup"><span data-stu-id="b1b28-110">Use actions toosend an email, create a new calendar event, and more.</span></span> <span data-ttu-id="b1b28-111">Na przykład, jeśli jest nowy obiekt w usłudze Salesforce (wyzwalacz), Wyślij wiadomość e-mail tooyour programu Outlook pakietu Office 365 (działanie).</span><span class="sxs-lookup"><span data-stu-id="b1b28-111">For example, when there is a new object in Salesforce (a trigger), send an email tooyour Office 365 Outlook (an action).</span></span> 

<span data-ttu-id="b1b28-112">W tym temacie pokazano, jak toouse hello łącznika programu Outlook pakietu Office 365 w aplikacji logiki, a także list hello wyzwalacze i akcje.</span><span class="sxs-lookup"><span data-stu-id="b1b28-112">This topic shows you how toouse hello Office 365 Outlook connector in a logic app, and also lists hello triggers and actions.</span></span>

> [!NOTE]
> <span data-ttu-id="b1b28-113">Ta wersja artykułu hello ma zastosowanie tooLogic aplikacji ogólnodostępnej (GA).</span><span class="sxs-lookup"><span data-stu-id="b1b28-113">This version of hello article applies tooLogic Apps general availability (GA).</span></span>
> 
> 

<span data-ttu-id="b1b28-114">toolearn więcej informacji na temat aplikacji logiki, zobacz [co to jest logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) i [tworzenie aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="b1b28-114">toolearn more about Logic Apps, see [What are logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-toooffice-365"></a><span data-ttu-id="b1b28-115">Połącz tooOffice 365</span><span class="sxs-lookup"><span data-stu-id="b1b28-115">Connect tooOffice 365</span></span>
<span data-ttu-id="b1b28-116">Zanim aplikację logiki można uzyskać dostęp do dowolnej usługi, należy najpierw utworzyć *połączenia* toohello usługi.</span><span class="sxs-lookup"><span data-stu-id="b1b28-116">Before your logic app can access any service, you first create a *connection* toohello service.</span></span> <span data-ttu-id="b1b28-117">Połączenie stanowi połączenie między aplikacji logiki i innej usługi.</span><span class="sxs-lookup"><span data-stu-id="b1b28-117">A connection provides connectivity between a logic app and another service.</span></span> <span data-ttu-id="b1b28-118">Na przykład tooconnect tooOffice 365 programu Outlook, należy najpierw usługi Office 365 *połączenia*.</span><span class="sxs-lookup"><span data-stu-id="b1b28-118">For example, tooconnect tooOffice 365 Outlook, you first need an Office 365 *connection*.</span></span> <span data-ttu-id="b1b28-119">toocreate połączenie, wprowadź poświadczenia hello tooaccess hello usługi, które mają tooconnect do zwykle jest używana.</span><span class="sxs-lookup"><span data-stu-id="b1b28-119">toocreate a connection, enter hello credentials you normally use tooaccess hello service you wish tooconnect to.</span></span> <span data-ttu-id="b1b28-120">Dlatego w programie Outlook pakietu Office 365 należy wprowadzić hello poświadczenia tooyour połączenia hello toocreate konta usługi Office 365.</span><span class="sxs-lookup"><span data-stu-id="b1b28-120">So with Office 365 Outlook, enter hello credentials tooyour Office 365 account toocreate hello connection.</span></span>

## <a name="create-hello-connection"></a><span data-ttu-id="b1b28-121">Utwórz połączenie hello</span><span class="sxs-lookup"><span data-stu-id="b1b28-121">Create hello connection</span></span>
> [!INCLUDE [Steps toocreate a connection tooOffice 365](../../includes/connectors-create-api-office365-outlook.md)]
> 
> 

## <a name="use-a-trigger"></a><span data-ttu-id="b1b28-122">Użyć wyzwalacza</span><span class="sxs-lookup"><span data-stu-id="b1b28-122">Use a trigger</span></span>
<span data-ttu-id="b1b28-123">Wyzwalacz jest zdarzenie, które mogą być zdefiniowane w aplikacji logiki hello toostart używane w przepływie pracy.</span><span class="sxs-lookup"><span data-stu-id="b1b28-123">A trigger is an event that can be used toostart hello workflow defined in a logic app.</span></span> <span data-ttu-id="b1b28-124">Wyzwalacze "sondować" hello usługi interwału i częstotliwość.</span><span class="sxs-lookup"><span data-stu-id="b1b28-124">Triggers "poll" hello service at an interval and frequency that you want.</span></span> <span data-ttu-id="b1b28-125">[Dowiedz się więcej o wyzwalaczy](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="b1b28-125">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

1. <span data-ttu-id="b1b28-126">W aplikacji logiki hello wpisz "office 365" tooget listę hello wyzwalaczy:</span><span class="sxs-lookup"><span data-stu-id="b1b28-126">In hello logic app, type "office 365" tooget a list of hello triggers:</span></span>  
   
    ![](./media/connectors-create-api-office365-outlook/office365-trigger.png)
2. <span data-ttu-id="b1b28-127">Wybierz **Office 365 Outlook - wkrótce uruchamiając zdarzeń nadchodzących**.</span><span class="sxs-lookup"><span data-stu-id="b1b28-127">Select **Office 365 Outlook - When an upcoming event is starting soon**.</span></span> <span data-ttu-id="b1b28-128">Jeśli połączenie już istnieje, wybierz kalendarz, z listy rozwijanej hello.</span><span class="sxs-lookup"><span data-stu-id="b1b28-128">If a connection already exists, then select a calendar from hello drop-down list.</span></span>
   
    ![](./media/connectors-create-api-office365-outlook/sample-calendar.png)
   
    <span data-ttu-id="b1b28-129">Jeśli zostanie wyświetlony monit o toosign w, wprowadź znak hello szczegóły toocreate hello połączenia.</span><span class="sxs-lookup"><span data-stu-id="b1b28-129">If you are prompted toosign in, then enter hello sign in details toocreate hello connection.</span></span> <span data-ttu-id="b1b28-130">[Utwórz połączenie hello](connectors-create-api-office365-outlook.md#create-the-connection) w tym temacie przedstawiono kroki hello.</span><span class="sxs-lookup"><span data-stu-id="b1b28-130">[Create hello connection](connectors-create-api-office365-outlook.md#create-the-connection) in this topic lists hello steps.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="b1b28-131">W tym przykładzie aplikacji logiki hello jest uruchamiana po zaktualizowaniu zdarzenia kalendarza.</span><span class="sxs-lookup"><span data-stu-id="b1b28-131">In this example, hello logic app runs when a calendar event is updated.</span></span> <span data-ttu-id="b1b28-132">wyniki hello toosee tego wyzwalacza, Dodaj inną akcję, która wysyła do Ciebie wiadomość SMS.</span><span class="sxs-lookup"><span data-stu-id="b1b28-132">toosee hello results of this trigger, add another action that sends you a text message.</span></span> <span data-ttu-id="b1b28-133">Na przykład dodać hello usługi Twilio *wysyła komunikat* akcję, która teksty podczas hello kalendarza zdarzeń jest uruchamiana w ciągu 15 minut.</span><span class="sxs-lookup"><span data-stu-id="b1b28-133">For example, add hello Twilio *Send message* action that texts you when hello calendar event is starting in 15 minutes.</span></span> 
   > 
   > 
3. <span data-ttu-id="b1b28-134">Wybierz hello **Edytuj** przycisk i ustaw hello **częstotliwość** i **interwał** wartości.</span><span class="sxs-lookup"><span data-stu-id="b1b28-134">Select hello **Edit** button and set hello **Frequency** and **Interval** values.</span></span> <span data-ttu-id="b1b28-135">Na przykład, jeśli chcesz toopoll wyzwalacza hello co 15 minut, następnie ustawić hello **częstotliwość** za**minutę**i ustaw hello **interwał** zbyt**15**.</span><span class="sxs-lookup"><span data-stu-id="b1b28-135">For example, if you want hello trigger toopoll every 15 minutes, then set hello **Frequency** too**Minute**, and set hello **Interval** too**15**.</span></span> 
   
    ![](./media/connectors-create-api-office365-outlook/calendar-settings.png)
4. <span data-ttu-id="b1b28-136">**Zapisz** zmiany (lewym górnym rogu paska narzędzi hello).</span><span class="sxs-lookup"><span data-stu-id="b1b28-136">**Save** your changes (top left corner of hello toolbar).</span></span> <span data-ttu-id="b1b28-137">Aplikację logiki jest zapisywana i automatycznie włączone.</span><span class="sxs-lookup"><span data-stu-id="b1b28-137">Your logic app is saved and may be automatically enabled.</span></span>

## <a name="use-an-action"></a><span data-ttu-id="b1b28-138">Za pomocą akcji</span><span class="sxs-lookup"><span data-stu-id="b1b28-138">Use an action</span></span>
<span data-ttu-id="b1b28-139">Akcja jest wykonywane przez przepływ pracy hello zdefiniowanych w aplikacji logiki operacji.</span><span class="sxs-lookup"><span data-stu-id="b1b28-139">An action is an operation carried out by hello workflow defined in a logic app.</span></span> <span data-ttu-id="b1b28-140">[Dowiedz się więcej o akcjach](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="b1b28-140">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

1. <span data-ttu-id="b1b28-141">Wybierz znak plus hello.</span><span class="sxs-lookup"><span data-stu-id="b1b28-141">Select hello plus sign.</span></span> <span data-ttu-id="b1b28-142">Zobacz kilka opcji: **Dodaj akcję**, **Dodaj warunek**, lub jeden z hello **więcej** opcje.</span><span class="sxs-lookup"><span data-stu-id="b1b28-142">You see several choices: **Add an action**, **Add a condition**, or one of hello **More** options.</span></span>
   
    ![](./media/connectors-create-api-office365-outlook/add-action.png)
2. <span data-ttu-id="b1b28-143">Wybierz **Dodaj akcję**.</span><span class="sxs-lookup"><span data-stu-id="b1b28-143">Choose **Add an action**.</span></span>
3. <span data-ttu-id="b1b28-144">W polu tekstowym hello wpisz "office 365" tooget listę wszystkich hello dostępne akcje.</span><span class="sxs-lookup"><span data-stu-id="b1b28-144">In hello text box, type “office 365” tooget a list of all hello available actions.</span></span>
   
    ![](./media/connectors-create-api-office365-outlook/office365-actions.png) 
4. <span data-ttu-id="b1b28-145">W tym przykładzie wybierz **Office 365 Outlook - Tworzenie kontaktu**.</span><span class="sxs-lookup"><span data-stu-id="b1b28-145">In our example, choose **Office 365 Outlook - Create contact**.</span></span> <span data-ttu-id="b1b28-146">Jeśli połączenie już istnieje, a następnie wybierz hello **identyfikator folderu**, **imię**i inne właściwości:</span><span class="sxs-lookup"><span data-stu-id="b1b28-146">If a connection already exists, then choose hello **Folder ID**, **Given Name**, and other properties:</span></span>  
   
    ![](./media/connectors-create-api-office365-outlook/office365-sampleaction.png)
   
    <span data-ttu-id="b1b28-147">Jeśli zostanie wyświetlony monit o informacje o połączeniu hello, wprowadź hello szczegóły toocreate hello połączenia.</span><span class="sxs-lookup"><span data-stu-id="b1b28-147">If you are prompted for hello connection information, then enter hello details toocreate hello connection.</span></span> <span data-ttu-id="b1b28-148">[Utwórz połączenie hello](connectors-create-api-office365-outlook.md#create-the-connection) w tym temacie opisano te właściwości.</span><span class="sxs-lookup"><span data-stu-id="b1b28-148">[Create hello connection](connectors-create-api-office365-outlook.md#create-the-connection) in this topic describes these properties.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="b1b28-149">W tym przykładzie utworzymy nowy kontakt w programie Outlook pakietu Office 365.</span><span class="sxs-lookup"><span data-stu-id="b1b28-149">In this example, we create a new contact in Office 365 Outlook.</span></span> <span data-ttu-id="b1b28-150">Można użyć danych wyjściowych z innego kontaktu hello toocreate wyzwalacza.</span><span class="sxs-lookup"><span data-stu-id="b1b28-150">You can use output from another trigger toocreate hello contact.</span></span> <span data-ttu-id="b1b28-151">Na przykład dodać hello SalesForce *podczas tworzenia obiektu* wyzwalacza.</span><span class="sxs-lookup"><span data-stu-id="b1b28-151">For example, add hello SalesForce *When an object is created* trigger.</span></span> <span data-ttu-id="b1b28-152">Następnie dodaj hello Office 365 Outlook *utworzenie kontaktu* akcję, która używa hello SalesForce pola toocreate hello nowe miejsce nowego kontaktu w usłudze Office 365.</span><span class="sxs-lookup"><span data-stu-id="b1b28-152">Then add hello Office 365 Outlook *Create contact* action that uses hello SalesForce fields toocreate hello new new contact in Office 365.</span></span> 
   > 
   > 
5. <span data-ttu-id="b1b28-153">**Zapisz** zmiany (lewym górnym rogu paska narzędzi hello).</span><span class="sxs-lookup"><span data-stu-id="b1b28-153">**Save** your changes (top left corner of hello toolbar).</span></span> <span data-ttu-id="b1b28-154">Aplikację logiki jest zapisywana i automatycznie włączone.</span><span class="sxs-lookup"><span data-stu-id="b1b28-154">Your logic app is saved and may be automatically enabled.</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="b1b28-155">Szczegóły dotyczące łącznika</span><span class="sxs-lookup"><span data-stu-id="b1b28-155">Connector-specific details</span></span>

<span data-ttu-id="b1b28-156">Wyświetl wszystkie wyzwalacze i akcje zdefiniowane w hello swagger i zobacz też żadnych limitów w hello [szczegóły łącznika](/connectors/office365connector/).</span><span class="sxs-lookup"><span data-stu-id="b1b28-156">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/office365connector/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="b1b28-157">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b1b28-157">Next Steps</span></span>
<span data-ttu-id="b1b28-158">[Tworzenie aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="b1b28-158">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="b1b28-159">Eksploruj hello innych dostępnych łączników w aplikacjach logiki w naszym [listy interfejsów API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="b1b28-159">Explore hello other available connectors in Logic Apps at our [APIs list](apis-list.md).</span></span>

