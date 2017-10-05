---
title: "Dodaj łącznik programu Outlook pakietu Office 365 w aplikacji logiki | Dokumentacja firmy Microsoft"
description: "Tworzenie aplikacji logiki z łącznikiem usługi Office 365, aby umożliwić interakcję z usługą Office 365. Na przykład: tworzenie, edytowanie i aktualizowanie kontakty i elementy kalendarza."
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
ms.openlocfilehash: 5335dae62e61659b68e8befb4ed0d404dffb800c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-office-365-outlook-connector"></a><span data-ttu-id="72736-104">Rozpoczynanie pracy z łącznika programu Outlook pakietu Office 365</span><span class="sxs-lookup"><span data-stu-id="72736-104">Get started with the Office 365 Outlook connector</span></span>
<span data-ttu-id="72736-105">Łącznik programu Outlook pakietu Office 365 umożliwia interakcję z programu Outlook w usłudze Office 365.</span><span class="sxs-lookup"><span data-stu-id="72736-105">The Office 365 Outlook connector enables interaction with Outlook in Office 365.</span></span> <span data-ttu-id="72736-106">Używaj tego łącznika do tworzenia, edycji i zaktualizuj kontakty i elementy kalendarza i również uzyskać, wysyłania i Odpowiedz na wiadomość e-mail.</span><span class="sxs-lookup"><span data-stu-id="72736-106">Use this connector to create, edit, and update contacts and calendar items, and also get, send, and reply to email.</span></span>

<span data-ttu-id="72736-107">W programie Outlook pakietu Office 365 możesz:</span><span class="sxs-lookup"><span data-stu-id="72736-107">With Office 365 Outlook, you:</span></span>

* <span data-ttu-id="72736-108">Tworzenie przepływu pracy przy użyciu funkcji poczty e-mail i kalendarza w ramach usługi Office 365.</span><span class="sxs-lookup"><span data-stu-id="72736-108">Build your workflow using the email and calendar features within Office 365.</span></span> 
* <span data-ttu-id="72736-109">Wyzwalacze są używane do uruchomienia przepływu pracy po nowej wiadomości e-mail, po zaktualizowaniu elementu kalendarza i inne.</span><span class="sxs-lookup"><span data-stu-id="72736-109">Use triggers to start your workflow when there is a new email, when a calendar item is updated, and more.</span></span>
* <span data-ttu-id="72736-110">Użyj akcji, aby wysłać wiadomość e-mail, należy utworzyć nowe zdarzenie kalendarza i inne.</span><span class="sxs-lookup"><span data-stu-id="72736-110">Use actions to send an email, create a new calendar event, and more.</span></span> <span data-ttu-id="72736-111">Na przykład jeśli jest nowy obiekt w usłudze Salesforce (wyzwalacz), należy wysłać wiadomość e-mail programu Office 365 Outlook (działanie).</span><span class="sxs-lookup"><span data-stu-id="72736-111">For example, when there is a new object in Salesforce (a trigger), send an email to your Office 365 Outlook (an action).</span></span> 

<span data-ttu-id="72736-112">W tym temacie opisano sposób korzystania z łącznika programu Outlook pakietu Office 365 w aplikacji logiki, a także wyświetla wyzwalacze i akcje.</span><span class="sxs-lookup"><span data-stu-id="72736-112">This topic shows you how to use the Office 365 Outlook connector in a logic app, and also lists the triggers and actions.</span></span>

> [!NOTE]
> <span data-ttu-id="72736-113">Ta wersja artykułu ma zastosowanie do aplikacji logiki ogólnodostępnej (GA).</span><span class="sxs-lookup"><span data-stu-id="72736-113">This version of the article applies to Logic Apps general availability (GA).</span></span>
> 
> 

