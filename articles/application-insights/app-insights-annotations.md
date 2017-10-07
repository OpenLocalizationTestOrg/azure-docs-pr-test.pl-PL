---
title: "Adnotacje aaaRelease dla usługi Application Insights | Dokumentacja firmy Microsoft"
description: "Dodaj wdrożenie lub kompilacji znaczników wykresy Eksploratora metryk tooyour w usłudze Application Insights."
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
ms.openlocfilehash: e802d22701cb69e96fd1a6b469ea67454195f77a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="annotations-on-metric-charts-in-application-insights"></a><span data-ttu-id="a25da-103">Adnotacje na wykresach metryki w usłudze Application Insights</span><span class="sxs-lookup"><span data-stu-id="a25da-103">Annotations on metric charts in Application Insights</span></span>
<span data-ttu-id="a25da-104">Adnotacje w [Eksploratora metryk](app-insights-metrics-explorer.md) wdrożonym nowej kompilacji lub innego istotnego zdarzenia na wykresach.</span><span class="sxs-lookup"><span data-stu-id="a25da-104">Annotations on [Metrics Explorer](app-insights-metrics-explorer.md) charts show where you deployed a new build, or other significant event.</span></span> <span data-ttu-id="a25da-105">Finalizowania go łatwo toosee czy zmiany miało wpływu na wydajność aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a25da-105">They make it easy toosee whether your changes had any effect on your application's performance.</span></span> <span data-ttu-id="a25da-106">Mogą być automatycznie tworzone przez hello [systemu kompilacji programu Visual Studio Team Services](https://www.visualstudio.com/en-us/get-started/build/build-your-app-vs).</span><span class="sxs-lookup"><span data-stu-id="a25da-106">They can be automatically created by hello [Visual Studio Team Services build system](https://www.visualstudio.com/en-us/get-started/build/build-your-app-vs).</span></span> <span data-ttu-id="a25da-107">Można również utworzyć tooflag adnotacje dowolnego zdarzenia, które chcesz przez [tworzenie je z programu PowerShell](#create-annotations-from-powershell).</span><span class="sxs-lookup"><span data-stu-id="a25da-107">You can also create annotations tooflag any event you like by [creating them from PowerShell](#create-annotations-from-powershell).</span></span>

![Przykład adnotacje z korelacją widoczne z czas odpowiedzi serwera](./media/app-insights-annotations/00.png)



## <a name="release-annotations-with-vsts-build"></a><span data-ttu-id="a25da-109">Adnotacje wydania z kompilacji programu VSTS</span><span class="sxs-lookup"><span data-stu-id="a25da-109">Release annotations with VSTS build</span></span>

<span data-ttu-id="a25da-110">Adnotacje zlecenia są funkcją hello kompilacji opartej na chmurze i wersję usługi Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="a25da-110">Release annotations are a feature of hello cloud-based build and release service of Visual Studio Team Services.</span></span> 

### <a name="install-hello-annotations-extension-one-time"></a><span data-ttu-id="a25da-111">Zainstaluj rozszerzenie adnotacje hello (jeden raz)</span><span class="sxs-lookup"><span data-stu-id="a25da-111">Install hello Annotations extension (one time)</span></span>
<span data-ttu-id="a25da-112">Adnotacje zlecenia może toocreate toobe, będziesz potrzebować tooinstall jedną z hello w wiele rozszerzeń usługi Team hello Visual Studio Marketplace.</span><span class="sxs-lookup"><span data-stu-id="a25da-112">toobe able toocreate release annotations, you'll need tooinstall one of hello many Team Service extensions available in hello Visual Studio Marketplace.</span></span>

