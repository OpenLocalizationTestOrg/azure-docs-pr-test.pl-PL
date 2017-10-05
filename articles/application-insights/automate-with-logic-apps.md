---
title: "Zautomatyzować procesy Azure Application Insights przy użyciu Logic Apps."
description: "Dowiedz się, jak szybko można zautomatyzować powtarzalnych procesów przez dodanie łącznika usługi Application Insights do aplikacji logiki."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: bwren
ms.openlocfilehash: 36df5bc0a019f4197d40fd6fa5a2a9957820c8b4
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="automate-application-insights-processes-by-using-logic-apps"></a><span data-ttu-id="272cf-103">Zautomatyzować procesy usługi Application Insights przy użyciu aplikacji logiki</span><span class="sxs-lookup"><span data-stu-id="272cf-103">Automate Application Insights processes by using Logic Apps</span></span>

<span data-ttu-id="272cf-104">Czy zaczniesz wielokrotnego uruchamiania tej samej zapytań na podstawie danych telemetrii, aby sprawdzić, czy usługa działa prawidłowo?</span><span class="sxs-lookup"><span data-stu-id="272cf-104">Do you find yourself repeatedly running the same queries on your telemetry data to check whether your service is functioning properly?</span></span> <span data-ttu-id="272cf-105">Szukasz zautomatyzować te zapytania do znajdowania trendów i anomalii i późniejszego kompilowania własne przepływy pracy wokół nich?</span><span class="sxs-lookup"><span data-stu-id="272cf-105">Are you looking to automate these queries for finding trends and anomalies and then build your own workflows around them?</span></span> <span data-ttu-id="272cf-106">Łącznik usługi Azure Application Insights (wersja zapoznawcza) dla usługi Logic Apps jest właściwych narzędzi, w tym celu.</span><span class="sxs-lookup"><span data-stu-id="272cf-106">The Azure Application Insights connector (preview) for Logic Apps is the right tool for this purpose.</span></span>

<span data-ttu-id="272cf-107">Dzięki tej integracji można zautomatyzować wiele procesów bez pisania pojedynczy wiersz kodu.</span><span class="sxs-lookup"><span data-stu-id="272cf-107">With this integration, you can automate numerous processes without writing a single line of code.</span></span> <span data-ttu-id="272cf-108">Można utworzyć aplikację logiki z łącznikiem usługi Application Insights, aby szybko zautomatyzować każdy proces usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="272cf-108">You can create a logic app with the Application Insights connector to quickly automate any Application Insights process.</span></span> 