<span data-ttu-id="72736-114">Aby dowiedzieć się więcej na temat aplikacji logiki, zobacz [co to jest logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) i [tworzenie aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="72736-114">To learn more about Logic Apps, see [What are logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-to-office-365"></a><span data-ttu-id="72736-115">Łączenie z usługą Office 365</span><span class="sxs-lookup"><span data-stu-id="72736-115">Connect to Office 365</span></span>
<span data-ttu-id="72736-116">Zanim aplikację logiki można uzyskać dostęp do dowolnej usługi, należy najpierw utworzyć *połączenia* do usługi.</span><span class="sxs-lookup"><span data-stu-id="72736-116">Before your logic app can access any service, you first create a *connection* to the service.</span></span> <span data-ttu-id="72736-117">Połączenie stanowi połączenie między aplikacji logiki i innej usługi.</span><span class="sxs-lookup"><span data-stu-id="72736-117">A connection provides connectivity between a logic app and another service.</span></span> <span data-ttu-id="72736-118">Na przykład, aby połączyć program Outlook pakietu Office 365, należy najpierw usługi Office 365 *połączenia*.</span><span class="sxs-lookup"><span data-stu-id="72736-118">For example, to connect to Office 365 Outlook, you first need an Office 365 *connection*.</span></span> <span data-ttu-id="72736-119">Aby utworzyć połączenie, wprowadź poświadczenia, zwykle używanego do uzyskania dostępu do usługi, który chcesz połączyć się z.</span><span class="sxs-lookup"><span data-stu-id="72736-119">To create a connection, enter the credentials you normally use to access the service you wish to connect to.</span></span> <span data-ttu-id="72736-120">Dlatego w programie Outlook pakietu Office 365 wprowadź poświadczenia konta usługi Office 365, aby utworzyć połączenie.</span><span class="sxs-lookup"><span data-stu-id="72736-120">So with Office 365 Outlook, enter the credentials to your Office 365 account to create the connection.</span></span>

## <a name="create-the-connection"></a><span data-ttu-id="72736-121">Tworzenie połączenia</span><span class="sxs-lookup"><span data-stu-id="72736-121">Create the connection</span></span>
> [!INCLUDE [Steps to create a connection to Office 365](../../includes/connectors-create-api-office365-outlook.md)]
> 
> 

## <a name="use-a-trigger"></a><span data-ttu-id="72736-122">Użyć wyzwalacza</span><span class="sxs-lookup"><span data-stu-id="72736-122">Use a trigger</span></span>
<span data-ttu-id="72736-123">Wyzwalacz to zdarzenie służy do uruchomienia przepływu pracy zdefiniowanych w aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="72736-123">A trigger is an event that can be used to start the workflow defined in a logic app.</span></span> <span data-ttu-id="72736-124">Wyzwalacze "sondować" Usługa interwału i częstotliwość.</span><span class="sxs-lookup"><span data-stu-id="72736-124">Triggers "poll" the service at an interval and frequency that you want.</span></span> <span data-ttu-id="72736-125">[Dowiedz się więcej o wyzwalaczy](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="72736-125">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

1. <span data-ttu-id="72736-126">W aplikacji logiki wpisz "office 365" Aby uzyskać listę wyzwalaczy:</span><span class="sxs-lookup"><span data-stu-id="72736-126">In the logic app, type "office 365" to get a list of the triggers:</span></span>  
   
    ![](./media/connectors-create-api-office365-outlook/office365-trigger.png)
2. <span data-ttu-id="72736-127">Wybierz **Office 365 Outlook - wkrótce uruchamiając zdarzeń nadchodzących**.</span><span class="sxs-lookup"><span data-stu-id="72736-127">Select **Office 365 Outlook - When an upcoming event is starting soon**.</span></span> <span data-ttu-id="72736-128">Jeśli połączenie już istnieje, wybierz kalendarz, z listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="72736-128">If a connection already exists, then select a calendar from the drop-down list.</span></span>
   
    ![](./media/connectors-create-api-office365-outlook/sample-calendar.png)
   
    <span data-ttu-id="72736-129">Po pojawieniu się zalogować, wprowadź znak w szczegóły, aby utworzyć połączenie.</span><span class="sxs-lookup"><span data-stu-id="72736-129">If you are prompted to sign in, then enter the sign in details to create the connection.</span></span> <span data-ttu-id="72736-130">[Utwórz połączenie](connectors-create-api-office365-outlook.md#create-the-connection) w tym temacie przedstawiono kroki.</span><span class="sxs-lookup"><span data-stu-id="72736-130">[Create the connection](connectors-create-api-office365-outlook.md#create-the-connection) in this topic lists the steps.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="72736-131">W tym przykładzie aplikacja logiki jest uruchamiana po zaktualizowaniu zdarzenia kalendarza.</span><span class="sxs-lookup"><span data-stu-id="72736-131">In this example, the logic app runs when a calendar event is updated.</span></span> <span data-ttu-id="72736-132">Aby wyświetlić wyniki tego wyzwalacza, Dodaj inną akcję wysyłanej wiadomości tekstowej.</span><span class="sxs-lookup"><span data-stu-id="72736-132">To see the results of this trigger, add another action that sends you a text message.</span></span> <span data-ttu-id="72736-133">Na przykład dodać usługi Twilio *wysyła komunikat* akcji tego teksty podczas zdarzenia kalendarza jest uruchamiana w ciągu 15 minut.</span><span class="sxs-lookup"><span data-stu-id="72736-133">For example, add the Twilio *Send message* action that texts you when the calendar event is starting in 15 minutes.</span></span> 
   > 
   > 
3. <span data-ttu-id="72736-134">Wybierz **Edytuj** przycisk i ustaw **częstotliwość** i **interwał** wartości.</span><span class="sxs-lookup"><span data-stu-id="72736-134">Select the **Edit** button and set the **Frequency** and **Interval** values.</span></span> <span data-ttu-id="72736-135">Na przykład, jeśli chcesz wyzwalacza do sondowania co 15 minut, następnie ustawić **częstotliwość** do **minutę**i ustaw **interwał** do **15**.</span><span class="sxs-lookup"><span data-stu-id="72736-135">For example, if you want the trigger to poll every 15 minutes, then set the **Frequency** to **Minute**, and set the **Interval** to **15**.</span></span> 
   
    ![](./media/connectors-create-api-office365-outlook/calendar-settings.png)
4. <span data-ttu-id="72736-136">**Zapisz** zmiany (lewym górnym rogu paska narzędzi).</span><span class="sxs-lookup"><span data-stu-id="72736-136">**Save** your changes (top left corner of the toolbar).</span></span> <span data-ttu-id="72736-137">Aplikację logiki jest zapisywana i automatycznie włączone.</span><span class="sxs-lookup"><span data-stu-id="72736-137">Your logic app is saved and may be automatically enabled.</span></span>

## <a name="use-an-action"></a><span data-ttu-id="72736-138">Za pomocą akcji</span><span class="sxs-lookup"><span data-stu-id="72736-138">Use an action</span></span>
<span data-ttu-id="72736-139">Akcja jest przeprowadzane przez przepływ pracy zdefiniowanych w aplikacji logiki operacji.</span><span class="sxs-lookup"><span data-stu-id="72736-139">An action is an operation carried out by the workflow defined in a logic app.</span></span> <span data-ttu-id="72736-140">[Dowiedz się więcej o akcjach](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="72736-140">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

1. <span data-ttu-id="72736-141">Wybierz znak plus.</span><span class="sxs-lookup"><span data-stu-id="72736-141">Select the plus sign.</span></span> <span data-ttu-id="72736-142">Zobacz kilka opcji: **Dodaj akcję**, **Dodaj warunek**, lub jeden z **więcej** opcje.</span><span class="sxs-lookup"><span data-stu-id="72736-142">You see several choices: **Add an action**, **Add a condition**, or one of the **More** options.</span></span>
   
    ![](./media/connectors-create-api-office365-outlook/add-action.png)
2. <span data-ttu-id="72736-143">Wybierz **Dodaj akcję**.</span><span class="sxs-lookup"><span data-stu-id="72736-143">Choose **Add an action**.</span></span>
3. <span data-ttu-id="72736-144">W polu tekstowym wpisz "office 365" Aby uzyskać listę dostępnych akcji.</span><span class="sxs-lookup"><span data-stu-id="72736-144">In the text box, type “office 365” to get a list of all the available actions.</span></span>
   
    ![](./media/connectors-create-api-office365-outlook/office365-actions.png) 
4. <span data-ttu-id="72736-145">W tym przykładzie wybierz **Office 365 Outlook - Tworzenie kontaktu**.</span><span class="sxs-lookup"><span data-stu-id="72736-145">In our example, choose **Office 365 Outlook - Create contact**.</span></span> <span data-ttu-id="72736-146">Jeśli połączenie już istnieje, należy wybrać **identyfikator folderu**, **imię**i inne właściwości:</span><span class="sxs-lookup"><span data-stu-id="72736-146">If a connection already exists, then choose the **Folder ID**, **Given Name**, and other properties:</span></span>  
   
    ![](./media/connectors-create-api-office365-outlook/office365-sampleaction.png)
   
    <span data-ttu-id="72736-147">Jeśli zostanie wyświetlony monit o informacje dotyczące połączenia, wprowadź szczegóły, aby utworzyć połączenie.</span><span class="sxs-lookup"><span data-stu-id="72736-147">If you are prompted for the connection information, then enter the details to create the connection.</span></span> <span data-ttu-id="72736-148">[Utwórz połączenie](connectors-create-api-office365-outlook.md#create-the-connection) w tym temacie opisano te właściwości.</span><span class="sxs-lookup"><span data-stu-id="72736-148">[Create the connection](connectors-create-api-office365-outlook.md#create-the-connection) in this topic describes these properties.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="72736-149">W tym przykładzie utworzymy nowy kontakt w programie Outlook pakietu Office 365.</span><span class="sxs-lookup"><span data-stu-id="72736-149">In this example, we create a new contact in Office 365 Outlook.</span></span> <span data-ttu-id="72736-150">Dane wyjściowe z innego wyzwalacza umożliwia utworzenie kontaktu.</span><span class="sxs-lookup"><span data-stu-id="72736-150">You can use output from another trigger to create the contact.</span></span> <span data-ttu-id="72736-151">Na przykład dodać usług SalesForce *podczas tworzenia obiektu* wyzwalacza.</span><span class="sxs-lookup"><span data-stu-id="72736-151">For example, add the SalesForce *When an object is created* trigger.</span></span> <span data-ttu-id="72736-152">Następnie dodaj Office 365 Outlook *utworzenie kontaktu* akcję, która używa pola SalesForce w celu utworzenia nowego nowy kontakt w usłudze Office 365.</span><span class="sxs-lookup"><span data-stu-id="72736-152">Then add the Office 365 Outlook *Create contact* action that uses the SalesForce fields to create the new new contact in Office 365.</span></span> 
   > 
   > 
5. <span data-ttu-id="72736-153">**Zapisz** zmiany (lewym górnym rogu paska narzędzi).</span><span class="sxs-lookup"><span data-stu-id="72736-153">**Save** your changes (top left corner of the toolbar).</span></span> <span data-ttu-id="72736-154">Aplikację logiki jest zapisywana i automatycznie włączone.</span><span class="sxs-lookup"><span data-stu-id="72736-154">Your logic app is saved and may be automatically enabled.</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="72736-155">Szczegóły dotyczące łącznika</span><span class="sxs-lookup"><span data-stu-id="72736-155">Connector-specific details</span></span>

<span data-ttu-id="72736-156">Wyświetl wszystkie wyzwalacze i akcje zdefiniowane w swagger i zobacz też żadnych limitów w [szczegóły łącznika](/connectors/office365connector/).</span><span class="sxs-lookup"><span data-stu-id="72736-156">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/office365connector/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="72736-157">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="72736-157">Next Steps</span></span>
<span data-ttu-id="72736-158">[Tworzenie aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="72736-158">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="72736-159">Eksploruj dostępnych łączników w aplikacjach logiki w naszym [listy interfejsów API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="72736-159">Explore the other available connectors in Logic Apps at our [APIs list](apis-list.md).</span></span>

