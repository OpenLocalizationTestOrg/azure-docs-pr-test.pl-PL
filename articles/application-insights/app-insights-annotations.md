---
title: "Adnotacje dla usługi Application Insights o wersji | Dokumentacja firmy Microsoft"
description: "Dodaj wdrożenie lub kompilacji znaczników w wykresach Eksploratora metryk w usłudze Application Insights."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 23173e33-d4f2-4528-a730-913a8fd5f02e
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 11/16/2016
ms.author: bwren
ms.openlocfilehash: f7eb2f3cba535eb64db5544c498289c9e895987a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="annotations-on-metric-charts-in-application-insights"></a><span data-ttu-id="03cb6-103">Adnotacje na wykresach metryki w usłudze Application Insights</span><span class="sxs-lookup"><span data-stu-id="03cb6-103">Annotations on metric charts in Application Insights</span></span>
<span data-ttu-id="03cb6-104">Adnotacje w [Eksploratora metryk](app-insights-metrics-explorer.md) wdrożonym nowej kompilacji lub innego istotnego zdarzenia na wykresach.</span><span class="sxs-lookup"><span data-stu-id="03cb6-104">Annotations on [Metrics Explorer](app-insights-metrics-explorer.md) charts show where you deployed a new build, or other significant event.</span></span> <span data-ttu-id="03cb6-105">Ułatwiają one Zobacz, czy zmiany będzie miało wpływu na wydajność aplikacji.</span><span class="sxs-lookup"><span data-stu-id="03cb6-105">They make it easy to see whether your changes had any effect on your application's performance.</span></span> <span data-ttu-id="03cb6-106">Mogą być automatycznie tworzone przez [systemu kompilacji programu Visual Studio Team Services](https://www.visualstudio.com/en-us/get-started/build/build-your-app-vs).</span><span class="sxs-lookup"><span data-stu-id="03cb6-106">They can be automatically created by the [Visual Studio Team Services build system](https://www.visualstudio.com/en-us/get-started/build/build-your-app-vs).</span></span> <span data-ttu-id="03cb6-107">Można również utworzyć adnotacje do dowolnego zdarzenia, które chcesz przez flagi [tworzenie je z programu PowerShell](#create-annotations-from-powershell).</span><span class="sxs-lookup"><span data-stu-id="03cb6-107">You can also create annotations to flag any event you like by [creating them from PowerShell](#create-annotations-from-powershell).</span></span>

![Przykład adnotacje z korelacją widoczne z czas odpowiedzi serwera](./media/app-insights-annotations/00.png)



## <a name="release-annotations-with-vsts-build"></a><span data-ttu-id="03cb6-109">Adnotacje wydania z kompilacji programu VSTS</span><span class="sxs-lookup"><span data-stu-id="03cb6-109">Release annotations with VSTS build</span></span>

<span data-ttu-id="03cb6-110">Adnotacje wersji to funkcja oparta na chmurze kompilacji i wersję usługi Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="03cb6-110">Release annotations are a feature of the cloud-based build and release service of Visual Studio Team Services.</span></span> 

### <a name="install-the-annotations-extension-one-time"></a><span data-ttu-id="03cb6-111">Zainstaluj rozszerzenie adnotacji (jeden raz)</span><span class="sxs-lookup"><span data-stu-id="03cb6-111">Install the Annotations extension (one time)</span></span>
<span data-ttu-id="03cb6-112">Aby móc tworzyć adnotacji wersji, należy zainstalować jedną wiele rozszerzeń zespołu usługi dostępne w witrynie Marketplace programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="03cb6-112">To be able to create release annotations, you'll need to install one of the many Team Service extensions available in the Visual Studio Marketplace.</span></span>

