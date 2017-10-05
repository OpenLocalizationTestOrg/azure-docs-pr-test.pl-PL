---
title: "Microsoft Dynamics CRM i usługa Azure Application Insights | Dokumentacja firmy Microsoft"
description: "Pobierz dane telemetryczne z programu Microsoft Dynamics CRM Online przy użyciu usługi Application Insights. Pobieranie danych, wizualizacji i eksportowanie Przewodnik instalacji."
services: application-insights
documentationcenter: 
author: mazharmicrosoft
manager: carmonm
ms.assetid: 04c66338-687e-49e5-9975-be935f98f156
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 04/16/2017
ms.author: bwren
ms.openlocfilehash: a9593d5f198e05db80451a599428a296ed02e781
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="walkthrough-enabling-telemetry-for-microsoft-dynamics-crm-online-using-application-insights"></a><span data-ttu-id="78c8b-104">Wskazówki: Włączanie dane telemetryczne dla programu Microsoft Dynamics CRM Online przy użyciu usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="78c8b-104">Walkthrough: Enabling Telemetry for Microsoft Dynamics CRM Online using Application Insights</span></span>
<span data-ttu-id="78c8b-105">W tym artykule przedstawiono sposób pobierać dane telemetryczne [Microsoft Dynamics CRM Online](https://www.dynamics.com/) przy użyciu [Azure Application Insights](https://azure.microsoft.com/services/application-insights/).</span><span class="sxs-lookup"><span data-stu-id="78c8b-105">This article shows you how to get telemetry data from [Microsoft Dynamics CRM Online](https://www.dynamics.com/) using [Azure Application Insights](https://azure.microsoft.com/services/application-insights/).</span></span> <span data-ttu-id="78c8b-106">Zostanie omówiony Zakończ proces dodawania skryptów usługi Application Insights do aplikacji, przechwytywania danych i wizualizacji danych.</span><span class="sxs-lookup"><span data-stu-id="78c8b-106">We’ll walk through the complete process of adding Application Insights script to your application, capturing data, and data visualization.</span></span>

> [!NOTE]
> <span data-ttu-id="78c8b-107">[Przeglądaj przykładowe rozwiązanie](https://dynamicsandappinsights.codeplex.com/).</span><span class="sxs-lookup"><span data-stu-id="78c8b-107">[Browse the sample solution](https://dynamicsandappinsights.codeplex.com/).</span></span>
> 
> 

## <a name="add-application-insights-to-new-or-existing-crm-online-instance"></a><span data-ttu-id="78c8b-108">Dodawanie usługi Application Insights do nowego lub istniejącego wystąpienia CRM Online</span><span class="sxs-lookup"><span data-stu-id="78c8b-108">Add Application Insights to new or existing CRM Online instance</span></span>
<span data-ttu-id="78c8b-109">Do monitorowania aplikacji, należy dodać zestaw SDK usługi Application Insights do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="78c8b-109">To monitor your application, you add an Application Insights SDK to your application.</span></span> <span data-ttu-id="78c8b-110">Zestaw SDK wysyła dane telemetryczne do [portalu Application Insights](https://portal.azure.com), których można użyć naszych zaawansowane analizy i narzędzia diagnostyczne lub Eksportuj dane do magazynu.</span><span class="sxs-lookup"><span data-stu-id="78c8b-110">The SDK sends telemetry to the [Application Insights portal](https://portal.azure.com), where you can use our powerful analysis and diagnostic tools, or export the data to storage.</span></span>

### <a name="create-an-application-insights-resource-in-azure"></a><span data-ttu-id="78c8b-111">Tworzenie zasobu usługi Application Insights na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="78c8b-111">Create an Application Insights resource in Azure</span></span>
1. <span data-ttu-id="78c8b-112">Pobierz [konta na platformie Microsoft Azure](http://azure.com/pricing).</span><span class="sxs-lookup"><span data-stu-id="78c8b-112">Get [an account in Microsoft Azure](http://azure.com/pricing).</span></span> 
2. <span data-ttu-id="78c8b-113">Zaloguj się do [portalu Azure](https://portal.azure.com) i Dodaj nowy zasób usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="78c8b-113">Sign into the [Azure portal](https://portal.azure.com) and add a new Application Insights resource.</span></span> <span data-ttu-id="78c8b-114">Jest to, gdzie opracowywania i wyświetlania danych.</span><span class="sxs-lookup"><span data-stu-id="78c8b-114">This is where your data will be processed and displayed.</span></span>
   
    ![Kliknij pozycję +, usług deweloperskich, usługi Application Insights.](./media/app-insights-sample-mscrm/01.png)
   
    <span data-ttu-id="78c8b-116">Wybierz ASP.NET jako typ aplikacji.</span><span class="sxs-lookup"><span data-stu-id="78c8b-116">Choose ASP.NET as the application type.</span></span>
3. <span data-ttu-id="78c8b-117">Otwórz stronę wprowadzenie i otworzyć "Monitor i diagnozowanie po stronie klienta".</span><span class="sxs-lookup"><span data-stu-id="78c8b-117">Open the Getting Started page and open "Monitor and diagnose client side".</span></span>
   
    ![Fragment kodu dotyczący wstawiania na stronie sieci web](./media/app-insights-sample-mscrm/03.png)

<span data-ttu-id="78c8b-119">**Nie zamykaj strony kodowej** przy wykonywaniu do następnego kroku w innym oknie przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="78c8b-119">**Keep the code page open** while you do the next step in another browser window.</span></span> <span data-ttu-id="78c8b-120">Będziesz potrzebować kod wkrótce.</span><span class="sxs-lookup"><span data-stu-id="78c8b-120">You'll need the code soon.</span></span> 

### <a name="create-a-javascript-web-resource-in-microsoft-dynamics-crm"></a><span data-ttu-id="78c8b-121">Utwórz zasób sieci web JavaScript w programie Microsoft Dynamics CRM</span><span class="sxs-lookup"><span data-stu-id="78c8b-121">Create a JavaScript web resource in Microsoft Dynamics CRM</span></span>
1. <span data-ttu-id="78c8b-122">Otwórz wystąpienie CRM Online, a logowanie z uprawnieniami administratora.</span><span class="sxs-lookup"><span data-stu-id="78c8b-122">Open your CRM Online instance and login with administrator privileges.</span></span>
2. <span data-ttu-id="78c8b-123">Otwórz aplikację Microsoft Dynamics CRM ustawienia, dostosowania, dostosowywanie systemu</span><span class="sxs-lookup"><span data-stu-id="78c8b-123">Open Microsoft Dynamics CRM Settings, Customizations, Customize the System</span></span>
   
    ![Ustawienia programu Microsoft Dynamics CRM](./media/app-insights-sample-mscrm/04.png)
   
    ![Ustawienia > dostosowania](./media/app-insights-sample-mscrm/05.png)

    ![Dostosowywanie opcji systemu](./media/app-insights-sample-mscrm/06.png)

1. <span data-ttu-id="78c8b-127">Utwórz zasób języka JavaScript.</span><span class="sxs-lookup"><span data-stu-id="78c8b-127">Create a JavaScript resource.</span></span>
   
    ![Okno dialogowe nowego zasobu sieci Web](./media/app-insights-sample-mscrm/07.png)
   
    <span data-ttu-id="78c8b-129">Nadaj mu nazwę, wybierz opcję **skryptu (JScript)** , a następnie otwórz Edytor tekstu.</span><span class="sxs-lookup"><span data-stu-id="78c8b-129">Give it a name, select **Script (JScript)** and open the text editor.</span></span>
   
    ![Otwórz Edytor tekstu](./media/app-insights-sample-mscrm/08.png)
2. <span data-ttu-id="78c8b-131">Skopiuj kod z usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="78c8b-131">Copy the code from Application Insights.</span></span> <span data-ttu-id="78c8b-132">Podczas kopiowania upewnij się, że zignorowanie tagów skryptu.</span><span class="sxs-lookup"><span data-stu-id="78c8b-132">While copying make sure to ignore script tags.</span></span> <span data-ttu-id="78c8b-133">Zapoznaj się poniżej zrzut ekranu:</span><span class="sxs-lookup"><span data-stu-id="78c8b-133">Refer below screenshot:</span></span>
   
    ![Ustaw klucz Instrumentacji](./media/app-insights-sample-mscrm/09.png)
   
    <span data-ttu-id="78c8b-135">Kod zawiera klucz instrumentacji, który identyfikuje z zasobu usługi Application insights.</span><span class="sxs-lookup"><span data-stu-id="78c8b-135">The code includes the instrumentation key that identifies your Application insights resource.</span></span>
3. <span data-ttu-id="78c8b-136">Zapisz i opublikuj.</span><span class="sxs-lookup"><span data-stu-id="78c8b-136">Save and publish.</span></span>
   
    ![Zapisz i opublikuj](./media/app-insights-sample-mscrm/10.png)

### <a name="instrument-forms"></a><span data-ttu-id="78c8b-138">Formularze dokumentu</span><span class="sxs-lookup"><span data-stu-id="78c8b-138">Instrument Forms</span></span>
1. <span data-ttu-id="78c8b-139">W programie Microsoft CRM Online Otwórz formularz konta</span><span class="sxs-lookup"><span data-stu-id="78c8b-139">In Microsoft CRM Online, open the Account form</span></span>
   
    ![Formularz konta](./media/app-insights-sample-mscrm/11.png)
2. <span data-ttu-id="78c8b-141">Otwórz formularz właściwości</span><span class="sxs-lookup"><span data-stu-id="78c8b-141">Open the form Properties</span></span>
   
    ![Właściwości formularza](./media/app-insights-sample-mscrm/12.png)
3. <span data-ttu-id="78c8b-143">Dodaj zasób sieci web JavaScript, który został utworzony</span><span class="sxs-lookup"><span data-stu-id="78c8b-143">Add the JavaScript web resource that you created</span></span>
   
    ![Dodawanie menu](./media/app-insights-sample-mscrm/13.png)
   
    ![Dodaj zasób sieci web](./media/app-insights-sample-mscrm/14.png)
4. <span data-ttu-id="78c8b-146">Zapisz i opublikuj swoje dostosowania formularza.</span><span class="sxs-lookup"><span data-stu-id="78c8b-146">Save and publish your form customizations.</span></span>

## <a name="metrics-captured"></a><span data-ttu-id="78c8b-147">Metryki przechwycić</span><span class="sxs-lookup"><span data-stu-id="78c8b-147">Metrics captured</span></span>
<span data-ttu-id="78c8b-148">Po skonfigurowaniu teraz przechwytywania danych telemetrycznych dla formularza.</span><span class="sxs-lookup"><span data-stu-id="78c8b-148">You have now set up telemetry capture for the form.</span></span> <span data-ttu-id="78c8b-149">Zawsze, gdy jest on używany, dane zostaną wysłane do zasobu usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="78c8b-149">Whenever it is used, data will be sent to your Application Insights resource.</span></span>

<span data-ttu-id="78c8b-150">Poniżej przedstawiono przykłady, danych, który zostanie wyświetlony.</span><span class="sxs-lookup"><span data-stu-id="78c8b-150">Here are samples of the data that you'll see.</span></span>

#### <a name="application-health"></a><span data-ttu-id="78c8b-151">Kondycja aplikacji</span><span class="sxs-lookup"><span data-stu-id="78c8b-151">Application health</span></span>
![Czas ładowania strony przykład](./media/app-insights-sample-mscrm/15.png)

![Przykład strony widoki wykresu](./media/app-insights-sample-mscrm/16.png)

<span data-ttu-id="78c8b-154">Wyjątki przeglądarki:</span><span class="sxs-lookup"><span data-stu-id="78c8b-154">Browser exceptions:</span></span>

![Wykres wyjątków przeglądarki](./media/app-insights-sample-mscrm/17.png)

<span data-ttu-id="78c8b-156">Kliknij na wykresie, aby uzyskać więcej szczegółów:</span><span class="sxs-lookup"><span data-stu-id="78c8b-156">Click the chart to get more detail:</span></span>

![Listy wyjątków](./media/app-insights-sample-mscrm/18.png)

#### <a name="usage"></a><span data-ttu-id="78c8b-158">Sposób użycia</span><span class="sxs-lookup"><span data-stu-id="78c8b-158">Usage</span></span>
![Użytkownikami, sesjami i wyświetleń strony](./media/app-insights-sample-mscrm/19.png)

![Wykresy sesji](./media/app-insights-sample-mscrm/20.png)

![Wersji przeglądarki](./media/app-insights-sample-mscrm/21.png)

#### <a name="browsers"></a><span data-ttu-id="78c8b-162">Przeglądarki</span><span class="sxs-lookup"><span data-stu-id="78c8b-162">Browsers</span></span>
![Podział czas ładowania strony](./media/app-insights-sample-mscrm/22.png)

![Liczba sesji według wersji przeglądarki](./media/app-insights-sample-mscrm/23.png)

#### <a name="geolocation"></a><span data-ttu-id="78c8b-165">Używanie funkcji Geolokalizacji</span><span class="sxs-lookup"><span data-stu-id="78c8b-165">Geolocation</span></span>
![Liczba sesji według kraju](./media/app-insights-sample-mscrm/24.png)

![Sesje i użytkowników według kraju](./media/app-insights-sample-mscrm/25.png)

#### <a name="inside-page-view-request"></a><span data-ttu-id="78c8b-168">Żądanie dostępu do strony w widoku</span><span class="sxs-lookup"><span data-stu-id="78c8b-168">Inside page view request</span></span>
![Podsumowanie widoku strony](./media/app-insights-sample-mscrm/26.png)

![Wyszukaj zdarzenia widoku strony](./media/app-insights-sample-mscrm/27.png)

![Podobne wyświetleń strony](./media/app-insights-sample-mscrm/28.png)

![Właściwości wyświetlania stron](./media/app-insights-sample-mscrm/29.png)

![Strony na sesję](./media/app-insights-sample-mscrm/30.png)

## <a name="sample-code"></a><span data-ttu-id="78c8b-174">Przykładowy kod</span><span class="sxs-lookup"><span data-stu-id="78c8b-174">Sample code</span></span>
<span data-ttu-id="78c8b-175">[Przeglądaj w przykładowym kodzie](https://dynamicsandappinsights.codeplex.com/).</span><span class="sxs-lookup"><span data-stu-id="78c8b-175">[Browse the sample code](https://dynamicsandappinsights.codeplex.com/).</span></span>

## <a name="power-bi"></a><span data-ttu-id="78c8b-176">Power BI</span><span class="sxs-lookup"><span data-stu-id="78c8b-176">Power BI</span></span>
<span data-ttu-id="78c8b-177">Nawet dokładniejszej analizy można zrobić, jeśli użytkownik [eksportowanie danych do usługi Microsoft Power BI](app-insights-export-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="78c8b-177">You can do even deeper analysis if you [export the data to Microsoft Power BI](app-insights-export-power-bi.md).</span></span>

## <a name="sample-microsoft-dynamics-crm-solution"></a><span data-ttu-id="78c8b-178">Przykładowe Microsoft Dynamics CRM rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="78c8b-178">Sample Microsoft Dynamics CRM Solution</span></span>
<span data-ttu-id="78c8b-179">[Oto przykładowe rozwiązanie zaimplementowane w programie Microsoft Dynamics CRM](https://dynamicsandappinsights.codeplex.com/).</span><span class="sxs-lookup"><span data-stu-id="78c8b-179">[Here is the sample solution implemented in Microsoft Dynamics CRM](https://dynamicsandappinsights.codeplex.com/).</span></span>

## <a name="learn-more"></a><span data-ttu-id="78c8b-180">Dowiedz się więcej</span><span class="sxs-lookup"><span data-stu-id="78c8b-180">Learn more</span></span>
* [<span data-ttu-id="78c8b-181">Co to jest Application Insights?</span><span class="sxs-lookup"><span data-stu-id="78c8b-181">What is Application Insights?</span></span>](app-insights-overview.md)
* [<span data-ttu-id="78c8b-182">Application Insights dla stron sieci web</span><span class="sxs-lookup"><span data-stu-id="78c8b-182">Application Insights for web pages</span></span>](app-insights-javascript.md)
* [<span data-ttu-id="78c8b-183">Więcej przykłady i wskazówki</span><span class="sxs-lookup"><span data-stu-id="78c8b-183">More samples and walkthroughs</span></span>](app-insights-code-samples.md)
