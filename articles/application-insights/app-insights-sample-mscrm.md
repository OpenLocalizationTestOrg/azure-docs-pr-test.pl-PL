---
title: aaaMicrosoft Dynamics CRM i Azure Application Insights | Dokumentacja firmy Microsoft
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
ms.openlocfilehash: a39398060d6553fb18a26c101f085b7d87443636
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-enabling-telemetry-for-microsoft-dynamics-crm-online-using-application-insights"></a><span data-ttu-id="73ffd-104">Wskazówki: Włączanie dane telemetryczne dla programu Microsoft Dynamics CRM Online przy użyciu usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="73ffd-104">Walkthrough: Enabling Telemetry for Microsoft Dynamics CRM Online using Application Insights</span></span>
<span data-ttu-id="73ffd-105">W tym artykule opisano sposób danych telemetrycznych tooget [Microsoft Dynamics CRM Online](https://www.dynamics.com/) przy użyciu [Azure Application Insights](https://azure.microsoft.com/services/application-insights/).</span><span class="sxs-lookup"><span data-stu-id="73ffd-105">This article shows you how tooget telemetry data from [Microsoft Dynamics CRM Online](https://www.dynamics.com/) using [Azure Application Insights](https://azure.microsoft.com/services/application-insights/).</span></span> <span data-ttu-id="73ffd-106">Zostanie omówiony hello Zakończ proces dodawania aplikacji tooyour skryptu usługi Application Insights, przechwytywania danych i wizualizacji danych.</span><span class="sxs-lookup"><span data-stu-id="73ffd-106">We’ll walk through hello complete process of adding Application Insights script tooyour application, capturing data, and data visualization.</span></span>

> [!NOTE]
> <span data-ttu-id="73ffd-107">[Przeglądaj hello przykładowe rozwiązanie](https://dynamicsandappinsights.codeplex.com/).</span><span class="sxs-lookup"><span data-stu-id="73ffd-107">[Browse hello sample solution](https://dynamicsandappinsights.codeplex.com/).</span></span>
> 
> 

## <a name="add-application-insights-toonew-or-existing-crm-online-instance"></a><span data-ttu-id="73ffd-108">Dodawanie usługi Application Insights toonew lub istniejącego wystąpienia CRM Online</span><span class="sxs-lookup"><span data-stu-id="73ffd-108">Add Application Insights toonew or existing CRM Online instance</span></span>
<span data-ttu-id="73ffd-109">toomonitor aplikacji, należy dodać aplikację tooyour zestaw SDK usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="73ffd-109">toomonitor your application, you add an Application Insights SDK tooyour application.</span></span> <span data-ttu-id="73ffd-110">Witaj SDK wysyła dane telemetryczne toohello [portalu Application Insights](https://portal.azure.com), której można użyć naszych zaawansowane analizy i narzędzia diagnostyczne lub wyeksportować hello toostorage danych.</span><span class="sxs-lookup"><span data-stu-id="73ffd-110">hello SDK sends telemetry toohello [Application Insights portal](https://portal.azure.com), where you can use our powerful analysis and diagnostic tools, or export hello data toostorage.</span></span>

### <a name="create-an-application-insights-resource-in-azure"></a><span data-ttu-id="73ffd-111">Tworzenie zasobu usługi Application Insights na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="73ffd-111">Create an Application Insights resource in Azure</span></span>
1. <span data-ttu-id="73ffd-112">Pobierz [konta na platformie Microsoft Azure](http://azure.com/pricing).</span><span class="sxs-lookup"><span data-stu-id="73ffd-112">Get [an account in Microsoft Azure](http://azure.com/pricing).</span></span> 
2. <span data-ttu-id="73ffd-113">Zaloguj się na powitania [portalu Azure](https://portal.azure.com) i Dodaj nowy zasób usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="73ffd-113">Sign into hello [Azure portal](https://portal.azure.com) and add a new Application Insights resource.</span></span> <span data-ttu-id="73ffd-114">Jest to, gdzie opracowywania i wyświetlania danych.</span><span class="sxs-lookup"><span data-stu-id="73ffd-114">This is where your data will be processed and displayed.</span></span>
   
    ![Kliknij pozycję +, usług deweloperskich, usługi Application Insights.](./media/app-insights-sample-mscrm/01.png)
   
    <span data-ttu-id="73ffd-116">Wybierz platformy ASP.NET, jako typ aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="73ffd-116">Choose ASP.NET as hello application type.</span></span>
3. <span data-ttu-id="73ffd-117">Otwórz stronę wprowadzenie hello i otworzyć "Monitor i diagnozowanie po stronie klienta".</span><span class="sxs-lookup"><span data-stu-id="73ffd-117">Open hello Getting Started page and open "Monitor and diagnose client side".</span></span>
   
    ![Fragment kodu dotyczący wstawiania na stronie sieci web](./media/app-insights-sample-mscrm/03.png)

<span data-ttu-id="73ffd-119">**Nie zamykaj strony kodowej hello** podczas hello następnego kroku w innym oknie przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="73ffd-119">**Keep hello code page open** while you do hello next step in another browser window.</span></span> <span data-ttu-id="73ffd-120">Będziesz potrzebować kodu hello wkrótce.</span><span class="sxs-lookup"><span data-stu-id="73ffd-120">You'll need hello code soon.</span></span> 

### <a name="create-a-javascript-web-resource-in-microsoft-dynamics-crm"></a><span data-ttu-id="73ffd-121">Utwórz zasób sieci web JavaScript w programie Microsoft Dynamics CRM</span><span class="sxs-lookup"><span data-stu-id="73ffd-121">Create a JavaScript web resource in Microsoft Dynamics CRM</span></span>
1. <span data-ttu-id="73ffd-122">Otwórz wystąpienie CRM Online, a logowanie z uprawnieniami administratora.</span><span class="sxs-lookup"><span data-stu-id="73ffd-122">Open your CRM Online instance and login with administrator privileges.</span></span>
2. <span data-ttu-id="73ffd-123">Otwieranie programu Microsoft Dynamics CRM ustawienia, dostosowania, Dostosuj hello systemu</span><span class="sxs-lookup"><span data-stu-id="73ffd-123">Open Microsoft Dynamics CRM Settings, Customizations, Customize hello System</span></span>
   
    ![Ustawienia programu Microsoft Dynamics CRM](./media/app-insights-sample-mscrm/04.png)
   
    ![Ustawienia > dostosowania](./media/app-insights-sample-mscrm/05.png)

    ![Dostosowywanie opcji system hello](./media/app-insights-sample-mscrm/06.png)

1. <span data-ttu-id="73ffd-127">Utwórz zasób języka JavaScript.</span><span class="sxs-lookup"><span data-stu-id="73ffd-127">Create a JavaScript resource.</span></span>
   
    ![Okno dialogowe nowego zasobu sieci Web](./media/app-insights-sample-mscrm/07.png)
   
    <span data-ttu-id="73ffd-129">Nadaj mu nazwę, wybierz opcję **skryptu (JScript)** i hello Otwórz Edytor tekstów.</span><span class="sxs-lookup"><span data-stu-id="73ffd-129">Give it a name, select **Script (JScript)** and open hello text editor.</span></span>
   
    ![Witaj Otwórz Edytor tekstu](./media/app-insights-sample-mscrm/08.png)
2. <span data-ttu-id="73ffd-131">Skopiuj kod hello z usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="73ffd-131">Copy hello code from Application Insights.</span></span> <span data-ttu-id="73ffd-132">Podczas kopiowania upewnij się, że tooignore tagów skryptu.</span><span class="sxs-lookup"><span data-stu-id="73ffd-132">While copying make sure tooignore script tags.</span></span> <span data-ttu-id="73ffd-133">Zapoznaj się poniżej zrzut ekranu:</span><span class="sxs-lookup"><span data-stu-id="73ffd-133">Refer below screenshot:</span></span>
   
    ![Ustaw klucz Instrumentacji](./media/app-insights-sample-mscrm/09.png)
   
    <span data-ttu-id="73ffd-135">Kod Hello obejmuje hello Instrumentacji klucza, który identyfikuje z zasobu usługi Application insights.</span><span class="sxs-lookup"><span data-stu-id="73ffd-135">hello code includes hello instrumentation key that identifies your Application insights resource.</span></span>
3. <span data-ttu-id="73ffd-136">Zapisz i opublikuj.</span><span class="sxs-lookup"><span data-stu-id="73ffd-136">Save and publish.</span></span>
   
    ![Zapisz i opublikuj](./media/app-insights-sample-mscrm/10.png)

### <a name="instrument-forms"></a><span data-ttu-id="73ffd-138">Formularze dokumentu</span><span class="sxs-lookup"><span data-stu-id="73ffd-138">Instrument Forms</span></span>
1. <span data-ttu-id="73ffd-139">W programie Microsoft CRM Online Otwórz formularz konta hello</span><span class="sxs-lookup"><span data-stu-id="73ffd-139">In Microsoft CRM Online, open hello Account form</span></span>
   
    ![Formularz konta](./media/app-insights-sample-mscrm/11.png)
2. <span data-ttu-id="73ffd-141">Otwórz formularz hello właściwości</span><span class="sxs-lookup"><span data-stu-id="73ffd-141">Open hello form Properties</span></span>
   
    ![Właściwości formularza](./media/app-insights-sample-mscrm/12.png)
3. <span data-ttu-id="73ffd-143">Dodaj hello utworzony zasób sieci web JavaScript</span><span class="sxs-lookup"><span data-stu-id="73ffd-143">Add hello JavaScript web resource that you created</span></span>
   
    ![Dodawanie menu](./media/app-insights-sample-mscrm/13.png)
   
    ![Dodaj zasób sieci web hello](./media/app-insights-sample-mscrm/14.png)
4. <span data-ttu-id="73ffd-146">Zapisz i opublikuj swoje dostosowania formularza.</span><span class="sxs-lookup"><span data-stu-id="73ffd-146">Save and publish your form customizations.</span></span>

## <a name="metrics-captured"></a><span data-ttu-id="73ffd-147">Metryki przechwycić</span><span class="sxs-lookup"><span data-stu-id="73ffd-147">Metrics captured</span></span>
<span data-ttu-id="73ffd-148">Po skonfigurowaniu teraz przechwytywania danych telemetrycznych hello formularza.</span><span class="sxs-lookup"><span data-stu-id="73ffd-148">You have now set up telemetry capture for hello form.</span></span> <span data-ttu-id="73ffd-149">Zawsze, gdy jest on używany, dane zostaną wysłane tooyour zasobu usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="73ffd-149">Whenever it is used, data will be sent tooyour Application Insights resource.</span></span>

<span data-ttu-id="73ffd-150">Poniżej przedstawiono przykłady hello danych, który zostanie wyświetlony.</span><span class="sxs-lookup"><span data-stu-id="73ffd-150">Here are samples of hello data that you'll see.</span></span>

#### <a name="application-health"></a><span data-ttu-id="73ffd-151">Kondycja aplikacji</span><span class="sxs-lookup"><span data-stu-id="73ffd-151">Application health</span></span>
![Czas ładowania strony przykład](./media/app-insights-sample-mscrm/15.png)

![Przykład strony widoki wykresu](./media/app-insights-sample-mscrm/16.png)

<span data-ttu-id="73ffd-154">Wyjątki przeglądarki:</span><span class="sxs-lookup"><span data-stu-id="73ffd-154">Browser exceptions:</span></span>

![Wykres wyjątków przeglądarki](./media/app-insights-sample-mscrm/17.png)

<span data-ttu-id="73ffd-156">Kliknij tooget wykresu hello więcej szczegółów:</span><span class="sxs-lookup"><span data-stu-id="73ffd-156">Click hello chart tooget more detail:</span></span>

![Listy wyjątków](./media/app-insights-sample-mscrm/18.png)

#### <a name="usage"></a><span data-ttu-id="73ffd-158">Sposób użycia</span><span class="sxs-lookup"><span data-stu-id="73ffd-158">Usage</span></span>
![Użytkownikami, sesjami i wyświetleń strony](./media/app-insights-sample-mscrm/19.png)

![Wykresy sesji](./media/app-insights-sample-mscrm/20.png)

![Wersji przeglądarki](./media/app-insights-sample-mscrm/21.png)

#### <a name="browsers"></a><span data-ttu-id="73ffd-162">Przeglądarki</span><span class="sxs-lookup"><span data-stu-id="73ffd-162">Browsers</span></span>
![Podział czas ładowania strony](./media/app-insights-sample-mscrm/22.png)

![Liczba sesji według wersji przeglądarki](./media/app-insights-sample-mscrm/23.png)

#### <a name="geolocation"></a><span data-ttu-id="73ffd-165">Używanie funkcji Geolokalizacji</span><span class="sxs-lookup"><span data-stu-id="73ffd-165">Geolocation</span></span>
![Liczba sesji według kraju](./media/app-insights-sample-mscrm/24.png)

![Sesje i użytkowników według kraju](./media/app-insights-sample-mscrm/25.png)

#### <a name="inside-page-view-request"></a><span data-ttu-id="73ffd-168">Żądanie dostępu do strony w widoku</span><span class="sxs-lookup"><span data-stu-id="73ffd-168">Inside page view request</span></span>
![Podsumowanie widoku strony](./media/app-insights-sample-mscrm/26.png)

![Wyszukaj zdarzenia widoku strony](./media/app-insights-sample-mscrm/27.png)

![Podobne wyświetleń strony](./media/app-insights-sample-mscrm/28.png)

![Właściwości wyświetlania stron](./media/app-insights-sample-mscrm/29.png)

![Strony na sesję](./media/app-insights-sample-mscrm/30.png)

## <a name="sample-code"></a><span data-ttu-id="73ffd-174">Przykładowy kod</span><span class="sxs-lookup"><span data-stu-id="73ffd-174">Sample code</span></span>
<span data-ttu-id="73ffd-175">[Przeglądaj hello przykładowy kod](https://dynamicsandappinsights.codeplex.com/).</span><span class="sxs-lookup"><span data-stu-id="73ffd-175">[Browse hello sample code](https://dynamicsandappinsights.codeplex.com/).</span></span>

## <a name="power-bi"></a><span data-ttu-id="73ffd-176">Power BI</span><span class="sxs-lookup"><span data-stu-id="73ffd-176">Power BI</span></span>
<span data-ttu-id="73ffd-177">Nawet dokładniejszej analizy można zrobić, jeśli użytkownik [wyeksportować hello tooMicrosoft danych usługi Power BI](app-insights-export-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="73ffd-177">You can do even deeper analysis if you [export hello data tooMicrosoft Power BI](app-insights-export-power-bi.md).</span></span>

## <a name="sample-microsoft-dynamics-crm-solution"></a><span data-ttu-id="73ffd-178">Przykładowe Microsoft Dynamics CRM rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="73ffd-178">Sample Microsoft Dynamics CRM Solution</span></span>
<span data-ttu-id="73ffd-179">[Oto hello przykładowe rozwiązanie zaimplementowane w programie Microsoft Dynamics CRM](https://dynamicsandappinsights.codeplex.com/).</span><span class="sxs-lookup"><span data-stu-id="73ffd-179">[Here is hello sample solution implemented in Microsoft Dynamics CRM](https://dynamicsandappinsights.codeplex.com/).</span></span>

## <a name="learn-more"></a><span data-ttu-id="73ffd-180">Dowiedz się więcej</span><span class="sxs-lookup"><span data-stu-id="73ffd-180">Learn more</span></span>
* [<span data-ttu-id="73ffd-181">Co to jest Application Insights?</span><span class="sxs-lookup"><span data-stu-id="73ffd-181">What is Application Insights?</span></span>](app-insights-overview.md)
* [<span data-ttu-id="73ffd-182">Application Insights dla stron sieci web</span><span class="sxs-lookup"><span data-stu-id="73ffd-182">Application Insights for web pages</span></span>](app-insights-javascript.md)
* [<span data-ttu-id="73ffd-183">Więcej przykłady i wskazówki</span><span class="sxs-lookup"><span data-stu-id="73ffd-183">More samples and walkthroughs</span></span>](app-insights-code-samples.md)