1. <span data-ttu-id="03cb6-113">Zaloguj się do Twojego [Visual Studio Team Services](https://www.visualstudio.com/en-us/get-started/setup/sign-up-for-visual-studio-online) projektu.</span><span class="sxs-lookup"><span data-stu-id="03cb6-113">Sign in to your [Visual Studio Team Services](https://www.visualstudio.com/en-us/get-started/setup/sign-up-for-visual-studio-online) project.</span></span>
2. <span data-ttu-id="03cb6-114">W programie Visual Studio Marketplace [uzyskać rozszerzenie wersji adnotacje](https://marketplace.visualstudio.com/items/ms-appinsights.appinsightsreleaseannotations)i dodaj go do konta usługi Team Services.</span><span class="sxs-lookup"><span data-stu-id="03cb6-114">In Visual Studio Marketplace, [get the Release Annotations extension](https://marketplace.visualstudio.com/items/ms-appinsights.appinsightsreleaseannotations), and add it to your Team Services account.</span></span>

![AT z góry po prawej stronie sieci web usługi Team Services, otwórz Marketplace.](./media/app-insights-annotations/10.png)

<span data-ttu-id="03cb6-117">Należy w tym celu raz dla Twojego konta Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="03cb6-117">You only need to do this once for your Visual Studio Team Services account.</span></span> <span data-ttu-id="03cb6-118">Adnotacje wersji można teraz skonfigurować dla każdego projektu w ramach Twojego konta.</span><span class="sxs-lookup"><span data-stu-id="03cb6-118">Release annotations can now be configured for any project in your account.</span></span> 

### <a name="configure-release-annotations"></a><span data-ttu-id="03cb6-119">Skonfiguruj adnotacje zlecenia</span><span class="sxs-lookup"><span data-stu-id="03cb6-119">Configure release annotations</span></span>

<span data-ttu-id="03cb6-120">Potrzebujesz oddzielnych klucz interfejsu API dla każdego szablonu wersji usługi VSTS.</span><span class="sxs-lookup"><span data-stu-id="03cb6-120">You need to get a separate API key for each VSTS release template.</span></span>

1. <span data-ttu-id="03cb6-121">Zaloguj się do [portalu Microsoft Azure](https://portal.azure.com) , a następnie otwórz zasobu usługi Application Insights, który monitoruje aplikacji.</span><span class="sxs-lookup"><span data-stu-id="03cb6-121">Sign in to the [Microsoft Azure Portal](https://portal.azure.com) and open the Application Insights resource that monitors your application.</span></span> <span data-ttu-id="03cb6-122">(Lub [teraz utworzyć](app-insights-overview.md), jeśli nie zostało to jeszcze zrobione jeszcze.)</span><span class="sxs-lookup"><span data-stu-id="03cb6-122">(Or [create one now](app-insights-overview.md), if you haven't done so yet.)</span></span>
2. <span data-ttu-id="03cb6-123">Otwórz **dostępu do interfejsu API**, **Application Insights identyfikator**.</span><span class="sxs-lookup"><span data-stu-id="03cb6-123">Open **API Access**,  **Application Insights Id**.</span></span>
   
    ![Portal.azure.com Otwórz zasobu usługi Application Insights i wybierz polecenie Ustawienia.](./media/app-insights-annotations/20.png)

4. <span data-ttu-id="03cb6-127">W osobnym oknie przeglądarki otworzyć lub utworzyć szablon zlecenia, który zarządza wdrożeń z Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="03cb6-127">In a separate browser window, open (or create) the release template that manages your deployments from Visual Studio Team Services.</span></span> 
   
    <span data-ttu-id="03cb6-128">Dodać zadanie, a następnie wybierz zadanie Application Insights wersji adnotacji z menu.</span><span class="sxs-lookup"><span data-stu-id="03cb6-128">Add a task, and select the Application Insights Release Annotation task from the menu.</span></span>
   
    <span data-ttu-id="03cb6-129">Wklej **identyfikator aplikacji** skopiowany z bloku dostępu do interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="03cb6-129">Paste the **Application Id** that you copied from the API Access blade.</span></span>
   
    ![W programie Visual Studio Team Services otwórz wersji, wybierz definicji wersji i wybierz polecenie Edytuj.](./media/app-insights-annotations/30.png)
4. <span data-ttu-id="03cb6-133">Ustaw **APIKey** pole do zmiennej `$(ApiKey)`.</span><span class="sxs-lookup"><span data-stu-id="03cb6-133">Set the **APIKey** field to a variable `$(ApiKey)`.</span></span>

5. <span data-ttu-id="03cb6-134">W oknie Azure Utwórz nowy klucz interfejsu API i wykonać jego kopię.</span><span class="sxs-lookup"><span data-stu-id="03cb6-134">Back in the Azure window, create a new API Key and take a copy of it.</span></span>
   
    ![W bloku dostępu do interfejsu API w oknie Azure kliknij przycisk Utwórz klucz interfejsu API.](./media/app-insights-annotations/40.png)

6. <span data-ttu-id="03cb6-138">Otwórz kartę Konfiguracja szablonu zlecenia.</span><span class="sxs-lookup"><span data-stu-id="03cb6-138">Open the Configuration tab of the release template.</span></span>
   
    <span data-ttu-id="03cb6-139">Tworzenie definicji zmiennej `ApiKey`.</span><span class="sxs-lookup"><span data-stu-id="03cb6-139">Create a variable definition for `ApiKey`.</span></span>
   
    <span data-ttu-id="03cb6-140">Wklej klucz interfejsu API ApiKey definicji zmiennej.</span><span class="sxs-lookup"><span data-stu-id="03cb6-140">Paste your API key to the ApiKey variable definition.</span></span>
   
    ![W oknie usługi Team Services wybierz kartę Konfiguracja, a następnie kliknij przycisk Dodaj zmienną.](./media/app-insights-annotations/50.png)
7. <span data-ttu-id="03cb6-143">Na koniec **zapisać** definicji wersji.</span><span class="sxs-lookup"><span data-stu-id="03cb6-143">Finally, **Save** the release definition.</span></span>


## <a name="view-annotations"></a><span data-ttu-id="03cb6-144">Adnotacje widoku</span><span class="sxs-lookup"><span data-stu-id="03cb6-144">View annotations</span></span>
<span data-ttu-id="03cb6-145">Teraz gdy wdrażania nowej wersji przy użyciu szablonu wersji, adnotacja będą wysyłane do usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="03cb6-145">Now, whenever you use the release template to deploy a new release, an annotation will be sent to Application Insights.</span></span> <span data-ttu-id="03cb6-146">Adnotacje będą wyświetlane na wykresach w Eksploratorze metryk.</span><span class="sxs-lookup"><span data-stu-id="03cb6-146">The annotations will appear on charts in Metrics Explorer.</span></span>

<span data-ttu-id="03cb6-147">Kliknij znacznik żadnych adnotacji w taki sposób, aby otworzyć szczegółowe informacje o wersji, m.in. obiekt żądający, Rozgałęzienie kontroli źródła, wersji definicji, środowisko i inne.</span><span class="sxs-lookup"><span data-stu-id="03cb6-147">Click on any annotation marker to open details about the release, including requestor, source control branch, release definition, environment, and more.</span></span>

![Kliknij znacznik adnotacji dowolnej wersji.](./media/app-insights-annotations/60.png)

## <a name="create-custom-annotations-from-powershell"></a><span data-ttu-id="03cb6-149">Tworzenie niestandardowych adnotacje z programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="03cb6-149">Create custom annotations from PowerShell</span></span>
<span data-ttu-id="03cb6-150">Można również utworzyć adnotacje z żaden proces, który chcesz (bez użycia programu VS Team System).</span><span class="sxs-lookup"><span data-stu-id="03cb6-150">You can also create annotations from any process you like (without using VS Team System).</span></span> 


1. <span data-ttu-id="03cb6-151">Utwórz lokalne kopie z [skrypt programu Powershell z usługi GitHub](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/API/CreateReleaseAnnotation.ps1).</span><span class="sxs-lookup"><span data-stu-id="03cb6-151">Make a local copy of the [Powershell script from GitHub](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/API/CreateReleaseAnnotation.ps1).</span></span>

2. <span data-ttu-id="03cb6-152">Uzyskiwanie Identyfikatora aplikacji i Utwórz klucz interfejsu API w bloku dostępu do interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="03cb6-152">Get the Application ID and create an API key from the API Access blade.</span></span>

3. <span data-ttu-id="03cb6-153">Wywołanie skryptu następująco:</span><span class="sxs-lookup"><span data-stu-id="03cb6-153">Call the script like this:</span></span>

```PS

     .\CreateReleaseAnnotation.ps1 `
      -applicationId "<applicationId>" `
      -apiKey "<apiKey>" `
      -releaseName "<myReleaseName>" `
      -releaseProperties @{
          "ReleaseDescription"="a description";
          "TriggerBy"="My Name" }
```

<span data-ttu-id="03cb6-154">Jest łatwy w celu zmodyfikowania skryptu, na przykład do tworzenia adnotacji w ciągu ostatnich.</span><span class="sxs-lookup"><span data-stu-id="03cb6-154">It's easy to modify the script, for example to create annotations for the past.</span></span>

## <a name="next-steps"></a><span data-ttu-id="03cb6-155">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="03cb6-155">Next steps</span></span>

* [<span data-ttu-id="03cb6-156">Tworzenie elementów roboczych</span><span class="sxs-lookup"><span data-stu-id="03cb6-156">Create work items</span></span>](app-insights-diagnostic-search.md#create-work-item)
* [<span data-ttu-id="03cb6-157">Automatyzacja przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="03cb6-157">Automation with PowerShell</span></span>](app-insights-powershell.md)
