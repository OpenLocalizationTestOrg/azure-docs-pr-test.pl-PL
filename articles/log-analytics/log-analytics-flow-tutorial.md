---
title: "aaaAutomate Analiza dzienników Azure przetwarza z Flow firmy Microsoft"
description: "Dowiedz się, jak używasz Microsoft Flow tooquickly zautomatyzować powtarzalnych procesów za pomocą łącznika usługi Analiza dzienników Azure hello."
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
ms.openlocfilehash: 52026df968682842cc9f8d55f6f9875c5f9c10b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="automate-log-analytics-processes-with-hello-connector-for-microsoft-flow"></a><span data-ttu-id="d3351-103">Zautomatyzować procesy analizy dzienników z łącznikiem hello Flow firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="d3351-103">Automate Log Analytics processes with hello connector for Microsoft Flow</span></span>
<span data-ttu-id="d3351-104">[Microsoft Flow](https://ms.flow.microsoft.com) pozwala toocreate automatycznego przepływów pracy za pomocą setki akcje do różnych usług.</span><span class="sxs-lookup"><span data-stu-id="d3351-104">[Microsoft Flow](https://ms.flow.microsoft.com) allows you toocreate automated workflows using hundreds of actions for a variety of services.</span></span> <span data-ttu-id="d3351-105">Dane wyjściowe z jedną akcję może służyć jako tooanother wejściowych, umożliwiając integrację toocreate różnych usług.</span><span class="sxs-lookup"><span data-stu-id="d3351-105">Output from one action can be used as input tooanother allowing you toocreate integration between different services.</span></span>  <span data-ttu-id="d3351-106">Łącznik usługi Analiza dzienników Azure powitania dla Microsoft Flow pozwalają toobuild przepływy pracy, które zawierają dane pobierane przez dziennik wyszukiwania analizy dzienników.</span><span class="sxs-lookup"><span data-stu-id="d3351-106">hello Azure Log Analytics connector for Microsoft Flow allow you toobuild workflows that include data retrieved by log searches in Log Analytics.</span></span>

<span data-ttu-id="d3351-107">Na przykład można użyć danych analizy dzienników toouse Flow firmy Microsoft w wiadomość e-mail z powiadomieniem z usługi Office 365, tworzenie usterki w programie Visual Studio Team Services lub wysłać wiadomość Slack.</span><span class="sxs-lookup"><span data-stu-id="d3351-107">For example, you can use Microsoft Flow toouse Log Analytics data in an email notification from Office 365, create a bug in Visual Studio Team Services, or post a Slack message.</span></span>  <span data-ttu-id="d3351-108">Przez harmonogram prosty lub niektóre akcje w podłączonej usługi takie jak po odebraniu wiadomości e-mail lub tweet, może wyzwolić przepływu pracy.</span><span class="sxs-lookup"><span data-stu-id="d3351-108">You can trigger a workflow by a simple schedule or from some action in a connected service such as when a mail or a tweet is received.</span></span>  


> [!NOTE]
> <span data-ttu-id="d3351-109">Łącznik usługi Analiza dzienników Azure Hello dla Microsoft Flow wymaga obszaru roboczego toobe uaktualnione toohello nowego analizy dzienników zapytania języka.</span><span class="sxs-lookup"><span data-stu-id="d3351-109">hello Azure Log Analytics connector for Microsoft Flow requires your workspace toobe upgraded toohello new Log Analytics query language.</span></span> <span data-ttu-id="d3351-110">Możesz dowiedzieć się więcej o nowy język hello i uzyskać hello procedury tooupgrade obszaru roboczego na [uaktualnienia wyszukiwania dziennika toonew roboczym usługi Analiza dzienników Azure](log-analytics-log-search-upgrade.md).</span><span class="sxs-lookup"><span data-stu-id="d3351-110">You can learn more about hello new language and get hello procedure tooupgrade your workspace at [Upgrade your Azure Log Analytics workspace toonew log search](log-analytics-log-search-upgrade.md).</span></span>  

<span data-ttu-id="d3351-111">Samouczek Hello w tym artykule przedstawiono, jak toocreate przepływ, który automatycznie wysyła pocztą e-mail, tylko jeden przykład stosowania analizy dzienników w Microsoft Flow hello wyniki wyszukiwania dziennika analizy dzienników.</span><span class="sxs-lookup"><span data-stu-id="d3351-111">hello tutorial in this article shows you how toocreate a flow that automatically sends hello results of a Log Analytics log search by email, just one example of how you can use Log Analytics in Microsoft Flow.</span></span> 


## <a name="step-1-create-a-flow"></a><span data-ttu-id="d3351-112">Krok 1: Tworzenie przepływu</span><span class="sxs-lookup"><span data-stu-id="d3351-112">Step 1: Create a flow</span></span>
1. <span data-ttu-id="d3351-113">Zaloguj się za[Microsoft Flow](http://flow.microsoft.com)i wybierz **Moje przepływa**.</span><span class="sxs-lookup"><span data-stu-id="d3351-113">Sign in too[Microsoft Flow](http://flow.microsoft.com), and select **My Flows**.</span></span>
2. <span data-ttu-id="d3351-114">Kliknij przycisk **+ Utwórz z puste**.</span><span class="sxs-lookup"><span data-stu-id="d3351-114">Click **+ Create from blank**.</span></span>

## <a name="step-2-create-a-trigger-for-your-flow"></a><span data-ttu-id="d3351-115">Krok 2: Tworzenie wyzwalacza dla Twojego przepływu</span><span class="sxs-lookup"><span data-stu-id="d3351-115">Step 2: Create a trigger for your flow</span></span>
1. <span data-ttu-id="d3351-116">Kliknij przycisk **wyszukiwania setki łączników i wyzwalaczy**.</span><span class="sxs-lookup"><span data-stu-id="d3351-116">Click **Search hundreds of connectors and triggers**.</span></span>
2. <span data-ttu-id="d3351-117">Typ **harmonogram** hello pola wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="d3351-117">Type **Schedule** in hello search box.</span></span>
3. <span data-ttu-id="d3351-118">Wybierz **harmonogram**, a następnie wybierz **harmonogram - cyklu**.</span><span class="sxs-lookup"><span data-stu-id="d3351-118">Select **Schedule**, and then select **Schedule - Recurrence**.</span></span>
4. <span data-ttu-id="d3351-119">W hello **częstotliwość** polu Wybierz **dzień** w hello **interwał** wprowadź **1**.</span><span class="sxs-lookup"><span data-stu-id="d3351-119">In hello **Frequency** box select **Day** and in hello **Interval** box, enter **1**.</span></span><br><br><span data-ttu-id="d3351-120">![Okno dialogowe Microsoft Flow wyzwalacza](media/log-analytics-flow-tutorial/flow01.png)</span><span class="sxs-lookup"><span data-stu-id="d3351-120">![Microsoft Flow trigger dialog box](media/log-analytics-flow-tutorial/flow01.png)</span></span>


## <a name="step-3-add-a-log-analytics-action"></a><span data-ttu-id="d3351-121">Krok 3: Dodaj akcję analizy dzienników</span><span class="sxs-lookup"><span data-stu-id="d3351-121">Step 3: Add a Log Analytics action</span></span>
1. <span data-ttu-id="d3351-122">Kliknij przycisk **+ nowy krok**, a następnie kliknij przycisk **Dodaj akcję**.</span><span class="sxs-lookup"><span data-stu-id="d3351-122">Click **+ New step**, and then click **Add an action**.</span></span>
2. <span data-ttu-id="d3351-123">Wyszukaj **dziennika analizy**.</span><span class="sxs-lookup"><span data-stu-id="d3351-123">Search for **Log Analytics**.</span></span>
3. <span data-ttu-id="d3351-124">Kliknij przycisk **Azure Log Analytics — uruchomić zapytanie i wizualizacja wyników**.</span><span class="sxs-lookup"><span data-stu-id="d3351-124">Click **Azure Log Analytics – Run query and visualize results**.</span></span><br><br><span data-ttu-id="d3351-125">![Uruchom okno kwerendy analizy dzienników](media/log-analytics-flow-tutorial/flow02.png)</span><span class="sxs-lookup"><span data-stu-id="d3351-125">![Log Analytics run query window](media/log-analytics-flow-tutorial/flow02.png)</span></span>

## <a name="step-4-configure-hello-log-analytics-action"></a><span data-ttu-id="d3351-126">Krok 4: Konfigurowanie hello analizy dzienników akcji</span><span class="sxs-lookup"><span data-stu-id="d3351-126">Step 4: Configure hello Log Analytics action</span></span>

1. <span data-ttu-id="d3351-127">Określ szczegóły hello obszaru roboczego, w tym hello subskrypcji identyfikator, grupy zasobów, a nazwa obszaru roboczego.</span><span class="sxs-lookup"><span data-stu-id="d3351-127">Specify hello details for your workspace including hello Subscription ID, Resource Group, and Workspace Name.</span></span>
2. <span data-ttu-id="d3351-128">Dodaj powitania po toohello zapytania analizy dzienników **zapytania** okna.</span><span class="sxs-lookup"><span data-stu-id="d3351-128">Add hello following Log Analytics query toohello **Query** window.</span></span>  <span data-ttu-id="d3351-129">To jest tylko przykładowe zapytanie i możesz zastąpić dowolne inne zwracające dane.</span><span class="sxs-lookup"><span data-stu-id="d3351-129">This is only a sample query, and you can replace with any other that returns data.</span></span>
```
    Event
    | where EventLevelName == "Error" 
    | where TimeGenerated > ago(1day)
    | summarize count() by Computer
    | sort by Computerindow. 
```

2. <span data-ttu-id="d3351-130">Wybierz **tabeli HTML** dla hello **typ wykresu**.</span><span class="sxs-lookup"><span data-stu-id="d3351-130">Select **HTML Table** for hello **Chart Type**.</span></span><br><br><span data-ttu-id="d3351-131">![Dziennik akcji analityka](media/log-analytics-flow-tutorial/flow03.png)</span><span class="sxs-lookup"><span data-stu-id="d3351-131">![Log Analytics action](media/log-analytics-flow-tutorial/flow03.png)</span></span>

## <a name="step-5-configure-hello-flow-toosend-email"></a><span data-ttu-id="d3351-132">Krok 5: Konfigurowanie hello przepływu toosend e-mail</span><span class="sxs-lookup"><span data-stu-id="d3351-132">Step 5: Configure hello flow toosend email</span></span>

1. <span data-ttu-id="d3351-133">Kliknij przycisk **nowy krok**, a następnie kliknij przycisk **+ Dodaj akcję**.</span><span class="sxs-lookup"><span data-stu-id="d3351-133">Click **New step**, and then click **+ Add an action**.</span></span>
2. <span data-ttu-id="d3351-134">Wyszukaj **Outlook pakietu Office 365**.</span><span class="sxs-lookup"><span data-stu-id="d3351-134">Search for **Office 365 Outlook**.</span></span>
3. <span data-ttu-id="d3351-135">Kliknij przycisk **Office 365 Outlook — Wyślij usługi poczty e-mail**.</span><span class="sxs-lookup"><span data-stu-id="d3351-135">Click **Office 365 Outlook – Send an email**.</span></span><br><br><span data-ttu-id="d3351-136">![Okno wyboru Outlook pakietu Office 365](media/log-analytics-flow-tutorial/flow04.png)</span><span class="sxs-lookup"><span data-stu-id="d3351-136">![Office 365 Outlook selection window](media/log-analytics-flow-tutorial/flow04.png)</span></span>

4. <span data-ttu-id="d3351-137">Określ adres e-mail adresata hello w hello **do** okno i temat wiadomości e-mail hello w **podmiotu**.</span><span class="sxs-lookup"><span data-stu-id="d3351-137">Specify hello email address of a recipient in hello **To** window and a subject for hello email in **Subject**.</span></span>
5. <span data-ttu-id="d3351-138">Kliknij w dowolnym miejscu hello **treści** pole.</span><span class="sxs-lookup"><span data-stu-id="d3351-138">Click anywhere in hello **Body** box.</span></span>  <span data-ttu-id="d3351-139">A **zawartości dynamicznej** zostanie otwarte okno z wartości z poprzedniej akcji.</span><span class="sxs-lookup"><span data-stu-id="d3351-139">A **Dynamic content** window opens with values from previous actions.</span></span>  
6. <span data-ttu-id="d3351-140">Wybierz **treści**.</span><span class="sxs-lookup"><span data-stu-id="d3351-140">Select **Body**.</span></span>  <span data-ttu-id="d3351-141">Jest to hello wyniki zapytania hello w hello analizy dzienników akcji.</span><span class="sxs-lookup"><span data-stu-id="d3351-141">This is hello results of hello query in hello Log Analytics action.</span></span>
6. <span data-ttu-id="d3351-142">Kliknij przycisk **Pokaż zaawansowane opcje**.</span><span class="sxs-lookup"><span data-stu-id="d3351-142">Click **Show advanced options**.</span></span>
7. <span data-ttu-id="d3351-143">W hello **HTML jest** wybierz opcję **tak**.</span><span class="sxs-lookup"><span data-stu-id="d3351-143">In hello **Is HTML** box, select **Yes**.</span></span><br><br><span data-ttu-id="d3351-144">![Okno Konfiguracja poczty e-mail usługi Office 365](media/log-analytics-flow-tutorial/flow05.png)</span><span class="sxs-lookup"><span data-stu-id="d3351-144">![Office 365 email configuration window](media/log-analytics-flow-tutorial/flow05.png)</span></span>

## <a name="step-6-save-and-test-your-flow"></a><span data-ttu-id="d3351-145">Krok 6: Zapisz i testowania przepływu użytkownika</span><span class="sxs-lookup"><span data-stu-id="d3351-145">Step 6: Save and test your flow</span></span>
1. <span data-ttu-id="d3351-146">W hello **nazwy przepływu** , Dodaj nazwę użytkownika przepływ, a następnie kliknij przycisk **utworzyć przepływ**.</span><span class="sxs-lookup"><span data-stu-id="d3351-146">In hello **Flow name** box, add a name for your flow, and then click **Create flow**.</span></span><br><br><span data-ttu-id="d3351-147">![Zapisywanie przepływu](media/log-analytics-flow-tutorial/flow06.png)</span><span class="sxs-lookup"><span data-stu-id="d3351-147">![Save flow](media/log-analytics-flow-tutorial/flow06.png)</span></span>
2. <span data-ttu-id="d3351-148">Hello przepływ został utworzony i zostanie uruchomiony po dniu, czyli hello harmonogramem.</span><span class="sxs-lookup"><span data-stu-id="d3351-148">hello flow is now created and will run after a day which is hello schedule you specified.</span></span> 
3. <span data-ttu-id="d3351-149">tooimmediately testu hello przepływu, kliknij przycisk **Uruchom teraz** , a następnie **uruchomienia przepływu**.</span><span class="sxs-lookup"><span data-stu-id="d3351-149">tooimmediately test hello flow, click **Run Now** and then **Run flow**.</span></span><br><br><span data-ttu-id="d3351-150">![Uruchamianie przepływu](media/log-analytics-flow-tutorial/flow07.png)</span><span class="sxs-lookup"><span data-stu-id="d3351-150">![Run flow](media/log-analytics-flow-tutorial/flow07.png)</span></span>
3. <span data-ttu-id="d3351-151">Po zakończeniu przepływu hello, Sprawdź pocztę hello hello adresata, określony.</span><span class="sxs-lookup"><span data-stu-id="d3351-151">When hello flow completes, check hello mail of hello recipient that you specified.</span></span>  <span data-ttu-id="d3351-152">Powinna zostać odebrana poczty następujący toohello podobne treści:</span><span class="sxs-lookup"><span data-stu-id="d3351-152">You should have received a mail with a body similar toohello following:</span></span><br><br>![Przykładowej wiadomości e-mail](media/log-analytics-flow-tutorial/flow08.png)


## <a name="next-steps"></a><span data-ttu-id="d3351-154">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d3351-154">Next steps</span></span>

- <span data-ttu-id="d3351-155">Dowiedz się więcej o [Zaloguj wyszukiwania analizy dzienników](log-analytics-log-search-new.md).</span><span class="sxs-lookup"><span data-stu-id="d3351-155">Learn more about [log searches in Log Analytics](log-analytics-log-search-new.md).</span></span>
- <span data-ttu-id="d3351-156">Dowiedz się więcej o [Microsoft Flow](https://ms.flow.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="d3351-156">Learn more about [Microsoft Flow](https://ms.flow.microsoft.com).</span></span>



