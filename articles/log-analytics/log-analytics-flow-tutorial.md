---
title: "Automatyzowanie procesów Analiza dzienników Azure z Flow firmy Microsoft"
description: "Dowiedz się, jak można użyć Microsoft Flow można szybko zautomatyzować powtarzalnych procesów za pomocą łącznika usługi Analiza dzienników Azure."
services: log-analytics
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: log-analytics
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: bwren
ms.openlocfilehash: 4955f90de06cd720d78c5bb60c0adcd7dc633245
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="automate-log-analytics-processes-with-the-connector-for-microsoft-flow"></a><span data-ttu-id="e9ad0-103">Automatyzacji procesów analizy dzienników przy użyciu łącznika dla Flow firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="e9ad0-103">Automate Log Analytics processes with the connector for Microsoft Flow</span></span>
<span data-ttu-id="e9ad0-104">[Microsoft Flow](https://ms.flow.microsoft.com) służy do tworzenia automatycznych przepływów pracy za pomocą setki akcje dla różnych usług.</span><span class="sxs-lookup"><span data-stu-id="e9ad0-104">[Microsoft Flow](https://ms.flow.microsoft.com) allows you to create automated workflows using hundreds of actions for a variety of services.</span></span> <span data-ttu-id="e9ad0-105">Dane wyjściowe z jedną akcję może służyć jako dane wejściowe do innego pozwala na tworzenie integrację różnych usług.</span><span class="sxs-lookup"><span data-stu-id="e9ad0-105">Output from one action can be used as input to another allowing you to create integration between different services.</span></span>  <span data-ttu-id="e9ad0-106">Łącznik usługi Analiza dzienników Azure dla programu Microsoft Flow pozwalają na tworzenie przepływów pracy, które zawierają dane pobierane przez dziennik wyszukiwania analizy dzienników.</span><span class="sxs-lookup"><span data-stu-id="e9ad0-106">The Azure Log Analytics connector for Microsoft Flow allow you to build workflows that include data retrieved by log searches in Log Analytics.</span></span>

<span data-ttu-id="e9ad0-107">Na przykład można użyć Microsoft Flow korzystanie danych analizy dzienników powiadomienie e-mail z usługi Office 365, tworzenie usterki w programie Visual Studio Team Services lub wysłać wiadomość Slack.</span><span class="sxs-lookup"><span data-stu-id="e9ad0-107">For example, you can use Microsoft Flow to use Log Analytics data in an email notification from Office 365, create a bug in Visual Studio Team Services, or post a Slack message.</span></span>  <span data-ttu-id="e9ad0-108">Przez harmonogram prosty lub niektóre akcje w podłączonej usługi takie jak po odebraniu wiadomości e-mail lub tweet, może wyzwolić przepływu pracy.</span><span class="sxs-lookup"><span data-stu-id="e9ad0-108">You can trigger a workflow by a simple schedule or from some action in a connected service such as when a mail or a tweet is received.</span></span>  


> [!NOTE]
> <span data-ttu-id="e9ad0-109">Łącznik usługi Analiza dzienników Azure dla programu Microsoft Flow wymaga obszaru roboczego zostaną uaktualnione do nowego języka zapytań usługi Analiza dzienników.</span><span class="sxs-lookup"><span data-stu-id="e9ad0-109">The Azure Log Analytics connector for Microsoft Flow requires your workspace to be upgraded to the new Log Analytics query language.</span></span> <span data-ttu-id="e9ad0-110">Możesz dowiedzieć się więcej o nowy język i uzyskać Procedura uaktualniania obszaru roboczego na [uaktualnienia obszaru roboczego analizy dzienników Azure do nowego wyszukiwania dziennika](log-analytics-log-search-upgrade.md).</span><span class="sxs-lookup"><span data-stu-id="e9ad0-110">You can learn more about the new language and get the procedure to upgrade your workspace at [Upgrade your Azure Log Analytics workspace to new log search](log-analytics-log-search-upgrade.md).</span></span>  

<span data-ttu-id="e9ad0-111">Samouczek, w tym artykule przedstawiono sposób tworzenia przepływu, który automatycznie wysyła wyniki wyszukiwania dziennika analizy dzienników pocztą e-mail, tylko jeden przykład stosowania analizy dzienników w Flow firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="e9ad0-111">The tutorial in this article shows you how to create a flow that automatically sends the results of a Log Analytics log search by email, just one example of how you can use Log Analytics in Microsoft Flow.</span></span> 


## <a name="step-1-create-a-flow"></a><span data-ttu-id="e9ad0-112">Krok 1: Tworzenie przepływu</span><span class="sxs-lookup"><span data-stu-id="e9ad0-112">Step 1: Create a flow</span></span>
1. <span data-ttu-id="e9ad0-113">Zaloguj się do [Microsoft Flow](http://flow.microsoft.com)i wybierz **Moje przepływa**.</span><span class="sxs-lookup"><span data-stu-id="e9ad0-113">Sign in to [Microsoft Flow](http://flow.microsoft.com), and select **My Flows**.</span></span>
2. <span data-ttu-id="e9ad0-114">Kliknij przycisk **+ Utwórz z puste**.</span><span class="sxs-lookup"><span data-stu-id="e9ad0-114">Click **+ Create from blank**.</span></span>

## <a name="step-2-create-a-trigger-for-your-flow"></a><span data-ttu-id="e9ad0-115">Krok 2: Tworzenie wyzwalacza dla Twojego przepływu</span><span class="sxs-lookup"><span data-stu-id="e9ad0-115">Step 2: Create a trigger for your flow</span></span>
1. <span data-ttu-id="e9ad0-116">Kliknij przycisk **wyszukiwania setki łączników i wyzwalaczy**.</span><span class="sxs-lookup"><span data-stu-id="e9ad0-116">Click **Search hundreds of connectors and triggers**.</span></span>
2. <span data-ttu-id="e9ad0-117">Typ **harmonogram** w polu wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="e9ad0-117">Type **Schedule** in the search box.</span></span>
3. <span data-ttu-id="e9ad0-118">Wybierz **harmonogram**, a następnie wybierz **harmonogram - cyklu**.</span><span class="sxs-lookup"><span data-stu-id="e9ad0-118">Select **Schedule**, and then select **Schedule - Recurrence**.</span></span>
4. <span data-ttu-id="e9ad0-119">W **częstotliwość** polu Wybierz **dzień** i **interwał** wprowadź **1**.</span><span class="sxs-lookup"><span data-stu-id="e9ad0-119">In the **Frequency** box select **Day** and in the **Interval** box, enter **1**.</span></span><br><br><span data-ttu-id="e9ad0-120">![Okno dialogowe Microsoft Flow wyzwalacza](media/log-analytics-flow-tutorial/flow01.png)</span><span class="sxs-lookup"><span data-stu-id="e9ad0-120">![Microsoft Flow trigger dialog box](media/log-analytics-flow-tutorial/flow01.png)</span></span>


## <a name="step-3-add-a-log-analytics-action"></a><span data-ttu-id="e9ad0-121">Krok 3: Dodaj akcję analizy dzienników</span><span class="sxs-lookup"><span data-stu-id="e9ad0-121">Step 3: Add a Log Analytics action</span></span>
1. <span data-ttu-id="e9ad0-122">Kliknij przycisk **+ nowy krok**, a następnie kliknij przycisk **Dodaj akcję**.</span><span class="sxs-lookup"><span data-stu-id="e9ad0-122">Click **+ New step**, and then click **Add an action**.</span></span>
2. <span data-ttu-id="e9ad0-123">Wyszukaj **dziennika analizy**.</span><span class="sxs-lookup"><span data-stu-id="e9ad0-123">Search for **Log Analytics**.</span></span>
3. <span data-ttu-id="e9ad0-124">Kliknij przycisk **Azure Log Analytics — uruchomić zapytanie i wizualizacja wyników**.</span><span class="sxs-lookup"><span data-stu-id="e9ad0-124">Click **Azure Log Analytics – Run query and visualize results**.</span></span><br><br><span data-ttu-id="e9ad0-125">![Uruchom okno kwerendy analizy dzienników](media/log-analytics-flow-tutorial/flow02.png)</span><span class="sxs-lookup"><span data-stu-id="e9ad0-125">![Log Analytics run query window](media/log-analytics-flow-tutorial/flow02.png)</span></span>

## <a name="step-4-configure-the-log-analytics-action"></a><span data-ttu-id="e9ad0-126">Krok 4: Konfigurowanie akcji analizy dzienników</span><span class="sxs-lookup"><span data-stu-id="e9ad0-126">Step 4: Configure the Log Analytics action</span></span>

1. <span data-ttu-id="e9ad0-127">Określ szczegóły dla obszaru roboczego, w tym subskrypcji identyfikator, grupy zasobów, a nazwa obszaru roboczego.</span><span class="sxs-lookup"><span data-stu-id="e9ad0-127">Specify the details for your workspace including the Subscription ID, Resource Group, and Workspace Name.</span></span>
2. <span data-ttu-id="e9ad0-128">Następujące zapytanie analizy dzienników, aby dodać **zapytania** okna.</span><span class="sxs-lookup"><span data-stu-id="e9ad0-128">Add the following Log Analytics query to the **Query** window.</span></span>  <span data-ttu-id="e9ad0-129">To jest tylko przykładowe zapytanie i możesz zastąpić dowolne inne zwracające dane.</span><span class="sxs-lookup"><span data-stu-id="e9ad0-129">This is only a sample query, and you can replace with any other that returns data.</span></span>
```
    Event
    | where EventLevelName == "Error" 
    | where TimeGenerated > ago(1day)
    | summarize count() by Computer
    | sort by Computerindow. 
```

2. <span data-ttu-id="e9ad0-130">Wybierz **tabeli HTML** dla **typ wykresu**.</span><span class="sxs-lookup"><span data-stu-id="e9ad0-130">Select **HTML Table** for the **Chart Type**.</span></span><br><br><span data-ttu-id="e9ad0-131">![Dziennik akcji analityka](media/log-analytics-flow-tutorial/flow03.png)</span><span class="sxs-lookup"><span data-stu-id="e9ad0-131">![Log Analytics action](media/log-analytics-flow-tutorial/flow03.png)</span></span>

## <a name="step-5-configure-the-flow-to-send-email"></a><span data-ttu-id="e9ad0-132">Krok 5: Konfigurowanie przepływu do wysyłania wiadomości e-mail</span><span class="sxs-lookup"><span data-stu-id="e9ad0-132">Step 5: Configure the flow to send email</span></span>

1. <span data-ttu-id="e9ad0-133">Kliknij przycisk **nowy krok**, a następnie kliknij przycisk **+ Dodaj akcję**.</span><span class="sxs-lookup"><span data-stu-id="e9ad0-133">Click **New step**, and then click **+ Add an action**.</span></span>
2. <span data-ttu-id="e9ad0-134">Wyszukaj **Outlook pakietu Office 365**.</span><span class="sxs-lookup"><span data-stu-id="e9ad0-134">Search for **Office 365 Outlook**.</span></span>
3. <span data-ttu-id="e9ad0-135">Kliknij przycisk **Office 365 Outlook — Wyślij usługi poczty e-mail**.</span><span class="sxs-lookup"><span data-stu-id="e9ad0-135">Click **Office 365 Outlook – Send an email**.</span></span><br><br><span data-ttu-id="e9ad0-136">![Okno wyboru Outlook pakietu Office 365](media/log-analytics-flow-tutorial/flow04.png)</span><span class="sxs-lookup"><span data-stu-id="e9ad0-136">![Office 365 Outlook selection window](media/log-analytics-flow-tutorial/flow04.png)</span></span>

4. <span data-ttu-id="e9ad0-137">Określ adres e-mail odbiorcy w **do** okno i temat wiadomości e-mail w **podmiotu**.</span><span class="sxs-lookup"><span data-stu-id="e9ad0-137">Specify the email address of a recipient in the **To** window and a subject for the email in **Subject**.</span></span>
5. <span data-ttu-id="e9ad0-138">Kliknij w dowolnym miejscu **treści** pole.</span><span class="sxs-lookup"><span data-stu-id="e9ad0-138">Click anywhere in the **Body** box.</span></span>  <span data-ttu-id="e9ad0-139">A **zawartości dynamicznej** zostanie otwarte okno z wartości z poprzedniej akcji.</span><span class="sxs-lookup"><span data-stu-id="e9ad0-139">A **Dynamic content** window opens with values from previous actions.</span></span>  
6. <span data-ttu-id="e9ad0-140">Wybierz **treści**.</span><span class="sxs-lookup"><span data-stu-id="e9ad0-140">Select **Body**.</span></span>  <span data-ttu-id="e9ad0-141">Jest to wyniki zapytania w akcji analizy dzienników.</span><span class="sxs-lookup"><span data-stu-id="e9ad0-141">This is the results of the query in the Log Analytics action.</span></span>
6. <span data-ttu-id="e9ad0-142">Kliknij przycisk **Pokaż zaawansowane opcje**.</span><span class="sxs-lookup"><span data-stu-id="e9ad0-142">Click **Show advanced options**.</span></span>
7. <span data-ttu-id="e9ad0-143">W **HTML jest** wybierz opcję **tak**.</span><span class="sxs-lookup"><span data-stu-id="e9ad0-143">In the **Is HTML** box, select **Yes**.</span></span><br><br><span data-ttu-id="e9ad0-144">![Okno Konfiguracja poczty e-mail usługi Office 365](media/log-analytics-flow-tutorial/flow05.png)</span><span class="sxs-lookup"><span data-stu-id="e9ad0-144">![Office 365 email configuration window](media/log-analytics-flow-tutorial/flow05.png)</span></span>

## <a name="step-6-save-and-test-your-flow"></a><span data-ttu-id="e9ad0-145">Krok 6: Zapisz i testowania przepływu użytkownika</span><span class="sxs-lookup"><span data-stu-id="e9ad0-145">Step 6: Save and test your flow</span></span>
1. <span data-ttu-id="e9ad0-146">W **nazwy przepływu** , Dodaj nazwę użytkownika przepływ, a następnie kliknij przycisk **utworzyć przepływ**.</span><span class="sxs-lookup"><span data-stu-id="e9ad0-146">In the **Flow name** box, add a name for your flow, and then click **Create flow**.</span></span><br><br><span data-ttu-id="e9ad0-147">![Zapisywanie przepływu](media/log-analytics-flow-tutorial/flow06.png)</span><span class="sxs-lookup"><span data-stu-id="e9ad0-147">![Save flow](media/log-analytics-flow-tutorial/flow06.png)</span></span>
2. <span data-ttu-id="e9ad0-148">Przepływ został utworzony i zostanie uruchomiona po dniu, czyli harmonogram, który można określić.</span><span class="sxs-lookup"><span data-stu-id="e9ad0-148">The flow is now created and will run after a day which is the schedule you specified.</span></span> 
3. <span data-ttu-id="e9ad0-149">Aby natychmiast przetestować przepływ, **Uruchom teraz** , a następnie **uruchomienia przepływu**.</span><span class="sxs-lookup"><span data-stu-id="e9ad0-149">To immediately test the flow, click **Run Now** and then **Run flow**.</span></span><br><br><span data-ttu-id="e9ad0-150">![Uruchamianie przepływu](media/log-analytics-flow-tutorial/flow07.png)</span><span class="sxs-lookup"><span data-stu-id="e9ad0-150">![Run flow](media/log-analytics-flow-tutorial/flow07.png)</span></span>
3. <span data-ttu-id="e9ad0-151">Po zakończeniu przepływu, Sprawdź pocztę adresata, który można określić.</span><span class="sxs-lookup"><span data-stu-id="e9ad0-151">When the flow completes, check the mail of the recipient that you specified.</span></span>  <span data-ttu-id="e9ad0-152">Powinna zostać odebrana poczty z treścią podobny do następującego:</span><span class="sxs-lookup"><span data-stu-id="e9ad0-152">You should have received a mail with a body similar to the following:</span></span><br><br>![Przykładowej wiadomości e-mail](media/log-analytics-flow-tutorial/flow08.png)


## <a name="next-steps"></a><span data-ttu-id="e9ad0-154">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e9ad0-154">Next steps</span></span>

- <span data-ttu-id="e9ad0-155">Dowiedz się więcej o [Zaloguj wyszukiwania analizy dzienników](log-analytics-log-search-new.md).</span><span class="sxs-lookup"><span data-stu-id="e9ad0-155">Learn more about [log searches in Log Analytics](log-analytics-log-search-new.md).</span></span>
- <span data-ttu-id="e9ad0-156">Dowiedz się więcej o [Microsoft Flow](https://ms.flow.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="e9ad0-156">Learn more about [Microsoft Flow](https://ms.flow.microsoft.com).</span></span>



