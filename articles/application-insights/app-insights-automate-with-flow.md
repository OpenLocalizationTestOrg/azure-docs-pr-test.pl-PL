---
title: "Automatyzowanie procesów Azure Application Insights z Flow firmy Microsoft"
description: "Dowiedz się, jak można użyć Microsoft Flow można szybko zautomatyzować powtarzalnych procesów za pomocą łącznika usługi Application Insights."
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
ms.openlocfilehash: 510f4f284bbd0dbe4171896899f7ade7dee19e39
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="automate-azure-application-insights-processes-with-the-connector-for-microsoft-flow"></a><span data-ttu-id="64ba3-103">Zautomatyzować procesy Azure Application Insights z łącznikiem Flow firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="64ba3-103">Automate Azure Application Insights processes with the connector for Microsoft Flow</span></span>

<span data-ttu-id="64ba3-104">Czy zaczniesz wielokrotnego uruchamiania tej samej zapytań na podstawie danych telemetrii, aby sprawdzić, czy usługa działa prawidłowo?</span><span class="sxs-lookup"><span data-stu-id="64ba3-104">Do you find yourself repeatedly running the same queries on your telemetry data to check that your service is functioning properly?</span></span> <span data-ttu-id="64ba3-105">Szukasz zautomatyzować te zapytania do znajdowania trendów i anomalii i późniejszego kompilowania własne przepływy pracy wokół nich?</span><span class="sxs-lookup"><span data-stu-id="64ba3-105">Are you looking to automate these queries for finding trends and anomalies and then build your own workflows around them?</span></span> <span data-ttu-id="64ba3-106">Łącznik usługi Azure Application Insights (wersja zapoznawcza) dla Flow firmy Microsoft jest właściwych narzędzi dla tych celów.</span><span class="sxs-lookup"><span data-stu-id="64ba3-106">The Azure Application Insights connector (preview) for Microsoft Flow is the right tool for these purposes.</span></span>

<span data-ttu-id="64ba3-107">Dzięki tej integracji teraz można zautomatyzować wiele procesów bez pisania pojedynczy wiersz kodu.</span><span class="sxs-lookup"><span data-stu-id="64ba3-107">With this integration, you can now automate numerous processes without writing a single line of code.</span></span> <span data-ttu-id="64ba3-108">Po utworzeniu przepływu za pomocą akcji usługi Application Insights przepływ automatycznie uruchamia kwerendy analizy wgląd w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="64ba3-108">After you create a flow by using an Application Insights action, the flow automatically runs your Application Insights Analytics query.</span></span> 

