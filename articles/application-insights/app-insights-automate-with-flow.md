---
title: aaaAutomate Azure Application Insights przetwarza z Flow firmy Microsoft
description: "Dowiedz się, jak używasz Microsoft Flow tooquickly zautomatyzować powtarzalnych procesów za pomocą łącznika usługi Application Insights hello."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 06/25/2017
ms.author: bwren
ms.openlocfilehash: b34488a6b8b8b0a6add960a67f1426cbbbc13552
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="automate-azure-application-insights-processes-with-hello-connector-for-microsoft-flow"></a><span data-ttu-id="0a27a-103">Zautomatyzować procesy Azure Application Insights z łącznikiem hello Flow firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="0a27a-103">Automate Azure Application Insights processes with hello connector for Microsoft Flow</span></span>

<span data-ttu-id="0a27a-104">Czy zaczniesz wielokrotnie systemem hello tego samego zapytania z toocheck danych telemetrii, że usługa działa prawidłowo?</span><span class="sxs-lookup"><span data-stu-id="0a27a-104">Do you find yourself repeatedly running hello same queries on your telemetry data toocheck that your service is functioning properly?</span></span> <span data-ttu-id="0a27a-105">Następnie tworzenia własnych przepływów pracy wokół nich i są wyglądającej tooautomate te zapytania do znajdowania trendów i anomalii? Hello łącznika Azure Application Insights (wersja zapoznawcza) dla programu Microsoft Flow jest hello właściwych narzędzi dla tych celów.</span><span class="sxs-lookup"><span data-stu-id="0a27a-105">Are you looking tooautomate these queries for finding trends and anomalies and then build your own workflows around them? hello Azure Application Insights connector (preview) for Microsoft Flow is hello right tool for these purposes.</span></span>

<span data-ttu-id="0a27a-106">Dzięki tej integracji teraz można zautomatyzować wiele procesów bez pisania pojedynczy wiersz kodu.</span><span class="sxs-lookup"><span data-stu-id="0a27a-106">With this integration, you can now automate numerous processes without writing a single line of code.</span></span> <span data-ttu-id="0a27a-107">Po utworzeniu przepływu za pomocą usługi Application Insights akcji przepływu hello automatycznie uruchamia kwerendy analizy Insights aplikacji.</span><span class="sxs-lookup"><span data-stu-id="0a27a-107">After you create a flow by using an Application Insights action, hello flow automatically runs your Application Insights Analytics query.</span></span> 

