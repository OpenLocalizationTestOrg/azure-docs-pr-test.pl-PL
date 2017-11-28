---
title: "aaaAutomate Azure Application Insights przetwarza przy użyciu Logic Apps."
description: "Dowiedz się, jak szybko można zautomatyzować powtarzalnych procesów przez dodanie aplikacji logiki tooyour hello usługi Application Insights łącznika."
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
ms.openlocfilehash: 8565aadf0644ffb10da8a0964821901907db2e27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="automate-application-insights-processes-by-using-logic-apps"></a><span data-ttu-id="4e8fe-103">Zautomatyzować procesy usługi Application Insights przy użyciu aplikacji logiki</span><span class="sxs-lookup"><span data-stu-id="4e8fe-103">Automate Application Insights processes by using Logic Apps</span></span>

<span data-ttu-id="4e8fe-104">Czy zaczniesz wielokrotnie systemem hello tego samego zapytania z toocheck danych telemetrycznych czy usługa działa prawidłowo?</span><span class="sxs-lookup"><span data-stu-id="4e8fe-104">Do you find yourself repeatedly running hello same queries on your telemetry data toocheck whether your service is functioning properly?</span></span> <span data-ttu-id="4e8fe-105">Następnie tworzenia własnych przepływów pracy wokół nich i są wyglądającej tooautomate te zapytania do znajdowania trendów i anomalii? Hello łącznika usługi Azure Application Insights (wersja zapoznawcza) dla usługi Logic Apps jest hello właściwych narzędzi, w tym celu.</span><span class="sxs-lookup"><span data-stu-id="4e8fe-105">Are you looking tooautomate these queries for finding trends and anomalies and then build your own workflows around them? hello Azure Application Insights connector (preview) for Logic Apps is hello right tool for this purpose.</span></span>

<span data-ttu-id="4e8fe-106">Dzięki tej integracji można zautomatyzować wiele procesów bez pisania pojedynczy wiersz kodu.</span><span class="sxs-lookup"><span data-stu-id="4e8fe-106">With this integration, you can automate numerous processes without writing a single line of code.</span></span> <span data-ttu-id="4e8fe-107">Możesz utworzyć aplikację logiki za pomocą usługi Application Insights hello tooquickly łącznika automatyzować każdy proces usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="4e8fe-107">You can create a logic app with hello Application Insights connector tooquickly automate any Application Insights process.</span></span> 