<span data-ttu-id="64ba3-109">Można dodać również dodatkowe akcje.</span><span class="sxs-lookup"><span data-stu-id="64ba3-109">You can add additional actions as well.</span></span> <span data-ttu-id="64ba3-110">Microsoft Flow udostępnia setki akcje.</span><span class="sxs-lookup"><span data-stu-id="64ba3-110">Microsoft Flow makes hundreds of actions available.</span></span> <span data-ttu-id="64ba3-111">Na przykład można użyć Microsoft Flow można automatycznie wysłać wiadomość e-mail z powiadomieniem lub tworzenie usterki w programie Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="64ba3-111">For example, you can use Microsoft Flow to automatically send an email notification or create a bug in Visual Studio Team Services.</span></span> <span data-ttu-id="64ba3-112">Można także użyć jednego z wielu [szablony](https://ms.flow.microsoft.com/en-us/connectors/shared_applicationinsights/?slug=azure-application-insights) dostępnych dla łącznika Microsoft Flow.</span><span class="sxs-lookup"><span data-stu-id="64ba3-112">You can also use one of the many [templates](https://ms.flow.microsoft.com/en-us/connectors/shared_applicationinsights/?slug=azure-application-insights) that are available for the connector for Microsoft Flow.</span></span> <span data-ttu-id="64ba3-113">Te szablony przyspieszyć proces tworzenia przepływu.</span><span class="sxs-lookup"><span data-stu-id="64ba3-113">These templates speed up the process of creating a flow.</span></span> 

<!--The Application Insights connector also works with [Azure Power Apps](https://powerapps.microsoft.com/en-us/) and [Azure Logic Apps](https://azure.microsoft.com/services/logic-apps/?v=17.23h). --> 

## <a name="create-a-flow-for-application-insights"></a><span data-ttu-id="64ba3-114">Utwórz strumień dla usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="64ba3-114">Create a flow for Application Insights</span></span>

<span data-ttu-id="64ba3-115">Z tego samouczka dowiesz się, jak utworzyć przepływ, który używa algorytmu klastra automatycznie Analytics grupy atrybutów w danych dla aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="64ba3-115">In this tutorial, you will learn how to create a flow that uses the Analytics auto-cluster algorithm to group attributes in the data for a web application.</span></span> <span data-ttu-id="64ba3-116">Przepływ automatycznie wysyła wyniki za pośrednictwem poczty e-mail, tylko jeden przykład sposobu użycia Flow firmy Microsoft i analizy aplikacji Insights ze sobą.</span><span class="sxs-lookup"><span data-stu-id="64ba3-116">The flow automatically sends the results by email, just one example of how you can use Microsoft Flow and Application Insights Analytics together.</span></span> 

### <a name="step-1-create-a-flow"></a><span data-ttu-id="64ba3-117">Krok 1: Tworzenie przepływu</span><span class="sxs-lookup"><span data-stu-id="64ba3-117">Step 1: Create a flow</span></span>
1. <span data-ttu-id="64ba3-118">Zaloguj się do [Microsoft Flow](http://flow.microsoft.com), a następnie wybierz **Moje przepływa**.</span><span class="sxs-lookup"><span data-stu-id="64ba3-118">Sign in to [Microsoft Flow](http://flow.microsoft.com), and then select **My Flows**.</span></span>
2. <span data-ttu-id="64ba3-119">Kliknij przycisk **Utwórz przepływem na podstawie puste**.</span><span class="sxs-lookup"><span data-stu-id="64ba3-119">Click **Create a flow from blank**.</span></span>

### <a name="step-2-create-a-trigger-for-your-flow"></a><span data-ttu-id="64ba3-120">Krok 2: Tworzenie wyzwalacza dla Twojego przepływu</span><span class="sxs-lookup"><span data-stu-id="64ba3-120">Step 2: Create a trigger for your flow</span></span>
1. <span data-ttu-id="64ba3-121">Wybierz **harmonogram**, a następnie wybierz **harmonogram - cyklu**.</span><span class="sxs-lookup"><span data-stu-id="64ba3-121">Select **Schedule**, and then select **Schedule - Recurrence**.</span></span>
2. <span data-ttu-id="64ba3-122">W **częstotliwość** wybierz opcję **dzień**, a następnie w **interwał** wprowadź **1**.</span><span class="sxs-lookup"><span data-stu-id="64ba3-122">In the **Frequency** box, select **Day**, and in the **Interval** box, enter **1**.</span></span>

    ![Okno dialogowe Microsoft Flow wyzwalacza](./media/app-insights-automate-with-flow/flow1.png)


### <a name="step-3-add-an-application-insights-action"></a><span data-ttu-id="64ba3-124">Krok 3: Dodaj akcję usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="64ba3-124">Step 3: Add an Application Insights action</span></span>
1. <span data-ttu-id="64ba3-125">Kliknij przycisk **nowy krok**, a następnie kliknij przycisk **Dodaj akcję**.</span><span class="sxs-lookup"><span data-stu-id="64ba3-125">Click **New step**, and then click **Add an action**.</span></span>
2. <span data-ttu-id="64ba3-126">Wyszukaj **Azure Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="64ba3-126">Search for **Azure Application Insights**.</span></span>
3. <span data-ttu-id="64ba3-127">Kliknij przycisk **Azure Application Insights — wizualizacji analizy zapytania Podgląd**.</span><span class="sxs-lookup"><span data-stu-id="64ba3-127">Click **Azure Application Insights – Visualize Analytics query Preview**.</span></span>

    ![Uruchom okno kwerendy analityka](./media/app-insights-automate-with-flow/flow2.png)

### <a name="step-4-connect-to-an-application-insights-resource"></a><span data-ttu-id="64ba3-129">Krok 4: Łączenie z zasobu usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="64ba3-129">Step 4: Connect to an Application Insights resource</span></span>

<span data-ttu-id="64ba3-130">Aby ukończyć ten krok, należy identyfikator i klucz interfejsu API dla zasobu.</span><span class="sxs-lookup"><span data-stu-id="64ba3-130">To complete this step, you need an application ID and an API key for your resource.</span></span> <span data-ttu-id="64ba3-131">Można je pobrać z portalu Azure, jak pokazano na poniższym diagramie:</span><span class="sxs-lookup"><span data-stu-id="64ba3-131">You can retrieve them from the Azure portal, as shown in the following diagram:</span></span>

![Identyfikator aplikacji w portalu Azure](./media/app-insights-automate-with-flow/appid.png) 

- <span data-ttu-id="64ba3-133">Podaj nazwę dla połączenia, wraz z kluczem interfejsów API i identyfikator aplikacji.</span><span class="sxs-lookup"><span data-stu-id="64ba3-133">Provide a name for your connection, along with the application ID and API key.</span></span>

    ![Okno połączenia Flow firmy Microsoft](./media/app-insights-automate-with-flow/flow3.png)

### <a name="step-5-specify-the-analytics-query-and-chart-type"></a><span data-ttu-id="64ba3-135">Krok 5: Określ typ zapytania i wykres analizy</span><span class="sxs-lookup"><span data-stu-id="64ba3-135">Step 5: Specify the Analytics query and chart type</span></span>
<span data-ttu-id="64ba3-136">To przykładowe zapytanie wybiera żądań zakończonych niepowodzeniem w ciągu ostatniego dnia i są powiązane z nimi wyjątków, które wystąpiły w ramach operacji.</span><span class="sxs-lookup"><span data-stu-id="64ba3-136">This example query selects the failed requests within the last day and correlates them with exceptions that occurred as part of the operation.</span></span> <span data-ttu-id="64ba3-137">Analiza są powiązane z nimi na podstawie identyfikatora operation_Id.</span><span class="sxs-lookup"><span data-stu-id="64ba3-137">Analytics correlates them based on the operation_Id identifier.</span></span> <span data-ttu-id="64ba3-138">Zapytanie następnie segmentów wyników za pomocą algorytmu autocluster.</span><span class="sxs-lookup"><span data-stu-id="64ba3-138">The query then segments the results by using the autocluster algorithm.</span></span> 

<span data-ttu-id="64ba3-139">Podczas tworzenia własnych zapytań, sprawdź, czy działają prawidłowo w module analiz przed dodaniem go do Twojego przepływu.</span><span class="sxs-lookup"><span data-stu-id="64ba3-139">When you create your own queries, verify that they are working properly in Analytics before you add it to your flow.</span></span>

- <span data-ttu-id="64ba3-140">Dodaj następujące zapytanie Analytics, a następnie wybierz typ wykresu tabeli HTML.</span><span class="sxs-lookup"><span data-stu-id="64ba3-140">Add the following Analytics query, and then select the HTML table chart type.</span></span> 

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

### <a name="step-6-configure-the-flow-to-send-email"></a><span data-ttu-id="64ba3-142">Krok 6: Konfigurowanie przepływu do wysyłania wiadomości e-mail</span><span class="sxs-lookup"><span data-stu-id="64ba3-142">Step 6: Configure the flow to send email</span></span>

1. <span data-ttu-id="64ba3-143">Kliknij przycisk **nowy krok**, a następnie kliknij przycisk **Dodaj akcję**.</span><span class="sxs-lookup"><span data-stu-id="64ba3-143">Click **New step**, and then click **Add an action**.</span></span>
2. <span data-ttu-id="64ba3-144">Wyszukaj **Outlook pakietu Office 365**.</span><span class="sxs-lookup"><span data-stu-id="64ba3-144">Search for **Office 365 Outlook**.</span></span>
3. <span data-ttu-id="64ba3-145">Kliknij przycisk **Office 365 Outlook — Wyślij usługi poczty e-mail**.</span><span class="sxs-lookup"><span data-stu-id="64ba3-145">Click **Office 365 Outlook – Send an email**.</span></span>

    ![Okno wyboru Outlook pakietu Office 365](./media/app-insights-automate-with-flow/flow2b.png)

4. <span data-ttu-id="64ba3-147">W **wysłać wiadomość e-mail** okna, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="64ba3-147">In the **Send an email** window, do the following:</span></span>

   <span data-ttu-id="64ba3-148">a.</span><span class="sxs-lookup"><span data-stu-id="64ba3-148">a.</span></span> <span data-ttu-id="64ba3-149">Wpisz adres e-mail odbiorcy.</span><span class="sxs-lookup"><span data-stu-id="64ba3-149">Type the email address of the recipient.</span></span>

   <span data-ttu-id="64ba3-150">b.</span><span class="sxs-lookup"><span data-stu-id="64ba3-150">b.</span></span> <span data-ttu-id="64ba3-151">Wpisz temat wiadomości e-mail.</span><span class="sxs-lookup"><span data-stu-id="64ba3-151">Type a subject for the email.</span></span>

   <span data-ttu-id="64ba3-152">c.</span><span class="sxs-lookup"><span data-stu-id="64ba3-152">c.</span></span> <span data-ttu-id="64ba3-153">Kliknij w dowolnym miejscu **treści** polu, a następnie na dynamicznej zawartości wyświetlonym menu z prawej strony, wybierz **treści**.</span><span class="sxs-lookup"><span data-stu-id="64ba3-153">Click anywhere in the **Body** box and then, on the dynamic content menu that opens at the right, select **Body**.</span></span>

   <span data-ttu-id="64ba3-154">d.</span><span class="sxs-lookup"><span data-stu-id="64ba3-154">d.</span></span> <span data-ttu-id="64ba3-155">Kliknij przycisk **Pokaż zaawansowane opcje**.</span><span class="sxs-lookup"><span data-stu-id="64ba3-155">Click **Show advanced options**.</span></span>

    ![Konfiguracja programu Outlook pakietu Office 365](./media/app-insights-automate-with-flow/flow5.png)

5. <span data-ttu-id="64ba3-157">W menu zawartości dynamicznej wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="64ba3-157">On the dynamic content menu, do the following:</span></span>

    <span data-ttu-id="64ba3-158">a.</span><span class="sxs-lookup"><span data-stu-id="64ba3-158">a.</span></span> <span data-ttu-id="64ba3-159">Wybierz **Nazwa załącznika**.</span><span class="sxs-lookup"><span data-stu-id="64ba3-159">Select **Attachment Name**.</span></span>

    <span data-ttu-id="64ba3-160">b.</span><span class="sxs-lookup"><span data-stu-id="64ba3-160">b.</span></span> <span data-ttu-id="64ba3-161">Wybierz **zawartości załącznika**.</span><span class="sxs-lookup"><span data-stu-id="64ba3-161">Select **Attachment Content**.</span></span>
    
    <span data-ttu-id="64ba3-162">c.</span><span class="sxs-lookup"><span data-stu-id="64ba3-162">c.</span></span> <span data-ttu-id="64ba3-163">W **HTML jest** wybierz opcję **tak**.</span><span class="sxs-lookup"><span data-stu-id="64ba3-163">In the **Is HTML** box, select **Yes**.</span></span>

    ![Okno Konfiguracja poczty e-mail usługi Office 365](./media/app-insights-automate-with-flow/flow7.png)

### <a name="step-7-save-and-test-your-flow"></a><span data-ttu-id="64ba3-165">Krok 7: Zapisz i testowania przepływu użytkownika</span><span class="sxs-lookup"><span data-stu-id="64ba3-165">Step 7: Save and test your flow</span></span>
- <span data-ttu-id="64ba3-166">W **nazwy przepływu** , Dodaj nazwę użytkownika przepływ, a następnie kliknij przycisk **utworzyć przepływ**.</span><span class="sxs-lookup"><span data-stu-id="64ba3-166">In the **Flow name** box, add a name for your flow, and then click **Create flow**.</span></span>

    ![Tworzenie przepływu okna](./media/app-insights-automate-with-flow/flow8.png)

<span data-ttu-id="64ba3-168">Możesz poczekać wyzwalacz do uruchomienia tej akcji, lub uruchomić przepływ natychmiast przez [systemem wyzwalacz na żądanie](https://flow.microsoft.com/blog/run-now-and-six-more-services/).</span><span class="sxs-lookup"><span data-stu-id="64ba3-168">You can wait for the trigger to run this action, or you can run the flow immediately by [running the trigger on demand](https://flow.microsoft.com/blog/run-now-and-six-more-services/).</span></span>

<span data-ttu-id="64ba3-169">Po uruchomieniu przepływu określone na liście e-mail adresatów otrzymywać wiadomości e-mail, która wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="64ba3-169">When the flow runs, the recipients you have specified in the email list receive an email message that looks like the following:</span></span>

![Przykładowej wiadomości e-mail](./media/app-insights-automate-with-flow/flow9.png)


## <a name="next-steps"></a><span data-ttu-id="64ba3-171">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="64ba3-171">Next steps</span></span>

- <span data-ttu-id="64ba3-172">Dowiedz się więcej o tworzeniu [zapytania analityczne](app-insights-analytics-using.md).</span><span class="sxs-lookup"><span data-stu-id="64ba3-172">Learn more about creating [Analytics queries](app-insights-analytics-using.md).</span></span>
- <span data-ttu-id="64ba3-173">Dowiedz się więcej o [Microsoft Flow](https://ms.flow.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="64ba3-173">Learn more about [Microsoft Flow](https://ms.flow.microsoft.com).</span></span>



<!--Link references-->





