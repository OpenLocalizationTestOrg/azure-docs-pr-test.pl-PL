---
title: "Przykładowe akcji alertu elementu Webhook w OMS Log Analytics | Dokumentacja firmy Microsoft"
description: "Jedną z akcji można uruchomić w odpowiedzi na alert analizy dzienników jest * webhook *, dzięki czemu można wywołać procesu zewnętrznego przez pojedyncze żądanie HTTP. W tym artykule przedstawiono przykład tworzenia akcji elementu webhook w alercie analizy dzienników, przy użyciu zapas czasu."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 13c39f0f-fd3c-472d-8324-ddf7538be45e
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/27/2017
ms.author: bwren
ms.openlocfilehash: 55b66132f7ec5c26c0a7cac1ec0a5c403dbd1082
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-alert-webhook-action-in-oms-log-analytics-to-send-message-to-slack"></a><span data-ttu-id="fbc42-104">Utworzenie elementu webhook alertów w OMS analizy dzienników do wysyłania wiadomości zapas czasu</span><span class="sxs-lookup"><span data-stu-id="fbc42-104">Create an alert webhook action in OMS Log Analytics to send message to Slack</span></span>
<span data-ttu-id="fbc42-105">Jedną z akcji można uruchomić w odpowiedzi na [alert analizy dzienników](log-analytics-alerts.md) jest *webhook*, który umożliwia wywołanie procesu zewnętrznego przez pojedyncze żądanie HTTP.</span><span class="sxs-lookup"><span data-stu-id="fbc42-105">One of the actions you can run in response to a [Log Analytics alert](log-analytics-alerts.md) is a *webhook*, which allows you to invoke an external process through a single HTTP request.</span></span>  <span data-ttu-id="fbc42-106">Możesz przeczytać o szczegółach alertów i elementów webhook w [alertów w analizy dzienników](log-analytics-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="fbc42-106">You can read about details of alerts and webhooks in [Alerts in Log Analytics](log-analytics-alerts.md)</span></span>

<span data-ttu-id="fbc42-107">W tym artykule omówimy przykładem tworzenia akcji elementu webhook w przypadku wystąpienia alertu analizy dzienników przy użyciu zapas czasu, która jest usługą obsługi wiadomości.</span><span class="sxs-lookup"><span data-stu-id="fbc42-107">In this article, we’ll walk through an example of creating a webhook action in a Log Analytics alert using Slack which is a messaging service.</span></span>

> [!NOTE]
> <span data-ttu-id="fbc42-108">Musisz mieć konto Slack do ukończenia tego przykładu.</span><span class="sxs-lookup"><span data-stu-id="fbc42-108">You must have a Slack account to complete this sample.</span></span>  <span data-ttu-id="fbc42-109">Można założyć bezpłatne konto w [slack.com](http://slack.com).</span><span class="sxs-lookup"><span data-stu-id="fbc42-109">You can sign up for a free account at [slack.com](http://slack.com).</span></span>
> 
> 

## <a name="step-1---enable-webhooks-in-slack"></a><span data-ttu-id="fbc42-110">Krok 1 — elementów webhook Włącz w zapas czasu</span><span class="sxs-lookup"><span data-stu-id="fbc42-110">Step 1 - Enable webhooks in Slack</span></span>
1. <span data-ttu-id="fbc42-111">Zaloguj się do zapas czasu na [slack.com](http://slack.com).</span><span class="sxs-lookup"><span data-stu-id="fbc42-111">Sign in to Slack at [slack.com](http://slack.com).</span></span>
2. <span data-ttu-id="fbc42-112">Wybierz kanał w **kanałów** sekcji w okienku po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="fbc42-112">Select a channel in the **Channels** section in the left pane.</span></span>  <span data-ttu-id="fbc42-113">Jest to kanał, który będzie można wysłać wiadomości do.</span><span class="sxs-lookup"><span data-stu-id="fbc42-113">This is the channel that the message will be sent to.</span></span>  <span data-ttu-id="fbc42-114">Można wybrać jedną z kanałów domyślne takich jak **ogólne** lub **losowe**.</span><span class="sxs-lookup"><span data-stu-id="fbc42-114">You can select one of the default channels such as **general** or **random**.</span></span>  <span data-ttu-id="fbc42-115">W środowisku produkcyjnym, należy prawdopodobnie utworzyć kanał specjalne takie jak **criticalservicealerts**.</span><span class="sxs-lookup"><span data-stu-id="fbc42-115">In a production scenario, you would most likely create a special channel such as **criticalservicealerts**.</span></span> <br>
   
   ![Kanałach Slack](media/log-analytics-alerts-webhooks/oms-webhooks01.png)
3. <span data-ttu-id="fbc42-117">Kliknij przycisk **Dodawanie aplikacji lub niestandardowej integracji** można otworzyć katalogu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="fbc42-117">Click **Add an app or custom integration** to open the App Directory.</span></span>
4. <span data-ttu-id="fbc42-118">Typ *elementów webhook* w polu wyszukiwania, a następnie wybierz **przychodzące elementów Webhook**.</span><span class="sxs-lookup"><span data-stu-id="fbc42-118">Type *webhooks* into the search box and then select **Incoming WebHooks**.</span></span> <br>
   
   ![Kanałach Slack](media/log-analytics-alerts-webhooks/oms-webhooks02.png)
5. <span data-ttu-id="fbc42-120">Kliknij przycisk **zainstalować** obok swojej nazwy zespołu.</span><span class="sxs-lookup"><span data-stu-id="fbc42-120">Click **Install** next to your team name.</span></span>
6. <span data-ttu-id="fbc42-121">Kliknij przycisk **Dodaj konfigurację**.</span><span class="sxs-lookup"><span data-stu-id="fbc42-121">Click **Add Configuration**.</span></span>
7. <span data-ttu-id="fbc42-122">Wybierz kanał, który będzie w tym przykładzie, a następnie kliknij przycisk **integracji dodać przychodzące elementów Webhook**.</span><span class="sxs-lookup"><span data-stu-id="fbc42-122">Select the the channel that you're going to use for this example, and then click **Add Incoming WebHooks integration**.</span></span>  
8. <span data-ttu-id="fbc42-123">Kopiuj **adresu URL elementu Webhook**.</span><span class="sxs-lookup"><span data-stu-id="fbc42-123">Copy the **Webhook URL**.</span></span>  <span data-ttu-id="fbc42-124">Będzie można wklejane to w konfiguracji alertu.</span><span class="sxs-lookup"><span data-stu-id="fbc42-124">You'll be pasting this into the Alert configuration.</span></span> <br>
   
    ![Kanałach Slack](media/log-analytics-alerts-webhooks/oms-webhooks05.png)

## <a name="step-2---create-alert-rule-in-log-analytics"></a><span data-ttu-id="fbc42-126">Krok 2 — Tworzenie reguły alertu w analizy dzienników</span><span class="sxs-lookup"><span data-stu-id="fbc42-126">Step 2 - Create alert rule in Log Analytics</span></span>
1. <span data-ttu-id="fbc42-127">[Tworzenie reguły alertu](log-analytics-alerts.md) z następującymi ustawieniami.</span><span class="sxs-lookup"><span data-stu-id="fbc42-127">[Create an alert rule](log-analytics-alerts.md) with the following settings.</span></span>
   * <span data-ttu-id="fbc42-128">Zapytanie:```    Type=Event EventLevelName=error ```</span><span class="sxs-lookup"><span data-stu-id="fbc42-128">Query: ```    Type=Event EventLevelName=error ```</span></span>
   * <span data-ttu-id="fbc42-129">Sprawdź, czy ten alert co: 5 minut</span><span class="sxs-lookup"><span data-stu-id="fbc42-129">Check for this alert every: 5 minutes</span></span>
   * <span data-ttu-id="fbc42-130">Liczba wyników: większe niż 10</span><span class="sxs-lookup"><span data-stu-id="fbc42-130">The number of results is: greater than 10</span></span>
   * <span data-ttu-id="fbc42-131">W tym oknie: 60 minut</span><span class="sxs-lookup"><span data-stu-id="fbc42-131">Over this time window: 60 minutes</span></span>
   * <span data-ttu-id="fbc42-132">Wybierz **tak** dla **Webhook** i **nr** dla innych działań.</span><span class="sxs-lookup"><span data-stu-id="fbc42-132">Select **Yes** for **Webhook** and **No** for the other actions.</span></span>
2. <span data-ttu-id="fbc42-133">Wklej adres URL zapas czasu do **adresu URL elementu Webhook** pola.</span><span class="sxs-lookup"><span data-stu-id="fbc42-133">Paste the Slack URL into the **Webhook URL** field.</span></span>
3. <span data-ttu-id="fbc42-134">Wybierz opcję **Uwzględnij niestandardowy ładunek JSON**.</span><span class="sxs-lookup"><span data-stu-id="fbc42-134">Select the option to **include a custom JSON payload**.</span></span>
4. <span data-ttu-id="fbc42-135">Zapas oczekuje ładunku zapisany w formacie JSON z parametru o nazwie *tekstu*.</span><span class="sxs-lookup"><span data-stu-id="fbc42-135">Slack expects a payload formatted in JSON with a parameter named *text*.</span></span>  <span data-ttu-id="fbc42-136">To jest tekst, który będzie wyświetlany w komunikacie, który tworzy.</span><span class="sxs-lookup"><span data-stu-id="fbc42-136">This is the text that it will display in the message it creates.</span></span>  <span data-ttu-id="fbc42-137">Można użyć co najmniej jeden alert parametry, używając  *#*  symbol, taki jak w poniższym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="fbc42-137">You can use one or more of the alert parameters using the *#* symbol such as in the following example.</span></span>
   
    ```
    {
    "text":"#alertrulename fired with #searchresultcount records which exceeds the over threshold of #thresholdvalue ."
    }
    ```
   
    ![Przykładowy ładunek JSON](media/log-analytics-alerts-webhooks/oms-webhooks07.png)
5. <span data-ttu-id="fbc42-139">Kliknij przycisk **zapisać** można zapisać reguły alertów.</span><span class="sxs-lookup"><span data-stu-id="fbc42-139">Click **Save** to save the alert rule.</span></span>
6. <span data-ttu-id="fbc42-140">Poczekaj wystarczającą ilość czasu dla tworzonego alertu można utworzyć, a następnie sprawdź zapas czasu dla wiadomości, które są podobne do następującego.</span><span class="sxs-lookup"><span data-stu-id="fbc42-140">Wait sufficient time for an alert to be created and then check Slack for a message which will be similar to the following.</span></span>
   
   ![przykład webhook w zapas czasu](media/log-analytics-alerts-webhooks/oms-webhooks08.png)

### <a name="advanced-webhook-payload-for-slack"></a><span data-ttu-id="fbc42-142">Zaawansowane ładunku elementu webhook dla zapas czasu</span><span class="sxs-lookup"><span data-stu-id="fbc42-142">Advanced webhook payload for Slack</span></span>
<span data-ttu-id="fbc42-143">Często można dostosować komunikaty przychodzące z zapas czasu.</span><span class="sxs-lookup"><span data-stu-id="fbc42-143">You can extensively customize inbound messages with Slack.</span></span> <span data-ttu-id="fbc42-144">Aby uzyskać więcej informacji, zobacz [przychodzące elementów Webhook](https://api.slack.com/incoming-webhooks) na Slack witryny sieci Web.</span><span class="sxs-lookup"><span data-stu-id="fbc42-144">For more information, see [Incoming Webhooks](https://api.slack.com/incoming-webhooks) on the Slack website.</span></span> <span data-ttu-id="fbc42-145">Poniżej przedstawiono bardziej złożonych ładunku do tworzenia zaawansowanych wiadomości z formatowaniem.</span><span class="sxs-lookup"><span data-stu-id="fbc42-145">Following is a more complex payload to create a rich message with formatting:</span></span>

    {
        "attachments": [
            {
                "title":"OMS Alerts Custom Payload",
                "fields": [
                    {
                        "title": "Alert Rule Name",
                        "value": "#alertrulename"},
                    {
                        "title": "Link To SearchResults",
                        "value": "<#linktosearchresults|OMS Search Results>"},
                    {
                        "title": "Search Interval",
                        "value": "#searchinterval"},
                    {
                        "title": "Threshold Operator",
                        "value": "#thresholdoperator"},
                    {
                        "title": "Threshold Value",
                        "value": "#thresholdvalue"}
                ],
                "color": "#F35A00"
            }
        ]
    }


<span data-ttu-id="fbc42-146">Spowoduje to wygenerowanie komunikatu w zapas czasu podobny do następującego.</span><span class="sxs-lookup"><span data-stu-id="fbc42-146">This would generate a message in Slack similar to the following.</span></span>

![Przykładowy komunikat w zapas czasu](media/log-analytics-alerts-webhooks/oms-webhooks09.png)

## <a name="summary"></a><span data-ttu-id="fbc42-148">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="fbc42-148">Summary</span></span>
<span data-ttu-id="fbc42-149">Przy użyciu tej reguły alertów w miejscu trzeba komunikat wysłany do Slack za każdym razem, gdy są spełnione kryteria.</span><span class="sxs-lookup"><span data-stu-id="fbc42-149">With this alert rule in place, you would have a message sent to Slack every time the criteria is met.</span></span>  

<span data-ttu-id="fbc42-150">To jest tylko jeden przykład działań, które można tworzyć w odpowiedzi na alert.</span><span class="sxs-lookup"><span data-stu-id="fbc42-150">This is only one example of an action that you can create in response to an alert.</span></span>  <span data-ttu-id="fbc42-151">Można utworzyć akcję elementu webhook, która wywołuje innej usługi zewnętrzne, akcję elementu runbook, aby uruchomić element runbook automatyzacji Azure lub akcję poczty e-mail do wysyłania wiadomości e-mail do siebie lub innych odbiorców.</span><span class="sxs-lookup"><span data-stu-id="fbc42-151">You could create a webhook action that calls another external service, a runbook action to start a runbook in Azure Automation, or an email action to send a mail to yourself or other recipients.</span></span>   

## <a name="next-steps"></a><span data-ttu-id="fbc42-152">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="fbc42-152">Next Steps</span></span>
* <span data-ttu-id="fbc42-153">Dowiedz się więcej o innych [alertów akcje w analizy dzienników](log-analytics-alerts-actions.md) łącznie z czynności.</span><span class="sxs-lookup"><span data-stu-id="fbc42-153">Learn about other [alert actions in Log Analytics](log-analytics-alerts-actions.md) including other actions.</span></span>