<span data-ttu-id="4e8fe-108">Można dodać również dodatkowe akcje.</span><span class="sxs-lookup"><span data-stu-id="4e8fe-108">You can add additional actions as well.</span></span> <span data-ttu-id="4e8fe-109">Funkcja Logic Apps Hello Azure App Service udostępnia setki akcje.</span><span class="sxs-lookup"><span data-stu-id="4e8fe-109">hello Logic Apps feature of Azure App Service makes hundreds of actions available.</span></span> <span data-ttu-id="4e8fe-110">Na przykład za pomocą aplikacji logiki, możesz można automatycznie wysłać wiadomość e-mail z powiadomieniem lub tworzenie usterki w programie Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="4e8fe-110">For example, by using a logic app, you can automatically send an email notification or create a bug in Visual Studio Team Services.</span></span> <span data-ttu-id="4e8fe-111">Umożliwia także jedną hello wiele dostępnych [szablony](https://docs.microsoft.com/azure/logic-apps/logic-apps-use-logic-app-templates) toohelp przyspieszenia hello proces tworzenia aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="4e8fe-111">You can also use one of hello many available [templates](https://docs.microsoft.com/azure/logic-apps/logic-apps-use-logic-app-templates) toohelp speed up hello process of creating your logic app.</span></span> 

## <a name="create-a-logic-app-for-application-insights"></a><span data-ttu-id="4e8fe-112">Tworzenie aplikacji logiki do usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="4e8fe-112">Create a logic app for Application Insights</span></span>

<span data-ttu-id="4e8fe-113">Z tego samouczka dowiesz się, jak toocreate aplikacji logiki, który używa hello Analytics autocluster algorytm toogroup atrybutów w hello danych dla aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="4e8fe-113">In this tutorial, you learn how toocreate a logic app that uses hello Analytics autocluster algorithm toogroup attributes in hello data for a web application.</span></span> <span data-ttu-id="4e8fe-114">Przepływ Hello automatycznie wysyła wyników hello za pośrednictwem poczty e-mail, tylko jeden przykład sposobu użycia Application Insights analizy i Logic Apps razem.</span><span class="sxs-lookup"><span data-stu-id="4e8fe-114">hello flow automatically sends hello results by email, just one example of how you can use Application Insights Analytics and Logic Apps together.</span></span> 

### <a name="step-1-create-a-logic-app"></a><span data-ttu-id="4e8fe-115">Krok 1: Tworzenie aplikacji logiki</span><span class="sxs-lookup"><span data-stu-id="4e8fe-115">Step 1: Create a logic app</span></span>
1. <span data-ttu-id="4e8fe-116">Zaloguj się toohello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4e8fe-116">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="4e8fe-117">W hello **nowy** okienku wybierz **sieci Web i mobilność**, a następnie wybierz **aplikacji logiki**.</span><span class="sxs-lookup"><span data-stu-id="4e8fe-117">In hello **New** pane, select **Web + Mobile**, and then select **Logic App**.</span></span>

    ![Nowe okno aplikacji logiki](./media/automate-with-logic-apps/logicapp1.png)

### <a name="step-2-create-a-trigger-for-your-logic-app"></a><span data-ttu-id="4e8fe-119">Krok 2: Tworzenie aplikacji logiki wyzwalacza</span><span class="sxs-lookup"><span data-stu-id="4e8fe-119">Step 2: Create a trigger for your logic app</span></span>
1. <span data-ttu-id="4e8fe-120">W hello **projektanta aplikacji logiki** okna, w obszarze **rozpoczynać wyzwalacz wspólnej**, wybierz pozycję **cyklu**.</span><span class="sxs-lookup"><span data-stu-id="4e8fe-120">In hello **Logic App Designer** window, under **Start with a common trigger**, select **Recurrence**.</span></span>

    ![Okna Projektant aplikacji logiki](./media/automate-with-logic-apps/logicapp2.png)

2. <span data-ttu-id="4e8fe-122">W hello **częstotliwość** wybierz opcję **dzień** , a następnie w hello **interwał** wpisz **1**.</span><span class="sxs-lookup"><span data-stu-id="4e8fe-122">In hello **Frequency** box, select **Day** and then, in hello **Interval** box, type **1**.</span></span>

    ![Projektant aplikacji logiki "Cyklu" okna](./media/automate-with-logic-apps/step2b.png)

### <a name="step-3-add-an-application-insights-action"></a><span data-ttu-id="4e8fe-124">Krok 3: Dodaj akcję usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="4e8fe-124">Step 3: Add an Application Insights action</span></span>
1. <span data-ttu-id="4e8fe-125">Kliknij przycisk **nowy krok**, a następnie kliknij przycisk **Dodaj akcję**.</span><span class="sxs-lookup"><span data-stu-id="4e8fe-125">Click **New step**, and then click **Add an action**.</span></span>

2. <span data-ttu-id="4e8fe-126">W hello **wybierz akcję** pole wyszukiwania, wpisz **Azure Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="4e8fe-126">In hello **Choose an action** search box, type **Azure Application Insights**.</span></span>

3. <span data-ttu-id="4e8fe-127">W obszarze **akcje**, kliknij przycisk **Azure Application Insights — wizualizacji analizy zapytania Podgląd**.</span><span class="sxs-lookup"><span data-stu-id="4e8fe-127">Under **Actions**, click **Azure Application Insights – Visualize Analytics query Preview**.</span></span>

    ![Okno "Wybierz akcję" Projektant aplikacji logiki](./media/automate-with-logic-apps/flow2.png)

### <a name="step-4-connect-tooan-application-insights-resource"></a><span data-ttu-id="4e8fe-129">Krok 4: Łączenie tooan zasobu usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="4e8fe-129">Step 4: Connect tooan Application Insights resource</span></span>

<span data-ttu-id="4e8fe-130">toocomplete ten krok, potrzebne są identyfikator i klucz interfejsu API dla zasobu.</span><span class="sxs-lookup"><span data-stu-id="4e8fe-130">toocomplete this step, you need an application ID and an API key for your resource.</span></span> <span data-ttu-id="4e8fe-131">Można je pobrać od hello portalu Azure, jak pokazano w powitania po diagramu:</span><span class="sxs-lookup"><span data-stu-id="4e8fe-131">You can retrieve them from hello Azure portal, as shown in hello following diagram:</span></span>

![Identyfikator aplikacji w portalu Azure hello](./media/automate-with-logic-apps/appid.png) 

<span data-ttu-id="4e8fe-133">Podaj nazwę dla połączenia, identyfikator aplikacji hello i hello klucz interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="4e8fe-133">Provide a name for your connection, hello application ID, and hello API key.</span></span>

![Logika Projektant aplikacji przepływu połączenia okna](./media/automate-with-logic-apps/flow3.png)

### <a name="step-5-specify-hello-analytics-query-and-chart-type"></a><span data-ttu-id="4e8fe-135">Krok 5: Określ hello Analytics zapytania i typ wykresu</span><span class="sxs-lookup"><span data-stu-id="4e8fe-135">Step 5: Specify hello Analytics query and chart type</span></span>
<span data-ttu-id="4e8fe-136">W hello poniższy przykład zapytania hello wybiera w hello ostatni dzień żądania hello nie powiodło się i są powiązane z nimi wyjątków, które wystąpiły w ramach operacji hello.</span><span class="sxs-lookup"><span data-stu-id="4e8fe-136">In hello following example, hello query selects hello failed requests within hello last day and correlates them with exceptions that occurred as part of hello operation.</span></span> <span data-ttu-id="4e8fe-137">Żądania hello nie powiodło się, na podstawie identyfikatora operation_Id hello są powiązane z analizy.</span><span class="sxs-lookup"><span data-stu-id="4e8fe-137">Analytics correlates hello failed requests, based on hello operation_Id identifier.</span></span> <span data-ttu-id="4e8fe-138">Zapytanie Hello następnie segmenty hello wyniki za pomocą algorytmu autocluster hello.</span><span class="sxs-lookup"><span data-stu-id="4e8fe-138">hello query then segments hello results by using hello autocluster algorithm.</span></span> 

<span data-ttu-id="4e8fe-139">Podczas tworzenia własnych zapytań, sprawdź, czy działają prawidłowo w module analiz przed dodaniem tooyour przepływu.</span><span class="sxs-lookup"><span data-stu-id="4e8fe-139">When you create your own queries, verify that they are working properly in Analytics before you add it tooyour flow.</span></span>

1. <span data-ttu-id="4e8fe-140">W hello **zapytania** Dodaj hello następującego zapytania Analytics:</span><span class="sxs-lookup"><span data-stu-id="4e8fe-140">In hello **Query** box, add hello following Analytics query:</span></span> 

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

2. <span data-ttu-id="4e8fe-141">W hello **typ wykresu** wybierz opcję **tabeli Html**.</span><span class="sxs-lookup"><span data-stu-id="4e8fe-141">In hello **Chart Type** box, select **Html Table**.</span></span>

    ![Okno konfiguracji kwerendy analityka](./media/automate-with-logic-apps/flow4.png)

### <a name="step-6-configure-hello-logic-app-toosend-email"></a><span data-ttu-id="4e8fe-143">Krok 6: Konfigurowanie hello logiki aplikacji toosend w wiadomości e-mail</span><span class="sxs-lookup"><span data-stu-id="4e8fe-143">Step 6: Configure hello logic app toosend email</span></span>

1. <span data-ttu-id="4e8fe-144">Kliknij przycisk **nowy krok**, a następnie wybierz **Dodaj akcję**.</span><span class="sxs-lookup"><span data-stu-id="4e8fe-144">Click **New step**, and then select **Add an action**.</span></span>

2. <span data-ttu-id="4e8fe-145">W polu wyszukiwania hello wpisz **Office 365 Outlook**.</span><span class="sxs-lookup"><span data-stu-id="4e8fe-145">In hello search box, type **Office 365 Outlook**.</span></span>

3. <span data-ttu-id="4e8fe-146">Kliknij przycisk **Office 365 Outlook — Wyślij usługi poczty e-mail**.</span><span class="sxs-lookup"><span data-stu-id="4e8fe-146">Click **Office 365 Outlook – Send an email**.</span></span>

    ![Wybór Outlook pakietu Office 365](./media/automate-with-logic-apps/flow2b.png)

4. <span data-ttu-id="4e8fe-148">W hello **wysłać wiadomość e-mail** oknie hello następujące:</span><span class="sxs-lookup"><span data-stu-id="4e8fe-148">In hello **Send an email** window, do hello following:</span></span>

   <span data-ttu-id="4e8fe-149">a.</span><span class="sxs-lookup"><span data-stu-id="4e8fe-149">a.</span></span> <span data-ttu-id="4e8fe-150">Wpisz adres e-mail adresata hello hello.</span><span class="sxs-lookup"><span data-stu-id="4e8fe-150">Type hello email address of hello recipient.</span></span>

   <span data-ttu-id="4e8fe-151">b.</span><span class="sxs-lookup"><span data-stu-id="4e8fe-151">b.</span></span> <span data-ttu-id="4e8fe-152">Wpisz temat hello poczty e-mail.</span><span class="sxs-lookup"><span data-stu-id="4e8fe-152">Type a subject for hello email.</span></span>

   <span data-ttu-id="4e8fe-153">c.</span><span class="sxs-lookup"><span data-stu-id="4e8fe-153">c.</span></span> <span data-ttu-id="4e8fe-154">Kliknij w dowolnym miejscu hello **treści** polu, a następnie na powitania dynamicznej zawartości wyświetlonym menu na powitania prawo, wybierz **treści**.</span><span class="sxs-lookup"><span data-stu-id="4e8fe-154">Click anywhere in hello **Body** box and then, on hello dynamic content menu that opens at hello right, select **Body**.</span></span>

   <span data-ttu-id="4e8fe-155">d.</span><span class="sxs-lookup"><span data-stu-id="4e8fe-155">d.</span></span> <span data-ttu-id="4e8fe-156">Kliknij przycisk **Pokaż zaawansowane opcje**.</span><span class="sxs-lookup"><span data-stu-id="4e8fe-156">Click **Show advanced options**.</span></span>

      ![Konfiguracja programu Outlook pakietu Office 365](./media/automate-with-logic-apps/flow5.png)

5. <span data-ttu-id="4e8fe-158">W menu hello dynamicznej zawartości hello następujące:</span><span class="sxs-lookup"><span data-stu-id="4e8fe-158">On hello dynamic content menu, do hello following:</span></span>

    <span data-ttu-id="4e8fe-159">a.</span><span class="sxs-lookup"><span data-stu-id="4e8fe-159">a.</span></span> <span data-ttu-id="4e8fe-160">Wybierz **Nazwa załącznika**.</span><span class="sxs-lookup"><span data-stu-id="4e8fe-160">Select **Attachment Name**.</span></span>

    <span data-ttu-id="4e8fe-161">b.</span><span class="sxs-lookup"><span data-stu-id="4e8fe-161">b.</span></span> <span data-ttu-id="4e8fe-162">Wybierz **zawartości załącznika**.</span><span class="sxs-lookup"><span data-stu-id="4e8fe-162">Select **Attachment Content**.</span></span>
    
    <span data-ttu-id="4e8fe-163">c.</span><span class="sxs-lookup"><span data-stu-id="4e8fe-163">c.</span></span> <span data-ttu-id="4e8fe-164">W hello **HTML jest** wybierz opcję **tak**.</span><span class="sxs-lookup"><span data-stu-id="4e8fe-164">In hello **Is HTML** box, select **Yes**.</span></span>

      ![Ekran konfiguracji poczty e-mail usługi Office 365](./media/automate-with-logic-apps/flow7.png)

### <a name="step-7-save-and-test-your-logic-app"></a><span data-ttu-id="4e8fe-166">Krok 7: Zapisz i przetestuj aplikację logiki</span><span class="sxs-lookup"><span data-stu-id="4e8fe-166">Step 7: Save and test your logic app</span></span>
* <span data-ttu-id="4e8fe-167">Kliknij przycisk **zapisać** toosave zmiany.</span><span class="sxs-lookup"><span data-stu-id="4e8fe-167">Click **Save** toosave your changes.</span></span>

<span data-ttu-id="4e8fe-168">Możesz poczekać aplikacji logiki hello toorun wyzwalacza hello, lub uruchom aplikację logiki hello natychmiast po wybraniu **Uruchom**.</span><span class="sxs-lookup"><span data-stu-id="4e8fe-168">You can wait for hello trigger toorun hello logic app, or you can run hello logic app immediately by selecting **Run**.</span></span>

![Ekran Tworzenie aplikacji logiki](./media/automate-with-logic-apps/step7.png)

<span data-ttu-id="4e8fe-170">Po uruchomieniu aplikacji logiki odbiorcy hello, określone na liście hello wiadomości e-mail będą otrzymywać wiadomości e-mail, która wygląda hello:</span><span class="sxs-lookup"><span data-stu-id="4e8fe-170">When your logic app runs, hello recipients you specified in hello email list will receive an email that looks like hello following:</span></span>

![Wiadomość e-mail aplikacji logiki](./media/automate-with-logic-apps/flow9.png)

## <a name="next-steps"></a><span data-ttu-id="4e8fe-172">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="4e8fe-172">Next steps</span></span>

- <span data-ttu-id="4e8fe-173">Dowiedz się więcej o tworzeniu [zapytania analityczne](app-insights-analytics-using.md).</span><span class="sxs-lookup"><span data-stu-id="4e8fe-173">Learn more about creating [Analytics queries](app-insights-analytics-using.md).</span></span>
- <span data-ttu-id="4e8fe-174">Dowiedz się więcej o [Logic Apps](https://docs.microsoft.com/azure/logic-apps/logic-apps-what-are-logic-apps).</span><span class="sxs-lookup"><span data-stu-id="4e8fe-174">Learn more about [Logic Apps](https://docs.microsoft.com/azure/logic-apps/logic-apps-what-are-logic-apps).</span></span>



<!--Link references-->





