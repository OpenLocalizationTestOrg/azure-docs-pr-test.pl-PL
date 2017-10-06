---
title: "Przykładowe akcji alertu aaaWebhook w OMS Log Analytics | Dokumentacja firmy Microsoft"
description: "Jedną z akcji hello można uruchomić w odpowiedzi tooa alert analizy dzienników jest * webhook *, dzięki czemu można tooinvoke procesu zewnętrznego przez pojedyncze żądanie HTTP. W tym artykule przedstawiono przykład tworzenia akcji elementu webhook w alercie analizy dzienników, przy użyciu zapas czasu."
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
ms.openlocfilehash: e60bdc4922347073d572c2e4719461b13e8e7d1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-alert-webhook-action-in-oms-log-analytics-toosend-message-tooslack"></a><span data-ttu-id="f10f7-104">Tworzy akcję alertu elementu webhook w tooSlack komunikat toosend OMS analizy dzienników</span><span class="sxs-lookup"><span data-stu-id="f10f7-104">Create an alert webhook action in OMS Log Analytics toosend message tooSlack</span></span>
<span data-ttu-id="f10f7-105">Jedną z akcji hello można uruchomić w odpowiedzi tooa [alert analizy dzienników](log-analytics-alerts.md) jest *webhook*, co pozwala tooinvoke procesu zewnętrznego przez pojedyncze żądanie HTTP.</span><span class="sxs-lookup"><span data-stu-id="f10f7-105">One of hello actions you can run in response tooa [Log Analytics alert](log-analytics-alerts.md) is a *webhook*, which allows you tooinvoke an external process through a single HTTP request.</span></span>  <span data-ttu-id="f10f7-106">Możesz przeczytać o szczegółach alertów i elementów webhook w [alertów w analizy dzienników](log-analytics-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="f10f7-106">You can read about details of alerts and webhooks in [Alerts in Log Analytics](log-analytics-alerts.md)</span></span>

<span data-ttu-id="f10f7-107">W tym artykule omówimy przykładem tworzenia akcji elementu webhook w przypadku wystąpienia alertu analizy dzienników przy użyciu zapas czasu, która jest usługą obsługi wiadomości.</span><span class="sxs-lookup"><span data-stu-id="f10f7-107">In this article, we’ll walk through an example of creating a webhook action in a Log Analytics alert using Slack which is a messaging service.</span></span>

> [!NOTE]
> <span data-ttu-id="f10f7-108">Toocomplete Slack konto musi mieć w tym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="f10f7-108">You must have a Slack account toocomplete this sample.</span></span>  <span data-ttu-id="f10f7-109">Można założyć bezpłatne konto w [slack.com](http://slack.com).</span><span class="sxs-lookup"><span data-stu-id="f10f7-109">You can sign up for a free account at [slack.com](http://slack.com).</span></span>
> 
> 

## <a name="step-1---enable-webhooks-in-slack"></a><span data-ttu-id="f10f7-110">Krok 1 — elementów webhook Włącz w zapas czasu</span><span class="sxs-lookup"><span data-stu-id="f10f7-110">Step 1 - Enable webhooks in Slack</span></span>
1. <span data-ttu-id="f10f7-111">Zaloguj się tooSlack na [slack.com](http://slack.com).</span><span class="sxs-lookup"><span data-stu-id="f10f7-111">Sign in tooSlack at [slack.com](http://slack.com).</span></span>
2. <span data-ttu-id="f10f7-112">Wybierz kanał hello **kanałów** sekcji w okienku po lewej stronie powitania.</span><span class="sxs-lookup"><span data-stu-id="f10f7-112">Select a channel in hello **Channels** section in hello left pane.</span></span>  <span data-ttu-id="f10f7-113">Jest to kanał hello otrzyma tę wiadomość hello.</span><span class="sxs-lookup"><span data-stu-id="f10f7-113">This is hello channel that hello message will be sent to.</span></span>  <span data-ttu-id="f10f7-114">Można wybrać jedną z kanałów domyślne hello takich jak **ogólne** lub **losowe**.</span><span class="sxs-lookup"><span data-stu-id="f10f7-114">You can select one of hello default channels such as **general** or **random**.</span></span>  <span data-ttu-id="f10f7-115">W środowisku produkcyjnym, należy prawdopodobnie utworzyć kanał specjalne takie jak **criticalservicealerts**.</span><span class="sxs-lookup"><span data-stu-id="f10f7-115">In a production scenario, you would most likely create a special channel such as **criticalservicealerts**.</span></span> <br>
   
   ![Kanałach Slack](media/log-analytics-alerts-webhooks/oms-webhooks01.png)
3. <span data-ttu-id="f10f7-117">Kliknij przycisk **Dodawanie aplikacji lub niestandardowej integracji** tooopen hello katalogu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f10f7-117">Click **Add an app or custom integration** tooopen hello App Directory.</span></span>
4. <span data-ttu-id="f10f7-118">Typ *elementów webhook* do pola wyszukiwania hello, a następnie wybierz **przychodzące elementów Webhook**.</span><span class="sxs-lookup"><span data-stu-id="f10f7-118">Type *webhooks* into hello search box and then select **Incoming WebHooks**.</span></span> <br>
   
   ![Kanałach Slack](media/log-analytics-alerts-webhooks/oms-webhooks02.png)
5. <span data-ttu-id="f10f7-120">Kliknij przycisk **zainstalować** Nazwa zespołu tooyour dalej.</span><span class="sxs-lookup"><span data-stu-id="f10f7-120">Click **Install** next tooyour team name.</span></span>
6. <span data-ttu-id="f10f7-121">Kliknij przycisk **Dodaj konfigurację**.</span><span class="sxs-lookup"><span data-stu-id="f10f7-121">Click **Add Configuration**.</span></span>
7. <span data-ttu-id="f10f7-122">Wybierz hello hello kanału zacząć toouse w tym przykładzie, a następnie kliknij przycisk **integracji dodać przychodzące elementów Webhook**.</span><span class="sxs-lookup"><span data-stu-id="f10f7-122">Select hello hello channel that you're going toouse for this example, and then click **Add Incoming WebHooks integration**.</span></span>  
8. <span data-ttu-id="f10f7-123">Kopiuj hello **adresu URL elementu Webhook**.</span><span class="sxs-lookup"><span data-stu-id="f10f7-123">Copy hello **Webhook URL**.</span></span>  <span data-ttu-id="f10f7-124">Będzie można wklejane to w konfiguracji alertu hello.</span><span class="sxs-lookup"><span data-stu-id="f10f7-124">You'll be pasting this into hello Alert configuration.</span></span> <br>
   
    ![Kanałach Slack](media/log-analytics-alerts-webhooks/oms-webhooks05.png)

## <a name="step-2---create-alert-rule-in-log-analytics"></a><span data-ttu-id="f10f7-126">Krok 2 — Tworzenie reguły alertu w analizy dzienników</span><span class="sxs-lookup"><span data-stu-id="f10f7-126">Step 2 - Create alert rule in Log Analytics</span></span>
1. <span data-ttu-id="f10f7-127">[Tworzenie reguły alertu](log-analytics-alerts.md) z hello następujące ustawienia.</span><span class="sxs-lookup"><span data-stu-id="f10f7-127">[Create an alert rule](log-analytics-alerts.md) with hello following settings.</span></span>
   * <span data-ttu-id="f10f7-128">Zapytanie:```    Type=Event EventLevelName=error ```</span><span class="sxs-lookup"><span data-stu-id="f10f7-128">Query: ```    Type=Event EventLevelName=error ```</span></span>
   * <span data-ttu-id="f10f7-129">Sprawdź, czy ten alert co: 5 minut</span><span class="sxs-lookup"><span data-stu-id="f10f7-129">Check for this alert every: 5 minutes</span></span>
   * <span data-ttu-id="f10f7-130">Witaj liczba wyników to: większe niż 10</span><span class="sxs-lookup"><span data-stu-id="f10f7-130">hello number of results is: greater than 10</span></span>
   * <span data-ttu-id="f10f7-131">W tym oknie: 60 minut</span><span class="sxs-lookup"><span data-stu-id="f10f7-131">Over this time window: 60 minutes</span></span>
   * <span data-ttu-id="f10f7-132">Wybierz **tak** dla **Webhook** i **nr** dla hello innych działań.</span><span class="sxs-lookup"><span data-stu-id="f10f7-132">Select **Yes** for **Webhook** and **No** for hello other actions.</span></span>
2. <span data-ttu-id="f10f7-133">Witaj Wklej adres URL zapas czasu na powitania **adresu URL elementu Webhook** pola.</span><span class="sxs-lookup"><span data-stu-id="f10f7-133">Paste hello Slack URL into hello **Webhook URL** field.</span></span>
3. <span data-ttu-id="f10f7-134">Wybierz opcję hello zbyt**Uwzględnij niestandardowy ładunek JSON**.</span><span class="sxs-lookup"><span data-stu-id="f10f7-134">Select hello option too**include a custom JSON payload**.</span></span>
4. <span data-ttu-id="f10f7-135">Zapas oczekuje ładunku zapisany w formacie JSON z parametru o nazwie *tekstu*.</span><span class="sxs-lookup"><span data-stu-id="f10f7-135">Slack expects a payload formatted in JSON with a parameter named *text*.</span></span>  <span data-ttu-id="f10f7-136">Jest to hello tekst, który będzie wyświetlany w wiadomości powitania, który tworzy.</span><span class="sxs-lookup"><span data-stu-id="f10f7-136">This is hello text that it will display in hello message it creates.</span></span>  <span data-ttu-id="f10f7-137">Można użyć co najmniej jednego hello alert parametry, używając hello  *#*  symboli, takie jak hello poniższy przykład.</span><span class="sxs-lookup"><span data-stu-id="f10f7-137">You can use one or more of hello alert parameters using hello *#* symbol such as in hello following example.</span></span>
   
    ```
    {
    "text":"#alertrulename fired with #searchresultcount records which exceeds hello over threshold of #thresholdvalue ."
    }
    ```
   
    ![Przykładowy ładunek JSON](media/log-analytics-alerts-webhooks/oms-webhooks07.png)
5. <span data-ttu-id="f10f7-139">Kliknij przycisk **zapisać** toosave hello alertu.</span><span class="sxs-lookup"><span data-stu-id="f10f7-139">Click **Save** toosave hello alert rule.</span></span>
6. <span data-ttu-id="f10f7-140">Poczekaj wystarczającą ilość czasu alertu toobe utworzone, a następnie sprawdź zapas czasu dla komunikatu, którego będzie podobne następujące toohello.</span><span class="sxs-lookup"><span data-stu-id="f10f7-140">Wait sufficient time for an alert toobe created and then check Slack for a message which will be similar toohello following.</span></span>
   
   ![przykład webhook w zapas czasu](media/log-analytics-alerts-webhooks/oms-webhooks08.png)

### <a name="advanced-webhook-payload-for-slack"></a><span data-ttu-id="f10f7-142">Zaawansowane ładunku elementu webhook dla zapas czasu</span><span class="sxs-lookup"><span data-stu-id="f10f7-142">Advanced webhook payload for Slack</span></span>
<span data-ttu-id="f10f7-143">Często można dostosować komunikaty przychodzące z zapas czasu.</span><span class="sxs-lookup"><span data-stu-id="f10f7-143">You can extensively customize inbound messages with Slack.</span></span> <span data-ttu-id="f10f7-144">Aby uzyskać więcej informacji, zobacz [przychodzące elementów Webhook](https://api.slack.com/incoming-webhooks) na powitania Slack witryny sieci Web.</span><span class="sxs-lookup"><span data-stu-id="f10f7-144">For more information, see [Incoming Webhooks](https://api.slack.com/incoming-webhooks) on hello Slack website.</span></span> <span data-ttu-id="f10f7-145">Poniżej przedstawiono bardziej złożonych toocreate ładunku sformatowany komunikat z formatowaniem.</span><span class="sxs-lookup"><span data-stu-id="f10f7-145">Following is a more complex payload toocreate a rich message with formatting:</span></span>

    {
        "attachments": [
            {
                "title":"OMS Alerts Custom Payload",
                "fields": [
                    {
                        "title": "Alert Rule Name",
                        "value": "#alertrulename"},
                    {
                        "title": "Link tooSearchResults",
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


<span data-ttu-id="f10f7-146">Spowoduje to generowanie wiadomości w Slack następujące toohello podobne.</span><span class="sxs-lookup"><span data-stu-id="f10f7-146">This would generate a message in Slack similar toohello following.</span></span>

![Przykładowy komunikat w zapas czasu](media/log-analytics-alerts-webhooks/oms-webhooks09.png)

## <a name="summary"></a><span data-ttu-id="f10f7-148">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="f10f7-148">Summary</span></span>
<span data-ttu-id="f10f7-149">Przy użyciu tej reguły alertów w miejscu trzeba tooSlack komunikatu wysłanego za każdym razem, gdy są spełnione kryteria hello.</span><span class="sxs-lookup"><span data-stu-id="f10f7-149">With this alert rule in place, you would have a message sent tooSlack every time hello criteria is met.</span></span>  

<span data-ttu-id="f10f7-150">Jest tylko jeden przykład działań można tworzyć w odpowiedzi tooan alertu.</span><span class="sxs-lookup"><span data-stu-id="f10f7-150">This is only one example of an action that you can create in response tooan alert.</span></span>  <span data-ttu-id="f10f7-151">Można utworzyć akcję elementu webhook, wywołującą innej usługi zewnętrzne toostart działania elementu runbook, element runbook w automatyzacji Azure lub toosend akcji poczty e-mail, tooyourself poczty lub innych odbiorców.</span><span class="sxs-lookup"><span data-stu-id="f10f7-151">You could create a webhook action that calls another external service, a runbook action toostart a runbook in Azure Automation, or an email action toosend a mail tooyourself or other recipients.</span></span>   

## <a name="next-steps"></a><span data-ttu-id="f10f7-152">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f10f7-152">Next Steps</span></span>
* <span data-ttu-id="f10f7-153">Dowiedz się więcej o innych [alertów akcje w analizy dzienników](log-analytics-alerts-actions.md) łącznie z czynności.</span><span class="sxs-lookup"><span data-stu-id="f10f7-153">Learn about other [alert actions in Log Analytics](log-analytics-alerts-actions.md) including other actions.</span></span>