1. <span data-ttu-id="a25da-113">Zaloguj się tooyour [Visual Studio Team Services](https://www.visualstudio.com/en-us/get-started/setup/sign-up-for-visual-studio-online) projektu.</span><span class="sxs-lookup"><span data-stu-id="a25da-113">Sign in tooyour [Visual Studio Team Services](https://www.visualstudio.com/en-us/get-started/setup/sign-up-for-visual-studio-online) project.</span></span>
2. <span data-ttu-id="a25da-114">W programie Visual Studio Marketplace [uzyskać rozszerzenie wersji adnotacje hello](https://marketplace.visualstudio.com/items/ms-appinsights.appinsightsreleaseannotations)i dodaj go tooyour konta usługi Team Services.</span><span class="sxs-lookup"><span data-stu-id="a25da-114">In Visual Studio Marketplace, [get hello Release Annotations extension](https://marketplace.visualstudio.com/items/ms-appinsights.appinsightsreleaseannotations), and add it tooyour Team Services account.</span></span>

![AT z góry po prawej stronie sieci web usługi Team Services, otwórz Marketplace.](./media/app-insights-annotations/10.png)

<span data-ttu-id="a25da-117">Wystarczy toodo raz dla Twojego konta Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="a25da-117">You only need toodo this once for your Visual Studio Team Services account.</span></span> <span data-ttu-id="a25da-118">Adnotacje wersji można teraz skonfigurować dla każdego projektu w ramach Twojego konta.</span><span class="sxs-lookup"><span data-stu-id="a25da-118">Release annotations can now be configured for any project in your account.</span></span> 

### <a name="configure-release-annotations"></a><span data-ttu-id="a25da-119">Skonfiguruj adnotacje zlecenia</span><span class="sxs-lookup"><span data-stu-id="a25da-119">Configure release annotations</span></span>

<span data-ttu-id="a25da-120">Należy klucza tooget oddzielne interfejsu API dla każdego szablonu wersji usługi VSTS.</span><span class="sxs-lookup"><span data-stu-id="a25da-120">You need tooget a separate API key for each VSTS release template.</span></span>

1. <span data-ttu-id="a25da-121">Zaloguj się toohello [portalu Microsoft Azure](https://portal.azure.com) , a następnie otwórz hello zasobu usługi Application Insights, który monitoruje aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a25da-121">Sign in toohello [Microsoft Azure Portal](https://portal.azure.com) and open hello Application Insights resource that monitors your application.</span></span> <span data-ttu-id="a25da-122">(Lub [teraz utworzyć](app-insights-overview.md), jeśli nie zostało to jeszcze zrobione jeszcze.)</span><span class="sxs-lookup"><span data-stu-id="a25da-122">(Or [create one now](app-insights-overview.md), if you haven't done so yet.)</span></span>
2. <span data-ttu-id="a25da-123">Otwórz **dostępu do interfejsu API**, **Application Insights identyfikator**.</span><span class="sxs-lookup"><span data-stu-id="a25da-123">Open **API Access**,  **Application Insights Id**.</span></span>
   
    ![Portal.azure.com Otwórz zasobu usługi Application Insights i wybierz polecenie Ustawienia.](./media/app-insights-annotations/20.png)

4. <span data-ttu-id="a25da-127">W osobnym oknie przeglądarki otworzyć lub utworzyć hello wersji szablonu, który zarządza wdrożeń z Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="a25da-127">In a separate browser window, open (or create) hello release template that manages your deployments from Visual Studio Team Services.</span></span> 
   
    <span data-ttu-id="a25da-128">Dodaj zadanie, a hello Application Insights wersji adnotacji zadań, wybierz z hello menu.</span><span class="sxs-lookup"><span data-stu-id="a25da-128">Add a task, and select hello Application Insights Release Annotation task from hello menu.</span></span>
   
    <span data-ttu-id="a25da-129">Wklej hello **identyfikator aplikacji** skopiowany z hello bloku dostępu do interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="a25da-129">Paste hello **Application Id** that you copied from hello API Access blade.</span></span>
   
    ![W programie Visual Studio Team Services otwórz wersji, wybierz definicji wersji i wybierz polecenie Edytuj.](./media/app-insights-annotations/30.png)
4. <span data-ttu-id="a25da-133">Zestaw hello **APIKey** zmiennej tooa pola `$(ApiKey)`.</span><span class="sxs-lookup"><span data-stu-id="a25da-133">Set hello **APIKey** field tooa variable `$(ApiKey)`.</span></span>

5. <span data-ttu-id="a25da-134">Po powrocie do hello Azure okna Utwórz nowy klucz interfejsu API i wykonać jego kopię.</span><span class="sxs-lookup"><span data-stu-id="a25da-134">Back in hello Azure window, create a new API Key and take a copy of it.</span></span>
   
    ![W bloku dostępu do interfejsu API w hello Azure okna hello kliknij przycisk Utwórz klucz interfejsu API.](./media/app-insights-annotations/40.png)

6. <span data-ttu-id="a25da-138">Otwórz kartę Konfiguracja hello hello wersji szablonu.</span><span class="sxs-lookup"><span data-stu-id="a25da-138">Open hello Configuration tab of hello release template.</span></span>
   
    <span data-ttu-id="a25da-139">Tworzenie definicji zmiennej `ApiKey`.</span><span class="sxs-lookup"><span data-stu-id="a25da-139">Create a variable definition for `ApiKey`.</span></span>
   
    <span data-ttu-id="a25da-140">Wklej Twojej toohello klucza interfejsu API ApiKey definicji zmiennej.</span><span class="sxs-lookup"><span data-stu-id="a25da-140">Paste your API key toohello ApiKey variable definition.</span></span>
   
    ![W oknie usługi Team Services hello wybierz kartę Konfiguracja hello, a następnie kliknij przycisk Dodaj zmienną.](./media/app-insights-annotations/50.png)
7. <span data-ttu-id="a25da-143">Na koniec **zapisać** hello definicji wersji.</span><span class="sxs-lookup"><span data-stu-id="a25da-143">Finally, **Save** hello release definition.</span></span>


## <a name="view-annotations"></a><span data-ttu-id="a25da-144">Adnotacje widoku</span><span class="sxs-lookup"><span data-stu-id="a25da-144">View annotations</span></span>
<span data-ttu-id="a25da-145">Teraz przy każdym użyciu hello wersji szablonu toodeploy nową wersję adnotacja zostanie wysłane tooApplication szczegółowych informacji.</span><span class="sxs-lookup"><span data-stu-id="a25da-145">Now, whenever you use hello release template toodeploy a new release, an annotation will be sent tooApplication Insights.</span></span> <span data-ttu-id="a25da-146">Adnotacje Hello będą wyświetlane na wykresach w Eksploratorze metryk.</span><span class="sxs-lookup"><span data-stu-id="a25da-146">hello annotations will appear on charts in Metrics Explorer.</span></span>

<span data-ttu-id="a25da-147">Kliknięcie dowolnej adnotacji znacznika tooopen szczegółowe informacje o wersji hello, m.in. obiekt żądający, Rozgałęzienie kontroli źródła, definicji wersji i środowiska.</span><span class="sxs-lookup"><span data-stu-id="a25da-147">Click on any annotation marker tooopen details about hello release, including requestor, source control branch, release definition, environment, and more.</span></span>

![Kliknij znacznik adnotacji dowolnej wersji.](./media/app-insights-annotations/60.png)

## <a name="create-custom-annotations-from-powershell"></a><span data-ttu-id="a25da-149">Tworzenie niestandardowych adnotacje z programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="a25da-149">Create custom annotations from PowerShell</span></span>
<span data-ttu-id="a25da-150">Można również utworzyć adnotacje z żaden proces, który chcesz (bez użycia programu VS Team System).</span><span class="sxs-lookup"><span data-stu-id="a25da-150">You can also create annotations from any process you like (without using VS Team System).</span></span> 


1. <span data-ttu-id="a25da-151">Wykonaj kopię lokalne powitania [skrypt programu Powershell z usługi GitHub](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/API/CreateReleaseAnnotation.ps1).</span><span class="sxs-lookup"><span data-stu-id="a25da-151">Make a local copy of hello [Powershell script from GitHub](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/API/CreateReleaseAnnotation.ps1).</span></span>

2. <span data-ttu-id="a25da-152">Pobierz identyfikator aplikacji hello i Utwórz klucz interfejsu API z hello bloku dostępu do interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="a25da-152">Get hello Application ID and create an API key from hello API Access blade.</span></span>

3. <span data-ttu-id="a25da-153">Wywołanie skryptu hello następująco:</span><span class="sxs-lookup"><span data-stu-id="a25da-153">Call hello script like this:</span></span>

```PS

     .\CreateReleaseAnnotation.ps1 `
      -applicationId "<applicationId>" `
      -apiKey "<apiKey>" `
      -releaseName "<myReleaseName>" `
      -releaseProperties @{
          "ReleaseDescription"="a description";
          "TriggerBy"="My Name" }
```

<span data-ttu-id="a25da-154">Jest łatwy toomodify hello skryptu, na przykład toocreate adnotacje dla ostatnich hello.</span><span class="sxs-lookup"><span data-stu-id="a25da-154">It's easy toomodify hello script, for example toocreate annotations for hello past.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a25da-155">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a25da-155">Next steps</span></span>

* [<span data-ttu-id="a25da-156">Tworzenie elementów roboczych</span><span class="sxs-lookup"><span data-stu-id="a25da-156">Create work items</span></span>](app-insights-diagnostic-search.md#create-work-item)
* [<span data-ttu-id="a25da-157">Automatyzacja przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="a25da-157">Automation with PowerShell</span></span>](app-insights-powershell.md)