<span data-ttu-id="0a27a-108">Można dodać również dodatkowe akcje.</span><span class="sxs-lookup"><span data-stu-id="0a27a-108">You can add additional actions as well.</span></span> <span data-ttu-id="0a27a-109">Microsoft Flow udostępnia setki akcje.</span><span class="sxs-lookup"><span data-stu-id="0a27a-109">Microsoft Flow makes hundreds of actions available.</span></span> <span data-ttu-id="0a27a-110">Na przykład można użyć Microsoft Flow tooautomatically Wyślij wiadomość e-mail z powiadomieniem lub tworzenie usterki w programie Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="0a27a-110">For example, you can use Microsoft Flow tooautomatically send an email notification or create a bug in Visual Studio Team Services.</span></span> <span data-ttu-id="0a27a-111">Umożliwia także jedną hello wiele [szablony](https://ms.flow.microsoft.com/en-us/connectors/shared_applicationinsights/?slug=azure-application-insights) dostępnych dla łącznika powitania dla Flow firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="0a27a-111">You can also use one of hello many [templates](https://ms.flow.microsoft.com/en-us/connectors/shared_applicationinsights/?slug=azure-application-insights) that are available for hello connector for Microsoft Flow.</span></span> <span data-ttu-id="0a27a-112">Te szablony przyspieszyć proces hello tworzenia przepływu.</span><span class="sxs-lookup"><span data-stu-id="0a27a-112">These templates speed up hello process of creating a flow.</span></span> 

<!--hello Application Insights connector also works with [Azure Power Apps](https://powerapps.microsoft.com/en-us/) and [Azure Logic Apps](https://azure.microsoft.com/services/logic-apps/?v=17.23h). --> 

## <a name="create-a-flow-for-application-insights"></a><span data-ttu-id="0a27a-113">Utwórz strumień dla usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="0a27a-113">Create a flow for Application Insights</span></span>

<span data-ttu-id="0a27a-114">Z tego samouczka dowiesz się, jak toocreate przepływ, który używa hello Analytics klastra automatycznie algorytmu toogroup atrybutów w hello danych dla aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="0a27a-114">In this tutorial, you will learn how toocreate a flow that uses hello Analytics auto-cluster algorithm toogroup attributes in hello data for a web application.</span></span> <span data-ttu-id="0a27a-115">Przepływ Hello automatycznie wysyła wyników hello za pośrednictwem poczty e-mail, tylko jeden przykład sposobu użycia Flow firmy Microsoft i analizy aplikacji Insights ze sobą.</span><span class="sxs-lookup"><span data-stu-id="0a27a-115">hello flow automatically sends hello results by email, just one example of how you can use Microsoft Flow and Application Insights Analytics together.</span></span> 

### <a name="step-1-create-a-flow"></a><span data-ttu-id="0a27a-116">Krok 1: Tworzenie przepływu</span><span class="sxs-lookup"><span data-stu-id="0a27a-116">Step 1: Create a flow</span></span>
1. <span data-ttu-id="0a27a-117">Zaloguj się za[Microsoft Flow](http://flow.microsoft.com), a następnie wybierz **Moje przepływa**.</span><span class="sxs-lookup"><span data-stu-id="0a27a-117">Sign in too[Microsoft Flow](http://flow.microsoft.com), and then select **My Flows**.</span></span>
2. <span data-ttu-id="0a27a-118">Kliknij przycisk **Utwórz przepływem na podstawie puste**.</span><span class="sxs-lookup"><span data-stu-id="0a27a-118">Click **Create a flow from blank**.</span></span>

### <a name="step-2-create-a-trigger-for-your-flow"></a><span data-ttu-id="0a27a-119">Krok 2: Tworzenie wyzwalacza dla Twojego przepływu</span><span class="sxs-lookup"><span data-stu-id="0a27a-119">Step 2: Create a trigger for your flow</span></span>
1. <span data-ttu-id="0a27a-120">Wybierz **harmonogram**, a następnie wybierz **harmonogram - cyklu**.</span><span class="sxs-lookup"><span data-stu-id="0a27a-120">Select **Schedule**, and then select **Schedule - Recurrence**.</span></span>
2. <span data-ttu-id="0a27a-121">W hello **częstotliwość** wybierz opcję **dzień**i w hello **interwał** wprowadź **1**.</span><span class="sxs-lookup"><span data-stu-id="0a27a-121">In hello **Frequency** box, select **Day**, and in hello **Interval** box, enter **1**.</span></span>

    ![Okno dialogowe Microsoft Flow wyzwalacza](./media/app-insights-automate-with-flow/flow1.png)


### <a name="step-3-add-an-application-insights-action"></a><span data-ttu-id="0a27a-123">Krok 3: Dodaj akcję usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="0a27a-123">Step 3: Add an Application Insights action</span></span>
1. <span data-ttu-id="0a27a-124">Kliknij przycisk **nowy krok**, a następnie kliknij przycisk **Dodaj akcję**.</span><span class="sxs-lookup"><span data-stu-id="0a27a-124">Click **New step**, and then click **Add an action**.</span></span>
2. <span data-ttu-id="0a27a-125">Wyszukaj **Azure Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="0a27a-125">Search for **Azure Application Insights**.</span></span>
3. <span data-ttu-id="0a27a-126">Kliknij przycisk **Azure Application Insights — wizualizacji analizy zapytania Podgląd**.</span><span class="sxs-lookup"><span data-stu-id="0a27a-126">Click **Azure Application Insights – Visualize Analytics query Preview**.</span></span>

    ![Uruchom okno kwerendy analityka](./media/app-insights-automate-with-flow/flow2.png)

### <a name="step-4-connect-tooan-application-insights-resource"></a><span data-ttu-id="0a27a-128">Krok 4: Łączenie tooan zasobu usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="0a27a-128">Step 4: Connect tooan Application Insights resource</span></span>

<span data-ttu-id="0a27a-129">toocomplete ten krok, potrzebne są identyfikator i klucz interfejsu API dla zasobu.</span><span class="sxs-lookup"><span data-stu-id="0a27a-129">toocomplete this step, you need an application ID and an API key for your resource.</span></span> <span data-ttu-id="0a27a-130">Można je pobrać od hello portalu Azure, jak pokazano w powitania po diagramu:</span><span class="sxs-lookup"><span data-stu-id="0a27a-130">You can retrieve them from hello Azure portal, as shown in hello following diagram:</span></span>

![Identyfikator aplikacji w portalu Azure hello](./media/app-insights-automate-with-flow/appid.png) 

- <span data-ttu-id="0a27a-132">Podaj nazwę dla połączenia, wraz z hello aplikacji identyfikator i klucz API.</span><span class="sxs-lookup"><span data-stu-id="0a27a-132">Provide a name for your connection, along with hello application ID and API key.</span></span>

    ![Okno połączenia Flow firmy Microsoft](./media/app-insights-automate-with-flow/flow3.png)

### <a name="step-5-specify-hello-analytics-query-and-chart-type"></a><span data-ttu-id="0a27a-134">Krok 5: Określ hello Analytics zapytania i typ wykresu</span><span class="sxs-lookup"><span data-stu-id="0a27a-134">Step 5: Specify hello Analytics query and chart type</span></span>
<span data-ttu-id="0a27a-135">To przykładowe zapytanie wybiera w hello ostatni dzień żądania hello nie powiodło się i są powiązane z nimi wyjątków, które wystąpiły w ramach operacji hello.</span><span class="sxs-lookup"><span data-stu-id="0a27a-135">This example query selects hello failed requests within hello last day and correlates them with exceptions that occurred as part of hello operation.</span></span> <span data-ttu-id="0a27a-136">Analiza są powiązane z nimi na podstawie identyfikatora operation_Id hello.</span><span class="sxs-lookup"><span data-stu-id="0a27a-136">Analytics correlates them based on hello operation_Id identifier.</span></span> <span data-ttu-id="0a27a-137">Zapytanie Hello następnie segmenty hello wyniki za pomocą algorytmu autocluster hello.</span><span class="sxs-lookup"><span data-stu-id="0a27a-137">hello query then segments hello results by using hello autocluster algorithm.</span></span> 

<span data-ttu-id="0a27a-138">Podczas tworzenia własnych zapytań, sprawdź, czy działają prawidłowo w module analiz przed dodaniem tooyour przepływu.</span><span class="sxs-lookup"><span data-stu-id="0a27a-138">When you create your own queries, verify that they are working properly in Analytics before you add it tooyour flow.</span></span>

- <span data-ttu-id="0a27a-139">Dodaj hello następującego zapytania Analytics, a następnie wybierz typ wykresu tabeli HTML hello.</span><span class="sxs-lookup"><span data-stu-id="0a27a-139">Add hello following Analytics query, and then select hello HTML table chart type.</span></span> 

    ```
    requests
    | where timestamp > ago(1d)
    | where success == "False"
    | project name, operation_Id
    | join ( exceptions
        | project problemId, outerMessage, operation_Id
    ) on operation_Id
    | evaluate autocluster()
    ```
    
    ![Okno konfiguracji kwerendy analityka](./media/app-insights-automate-with-flow/flow4.png)

### <a name="step-6-configure-hello-flow-toosend-email"></a><span data-ttu-id="0a27a-141">Krok 6: Konfigurowanie hello przepływu toosend e-mail</span><span class="sxs-lookup"><span data-stu-id="0a27a-141">Step 6: Configure hello flow toosend email</span></span>

1. <span data-ttu-id="0a27a-142">Kliknij przycisk **nowy krok**, a następnie kliknij przycisk **Dodaj akcję**.</span><span class="sxs-lookup"><span data-stu-id="0a27a-142">Click **New step**, and then click **Add an action**.</span></span>
2. <span data-ttu-id="0a27a-143">Wyszukaj **Outlook pakietu Office 365**.</span><span class="sxs-lookup"><span data-stu-id="0a27a-143">Search for **Office 365 Outlook**.</span></span>
3. <span data-ttu-id="0a27a-144">Kliknij przycisk **Office 365 Outlook — Wyślij usługi poczty e-mail**.</span><span class="sxs-lookup"><span data-stu-id="0a27a-144">Click **Office 365 Outlook – Send an email**.</span></span>

    ![Okno wyboru Outlook pakietu Office 365](./media/app-insights-automate-with-flow/flow2b.png)

4. <span data-ttu-id="0a27a-146">W hello **wysłać wiadomość e-mail** oknie hello następujące:</span><span class="sxs-lookup"><span data-stu-id="0a27a-146">In hello **Send an email** window, do hello following:</span></span>

   <span data-ttu-id="0a27a-147">a.</span><span class="sxs-lookup"><span data-stu-id="0a27a-147">a.</span></span> <span data-ttu-id="0a27a-148">Wpisz adres e-mail adresata hello hello.</span><span class="sxs-lookup"><span data-stu-id="0a27a-148">Type hello email address of hello recipient.</span></span>

   <span data-ttu-id="0a27a-149">b.</span><span class="sxs-lookup"><span data-stu-id="0a27a-149">b.</span></span> <span data-ttu-id="0a27a-150">Wpisz temat hello poczty e-mail.</span><span class="sxs-lookup"><span data-stu-id="0a27a-150">Type a subject for hello email.</span></span>

   <span data-ttu-id="0a27a-151">c.</span><span class="sxs-lookup"><span data-stu-id="0a27a-151">c.</span></span> <span data-ttu-id="0a27a-152">Kliknij w dowolnym miejscu hello **treści** polu, a następnie na powitania dynamicznej zawartości wyświetlonym menu na powitania prawo, wybierz **treści**.</span><span class="sxs-lookup"><span data-stu-id="0a27a-152">Click anywhere in hello **Body** box and then, on hello dynamic content menu that opens at hello right, select **Body**.</span></span>

   <span data-ttu-id="0a27a-153">d.</span><span class="sxs-lookup"><span data-stu-id="0a27a-153">d.</span></span> <span data-ttu-id="0a27a-154">Kliknij przycisk **Pokaż zaawansowane opcje**.</span><span class="sxs-lookup"><span data-stu-id="0a27a-154">Click **Show advanced options**.</span></span>

    ![Konfiguracja programu Outlook pakietu Office 365](./media/app-insights-automate-with-flow/flow5.png)

5. <span data-ttu-id="0a27a-156">W menu hello dynamicznej zawartości hello następujące:</span><span class="sxs-lookup"><span data-stu-id="0a27a-156">On hello dynamic content menu, do hello following:</span></span>

    <span data-ttu-id="0a27a-157">a.</span><span class="sxs-lookup"><span data-stu-id="0a27a-157">a.</span></span> <span data-ttu-id="0a27a-158">Wybierz **Nazwa załącznika**.</span><span class="sxs-lookup"><span data-stu-id="0a27a-158">Select **Attachment Name**.</span></span>

    <span data-ttu-id="0a27a-159">b.</span><span class="sxs-lookup"><span data-stu-id="0a27a-159">b.</span></span> <span data-ttu-id="0a27a-160">Wybierz **zawartości załącznika**.</span><span class="sxs-lookup"><span data-stu-id="0a27a-160">Select **Attachment Content**.</span></span>
    
    <span data-ttu-id="0a27a-161">c.</span><span class="sxs-lookup"><span data-stu-id="0a27a-161">c.</span></span> <span data-ttu-id="0a27a-162">W hello **HTML jest** wybierz opcję **tak**.</span><span class="sxs-lookup"><span data-stu-id="0a27a-162">In hello **Is HTML** box, select **Yes**.</span></span>

    ![Okno Konfiguracja poczty e-mail usługi Office 365](./media/app-insights-automate-with-flow/flow7.png)

### <a name="step-7-save-and-test-your-flow"></a><span data-ttu-id="0a27a-164">Krok 7: Zapisz i testowania przepływu użytkownika</span><span class="sxs-lookup"><span data-stu-id="0a27a-164">Step 7: Save and test your flow</span></span>
- <span data-ttu-id="0a27a-165">W hello **nazwy przepływu** , Dodaj nazwę użytkownika przepływ, a następnie kliknij przycisk **utworzyć przepływ**.</span><span class="sxs-lookup"><span data-stu-id="0a27a-165">In hello **Flow name** box, add a name for your flow, and then click **Create flow**.</span></span>

    ![Tworzenie przepływu okna](./media/app-insights-automate-with-flow/flow8.png)

<span data-ttu-id="0a27a-167">Możesz poczekać na powitania wyzwalacza toorun tej akcji, lub uruchomić przepływ hello natychmiast przez [uruchomionych wyzwalacza hello na żądanie](https://flow.microsoft.com/blog/run-now-and-six-more-services/).</span><span class="sxs-lookup"><span data-stu-id="0a27a-167">You can wait for hello trigger toorun this action, or you can run hello flow immediately by [running hello trigger on demand](https://flow.microsoft.com/blog/run-now-and-six-more-services/).</span></span>

<span data-ttu-id="0a27a-168">Po uruchomieniu przepływu hello hello adresatów, określone na liście e-mail hello otrzymywać wiadomości e-mail, która wygląda hello:</span><span class="sxs-lookup"><span data-stu-id="0a27a-168">When hello flow runs, hello recipients you have specified in hello email list receive an email message that looks like hello following:</span></span>

![Przykładowej wiadomości e-mail](./media/app-insights-automate-with-flow/flow9.png)


## <a name="next-steps"></a><span data-ttu-id="0a27a-170">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="0a27a-170">Next steps</span></span>

- <span data-ttu-id="0a27a-171">Dowiedz się więcej o tworzeniu [zapytania analityczne](app-insights-analytics-using.md).</span><span class="sxs-lookup"><span data-stu-id="0a27a-171">Learn more about creating [Analytics queries](app-insights-analytics-using.md).</span></span>
- <span data-ttu-id="0a27a-172">Dowiedz się więcej o [Microsoft Flow](https://ms.flow.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="0a27a-172">Learn more about [Microsoft Flow](https://ms.flow.microsoft.com).</span></span>



<!--Link references-->