<span data-ttu-id="272cf-109">Można dodać również dodatkowe akcje.</span><span class="sxs-lookup"><span data-stu-id="272cf-109">You can add additional actions as well.</span></span> <span data-ttu-id="272cf-110">Funkcję Logic Apps w usłudze Azure App Service udostępnia setki akcje.</span><span class="sxs-lookup"><span data-stu-id="272cf-110">The Logic Apps feature of Azure App Service makes hundreds of actions available.</span></span> <span data-ttu-id="272cf-111">Na przykład za pomocą aplikacji logiki, możesz można automatycznie wysłać wiadomość e-mail z powiadomieniem lub tworzenie usterki w programie Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="272cf-111">For example, by using a logic app, you can automatically send an email notification or create a bug in Visual Studio Team Services.</span></span> <span data-ttu-id="272cf-112">Można także użyć jednego z wielu dostępne [szablony](https://docs.microsoft.com/azure/logic-apps/logic-apps-use-logic-app-templates) aby przyspieszyć proces tworzenia aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="272cf-112">You can also use one of the many available [templates](https://docs.microsoft.com/azure/logic-apps/logic-apps-use-logic-app-templates) to help speed up the process of creating your logic app.</span></span> 

## <a name="create-a-logic-app-for-application-insights"></a><span data-ttu-id="272cf-113">Tworzenie aplikacji logiki do usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="272cf-113">Create a logic app for Application Insights</span></span>

<span data-ttu-id="272cf-114">W tym samouczku Dowiedz się jak utworzyć aplikację logiki, która używa algorytmu autocluster Analytics grupy atrybutów danych dla aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="272cf-114">In this tutorial, you learn how to create a logic app that uses the Analytics autocluster algorithm to group attributes in the data for a web application.</span></span> <span data-ttu-id="272cf-115">Przepływ automatycznie wysyła wyniki za pośrednictwem poczty e-mail, tylko jeden przykład sposobu użycia Application Insights analizy i Logic Apps razem.</span><span class="sxs-lookup"><span data-stu-id="272cf-115">The flow automatically sends the results by email, just one example of how you can use Application Insights Analytics and Logic Apps together.</span></span> 

### <a name="step-1-create-a-logic-app"></a><span data-ttu-id="272cf-116">Krok 1: Tworzenie aplikacji logiki</span><span class="sxs-lookup"><span data-stu-id="272cf-116">Step 1: Create a logic app</span></span>
1. <span data-ttu-id="272cf-117">Zaloguj się w witrynie [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="272cf-117">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="272cf-118">W **nowy** okienku wybierz **sieci Web i mobilność**, a następnie wybierz **aplikacji logiki**.</span><span class="sxs-lookup"><span data-stu-id="272cf-118">In the **New** pane, select **Web + Mobile**, and then select **Logic App**.</span></span>

    ![Nowe okno aplikacji logiki](./media/automate-with-logic-apps/logicapp1.png)

### <a name="step-2-create-a-trigger-for-your-logic-app"></a><span data-ttu-id="272cf-120">Krok 2: Tworzenie aplikacji logiki wyzwalacza</span><span class="sxs-lookup"><span data-stu-id="272cf-120">Step 2: Create a trigger for your logic app</span></span>
1. <span data-ttu-id="272cf-121">W **projektanta aplikacji logiki** okna, w obszarze **rozpoczynać wyzwalacz wspólnej**, wybierz pozycję **cyklu**.</span><span class="sxs-lookup"><span data-stu-id="272cf-121">In the **Logic App Designer** window, under **Start with a common trigger**, select **Recurrence**.</span></span>

    ![Okna Projektant aplikacji logiki](./media/automate-with-logic-apps/logicapp2.png)

2. <span data-ttu-id="272cf-123">W **częstotliwość** wybierz opcję **dzień** , a następnie w **interwał** wpisz **1**.</span><span class="sxs-lookup"><span data-stu-id="272cf-123">In the **Frequency** box, select **Day** and then, in the **Interval** box, type **1**.</span></span>

    ![Projektant aplikacji logiki "Cyklu" okna](./media/automate-with-logic-apps/step2b.png)

### <a name="step-3-add-an-application-insights-action"></a><span data-ttu-id="272cf-125">Krok 3: Dodaj akcję usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="272cf-125">Step 3: Add an Application Insights action</span></span>
1. <span data-ttu-id="272cf-126">Kliknij przycisk **nowy krok**, a następnie kliknij przycisk **Dodaj akcję**.</span><span class="sxs-lookup"><span data-stu-id="272cf-126">Click **New step**, and then click **Add an action**.</span></span>

2. <span data-ttu-id="272cf-127">W **wybierz akcję** pole wyszukiwania, wpisz **Azure Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="272cf-127">In the **Choose an action** search box, type **Azure Application Insights**.</span></span>

3. <span data-ttu-id="272cf-128">W obszarze **akcje**, kliknij przycisk **Azure Application Insights — wizualizacji analizy zapytania Podgląd**.</span><span class="sxs-lookup"><span data-stu-id="272cf-128">Under **Actions**, click **Azure Application Insights – Visualize Analytics query Preview**.</span></span>

    ![Okno "Wybierz akcję" Projektant aplikacji logiki](./media/automate-with-logic-apps/flow2.png)

### <a name="step-4-connect-to-an-application-insights-resource"></a><span data-ttu-id="272cf-130">Krok 4: Łączenie z zasobu usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="272cf-130">Step 4: Connect to an Application Insights resource</span></span>

<span data-ttu-id="272cf-131">Aby ukończyć ten krok, należy identyfikator i klucz interfejsu API dla zasobu.</span><span class="sxs-lookup"><span data-stu-id="272cf-131">To complete this step, you need an application ID and an API key for your resource.</span></span> <span data-ttu-id="272cf-132">Można je pobrać z portalu Azure, jak pokazano na poniższym diagramie:</span><span class="sxs-lookup"><span data-stu-id="272cf-132">You can retrieve them from the Azure portal, as shown in the following diagram:</span></span>

![Identyfikator aplikacji w portalu Azure](./media/automate-with-logic-apps/appid.png) 

<span data-ttu-id="272cf-134">Podaj nazwę połączenia, identyfikator i klucz interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="272cf-134">Provide a name for your connection, the application ID, and the API key.</span></span>

![Logika Projektant aplikacji przepływu połączenia okna](./media/automate-with-logic-apps/flow3.png)

### <a name="step-5-specify-the-analytics-query-and-chart-type"></a><span data-ttu-id="272cf-136">Krok 5: Określ typ zapytania i wykres analizy</span><span class="sxs-lookup"><span data-stu-id="272cf-136">Step 5: Specify the Analytics query and chart type</span></span>
<span data-ttu-id="272cf-137">W poniższym przykładzie zapytanie wybiera żądań zakończonych niepowodzeniem w ciągu ostatniego dnia i są powiązane z nimi wyjątków, które wystąpiły w ramach operacji.</span><span class="sxs-lookup"><span data-stu-id="272cf-137">In the following example, the query selects the failed requests within the last day and correlates them with exceptions that occurred as part of the operation.</span></span> <span data-ttu-id="272cf-138">Analiza skorelowany nieudanych żądań, na podstawie identyfikatora operation_Id.</span><span class="sxs-lookup"><span data-stu-id="272cf-138">Analytics correlates the failed requests, based on the operation_Id identifier.</span></span> <span data-ttu-id="272cf-139">Zapytanie następnie segmentów wyników za pomocą algorytmu autocluster.</span><span class="sxs-lookup"><span data-stu-id="272cf-139">The query then segments the results by using the autocluster algorithm.</span></span> 

<span data-ttu-id="272cf-140">Podczas tworzenia własnych zapytań, sprawdź, czy działają prawidłowo w module analiz przed dodaniem go do Twojego przepływu.</span><span class="sxs-lookup"><span data-stu-id="272cf-140">When you create your own queries, verify that they are working properly in Analytics before you add it to your flow.</span></span>

1. <span data-ttu-id="272cf-141">W **zapytania** Dodaj następujące zapytanie Analytics:</span><span class="sxs-lookup"><span data-stu-id="272cf-141">In the **Query** box, add the following Analytics query:</span></span> 

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

2. <span data-ttu-id="272cf-142">W **typ wykresu** wybierz opcję **tabeli Html**.</span><span class="sxs-lookup"><span data-stu-id="272cf-142">In the **Chart Type** box, select **Html Table**.</span></span>

    ![Okno konfiguracji kwerendy analityka](./media/automate-with-logic-apps/flow4.png)

### <a name="step-6-configure-the-logic-app-to-send-email"></a><span data-ttu-id="272cf-144">Krok 6: Skonfigurowanie aplikacji logiki do wysyłania wiadomości e-mail</span><span class="sxs-lookup"><span data-stu-id="272cf-144">Step 6: Configure the logic app to send email</span></span>

1. <span data-ttu-id="272cf-145">Kliknij przycisk **nowy krok**, a następnie wybierz **Dodaj akcję**.</span><span class="sxs-lookup"><span data-stu-id="272cf-145">Click **New step**, and then select **Add an action**.</span></span>

2. <span data-ttu-id="272cf-146">W polu wyszukiwania wpisz **Office 365 Outlook**.</span><span class="sxs-lookup"><span data-stu-id="272cf-146">In the search box, type **Office 365 Outlook**.</span></span>

3. <span data-ttu-id="272cf-147">Kliknij przycisk **Office 365 Outlook — Wyślij usługi poczty e-mail**.</span><span class="sxs-lookup"><span data-stu-id="272cf-147">Click **Office 365 Outlook – Send an email**.</span></span>

    ![Wybór Outlook pakietu Office 365](./media/automate-with-logic-apps/flow2b.png)

4. <span data-ttu-id="272cf-149">W **wysłać wiadomość e-mail** okna, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="272cf-149">In the **Send an email** window, do the following:</span></span>

   <span data-ttu-id="272cf-150">a.</span><span class="sxs-lookup"><span data-stu-id="272cf-150">a.</span></span> <span data-ttu-id="272cf-151">Wpisz adres e-mail odbiorcy.</span><span class="sxs-lookup"><span data-stu-id="272cf-151">Type the email address of the recipient.</span></span>

   <span data-ttu-id="272cf-152">b.</span><span class="sxs-lookup"><span data-stu-id="272cf-152">b.</span></span> <span data-ttu-id="272cf-153">Wpisz temat wiadomości e-mail.</span><span class="sxs-lookup"><span data-stu-id="272cf-153">Type a subject for the email.</span></span>

   <span data-ttu-id="272cf-154">c.</span><span class="sxs-lookup"><span data-stu-id="272cf-154">c.</span></span> <span data-ttu-id="272cf-155">Kliknij w dowolnym miejscu **treści** polu, a następnie na dynamicznej zawartości wyświetlonym menu z prawej strony, wybierz **treści**.</span><span class="sxs-lookup"><span data-stu-id="272cf-155">Click anywhere in the **Body** box and then, on the dynamic content menu that opens at the right, select **Body**.</span></span>

   <span data-ttu-id="272cf-156">d.</span><span class="sxs-lookup"><span data-stu-id="272cf-156">d.</span></span> <span data-ttu-id="272cf-157">Kliknij przycisk **Pokaż zaawansowane opcje**.</span><span class="sxs-lookup"><span data-stu-id="272cf-157">Click **Show advanced options**.</span></span>

      ![Konfiguracja programu Outlook pakietu Office 365](./media/automate-with-logic-apps/flow5.png)

5. <span data-ttu-id="272cf-159">W menu zawartości dynamicznej wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="272cf-159">On the dynamic content menu, do the following:</span></span>

    <span data-ttu-id="272cf-160">a.</span><span class="sxs-lookup"><span data-stu-id="272cf-160">a.</span></span> <span data-ttu-id="272cf-161">Wybierz **Nazwa załącznika**.</span><span class="sxs-lookup"><span data-stu-id="272cf-161">Select **Attachment Name**.</span></span>

    <span data-ttu-id="272cf-162">b.</span><span class="sxs-lookup"><span data-stu-id="272cf-162">b.</span></span> <span data-ttu-id="272cf-163">Wybierz **zawartości załącznika**.</span><span class="sxs-lookup"><span data-stu-id="272cf-163">Select **Attachment Content**.</span></span>
    
    <span data-ttu-id="272cf-164">c.</span><span class="sxs-lookup"><span data-stu-id="272cf-164">c.</span></span> <span data-ttu-id="272cf-165">W **HTML jest** wybierz opcję **tak**.</span><span class="sxs-lookup"><span data-stu-id="272cf-165">In the **Is HTML** box, select **Yes**.</span></span>

      ![Ekran konfiguracji poczty e-mail usługi Office 365](./media/automate-with-logic-apps/flow7.png)

### <a name="step-7-save-and-test-your-logic-app"></a><span data-ttu-id="272cf-167">Krok 7: Zapisz i przetestuj aplikację logiki</span><span class="sxs-lookup"><span data-stu-id="272cf-167">Step 7: Save and test your logic app</span></span>
* <span data-ttu-id="272cf-168">Kliknij przycisk **zapisać** Aby zapisać zmiany.</span><span class="sxs-lookup"><span data-stu-id="272cf-168">Click **Save** to save your changes.</span></span>

<span data-ttu-id="272cf-169">Możesz poczekać trigger, aby uruchomić aplikację logiki, lub uruchom aplikację logiki natychmiast po wybraniu **Uruchom**.</span><span class="sxs-lookup"><span data-stu-id="272cf-169">You can wait for the trigger to run the logic app, or you can run the logic app immediately by selecting **Run**.</span></span>

![Ekran Tworzenie aplikacji logiki](./media/automate-with-logic-apps/step7.png)

<span data-ttu-id="272cf-171">Po uruchomieniu aplikacji logiki, odbiorcy, określone na liście wiadomości e-mail będą otrzymywać wiadomości e-mail, która wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="272cf-171">When your logic app runs, the recipients you specified in the email list will receive an email that looks like the following:</span></span>

![Wiadomość e-mail aplikacji logiki](./media/automate-with-logic-apps/flow9.png)

## <a name="next-steps"></a><span data-ttu-id="272cf-173">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="272cf-173">Next steps</span></span>

- <span data-ttu-id="272cf-174">Dowiedz się więcej o tworzeniu [zapytania analityczne](app-insights-analytics-using.md).</span><span class="sxs-lookup"><span data-stu-id="272cf-174">Learn more about creating [Analytics queries](app-insights-analytics-using.md).</span></span>
- <span data-ttu-id="272cf-175">Dowiedz się więcej o [Logic Apps](https://docs.microsoft.com/azure/logic-apps/logic-apps-what-are-logic-apps).</span><span class="sxs-lookup"><span data-stu-id="272cf-175">Learn more about [Logic Apps](https://docs.microsoft.com/azure/logic-apps/logic-apps-what-are-logic-apps).</span></span>



<!--Link references-->





