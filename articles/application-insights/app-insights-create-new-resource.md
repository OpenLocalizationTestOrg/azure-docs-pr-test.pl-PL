---
title: "aaaCreate nowy zasób usługi Application Insights dla platformy Azure | Dokumentacja firmy Microsoft"
description: "Ręcznie skonfiguruj monitorowanie usługi Application Insights dla nowej aplikacji na żywo."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 878b007e-161c-4e36-8ab2-3d7047d8a92d
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: bwren
ms.openlocfilehash: 3aba7045e1f8fe43d473f0be01dd52106ab992a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-insights-resource"></a><span data-ttu-id="f16dd-103">Tworzenie zasobu usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="f16dd-103">Create an Application Insights resource</span></span>
<span data-ttu-id="f16dd-104">Azure Application Insights przedstawia dane dotyczące Twojej aplikacji w systemie Microsoft Azure *zasobów*.</span><span class="sxs-lookup"><span data-stu-id="f16dd-104">Azure Application Insights displays data about your application in a Microsoft Azure *resource*.</span></span> <span data-ttu-id="f16dd-105">Tworzenie nowego zasobu w związku z tym jest częścią [konfigurowania usługi Application Insights toomonitor nową aplikację][start].</span><span class="sxs-lookup"><span data-stu-id="f16dd-105">Creating a new resource is therefore part of [setting up Application Insights toomonitor a new application][start].</span></span> <span data-ttu-id="f16dd-106">W wielu przypadkach tworzenie zasobu można automatycznie hello IDE.</span><span class="sxs-lookup"><span data-stu-id="f16dd-106">In many cases, creating a resource can be done automatically by hello IDE.</span></span> <span data-ttu-id="f16dd-107">Jednak w niektórych przypadkach należy Utwórz ręcznie zasób — na przykład toohave oddzielne zasoby do rozwoju i produkcji tworzy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f16dd-107">But in some cases, you create a resource manually - for example, toohave separate resources for development and production builds of your application.</span></span>

<span data-ttu-id="f16dd-108">Po utworzeniu zasobu hello, możesz pobrać jego klucza Instrumentacji i użyć tego hello tooconfigure zestawu SDK w aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="f16dd-108">After you have created hello resource, you get its instrumentation key and use that tooconfigure hello SDK in hello application.</span></span> <span data-ttu-id="f16dd-109">linki do kluczowych zasobów Hello hello telemetrii toohello zasobów.</span><span class="sxs-lookup"><span data-stu-id="f16dd-109">hello resource key links hello telemetry toohello resource.</span></span>

## <a name="sign-up-toomicrosoft-azure"></a><span data-ttu-id="f16dd-110">Zarejestruj się tooMicrosoft Azure</span><span class="sxs-lookup"><span data-stu-id="f16dd-110">Sign up tooMicrosoft Azure</span></span>
<span data-ttu-id="f16dd-111">Jeśli nie mam [Microsoft konto, Uzyskaj je teraz](http://live.com).</span><span class="sxs-lookup"><span data-stu-id="f16dd-111">If you haven't got a [Microsoft account, get one now](http://live.com).</span></span> <span data-ttu-id="f16dd-112">(Jeśli korzystasz z usług takich jak Outlook.com, OneDrive, Windows Phone lub XBox Live, masz już konto Microsoft.)</span><span class="sxs-lookup"><span data-stu-id="f16dd-112">(If you use services like Outlook.com, OneDrive, Windows Phone, or XBox Live, you already have a Microsoft account.)</span></span>

<span data-ttu-id="f16dd-113">Należy również subskrypcji zbyt[Microsoft Azure](http://azure.com).</span><span class="sxs-lookup"><span data-stu-id="f16dd-113">You also need a subscription too[Microsoft Azure](http://azure.com).</span></span> <span data-ttu-id="f16dd-114">Jeśli zespół lub organizacja ma subskrypcję platformy Azure, właściciela hello można dodać możesz tooit, za pomocą identyfikatora Windows Live ID.</span><span class="sxs-lookup"><span data-stu-id="f16dd-114">If your team or organization has an Azure subscription, hello owner can add you tooit, using your Windows Live ID.</span></span> <span data-ttu-id="f16dd-115">Tylko są naliczane opłaty za można użyć.</span><span class="sxs-lookup"><span data-stu-id="f16dd-115">You're only charged for what you use.</span></span> <span data-ttu-id="f16dd-116">podstawowy plan domyślny Hello umożliwia pewnego wykorzystanie eksperymentalne bezpłatnie.</span><span class="sxs-lookup"><span data-stu-id="f16dd-116">hello default basic plan allows for a certain amount of experimental use free of charge.</span></span>

<span data-ttu-id="f16dd-117">Jeśli masz już dostępu tooa subskrypcji, zaloguj się za tooApplication wgląd w [http://portal.azure.com](https://portal.azure.com)i użyj toologin Twojego Identyfikatora Live.</span><span class="sxs-lookup"><span data-stu-id="f16dd-117">When you've got access tooa subscription, log in tooApplication Insights at [http://portal.azure.com](https://portal.azure.com), and use your Live ID toologin.</span></span>

## <a name="create-an-application-insights-resource"></a><span data-ttu-id="f16dd-118">Tworzenie zasobu usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="f16dd-118">Create an Application Insights resource</span></span>
<span data-ttu-id="f16dd-119">W hello [portal.azure.com](https://portal.azure.com), Dodaj zasób usługi Application Insights:</span><span class="sxs-lookup"><span data-stu-id="f16dd-119">In hello [portal.azure.com](https://portal.azure.com), add an Application Insights resource:</span></span>

![Kliknij kolejno polecenia Nowy, Application Insights](./media/app-insights-create-new-resource/01-new.png)

* <span data-ttu-id="f16dd-121">**Typ aplikacji** wpływa na informacje wyświetlane na powitania omówienie bloku i właściwości hello dostępnych w [Eksploratora metryk][metrics].</span><span class="sxs-lookup"><span data-stu-id="f16dd-121">**Application type** affects what you see on hello overview blade and hello properties available in [metric explorer][metrics].</span></span> <span data-ttu-id="f16dd-122">Jeśli nie widzisz typ aplikacji, wybierz pozycję Ogólne.</span><span class="sxs-lookup"><span data-stu-id="f16dd-122">If you don't see your type of app, choose General.</span></span>
* <span data-ttu-id="f16dd-123">**Subskrypcja** Twojego konta płatności na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="f16dd-123">**Subscription** is your payment account in Azure.</span></span>
* <span data-ttu-id="f16dd-124">**Grupa zasobów** jest wygodne właściwości zarządzania, takich jak kontrola dostępu.</span><span class="sxs-lookup"><span data-stu-id="f16dd-124">**Resource group** is a convenience for managing properties like access control.</span></span> <span data-ttu-id="f16dd-125">Jeśli utworzono już innych zasobów platformy Azure, możesz wybrać tooput tego nowego zasobu w hello tej samej grupy.</span><span class="sxs-lookup"><span data-stu-id="f16dd-125">If you have already created other Azure resources, you can choose tooput this new resource in hello same group.</span></span>
* <span data-ttu-id="f16dd-126">**Lokalizacja** jest, gdzie możemy przechowywanie danych.</span><span class="sxs-lookup"><span data-stu-id="f16dd-126">**Location** is where we keep your data.</span></span>
* <span data-ttu-id="f16dd-127">**Numer PIN toodashboard** umieszcza kafelka szybkiego dostępu dla zasobu na stronie głównej Azure.</span><span class="sxs-lookup"><span data-stu-id="f16dd-127">**Pin toodashboard** puts a quick-access tile for your resource on your Azure Home page.</span></span> <span data-ttu-id="f16dd-128">Zalecane.</span><span class="sxs-lookup"><span data-stu-id="f16dd-128">Recommended.</span></span>

<span data-ttu-id="f16dd-129">Po utworzeniu aplikacji, zostanie otwarty nowy blok.</span><span class="sxs-lookup"><span data-stu-id="f16dd-129">When your app has been created, a new blade opens.</span></span> <span data-ttu-id="f16dd-130">Ten blok jest, gdzie zobaczyć dane wydajności i użycia dotyczące Twojej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f16dd-130">This blade is where you see performance and usage data about your app.</span></span> 

<span data-ttu-id="f16dd-131">tooit wstecz tooget następnym zalogowaniu tooAzure, poszukaj aplikacji szybki start kafelka na powitania start tablicy (ekranu).</span><span class="sxs-lookup"><span data-stu-id="f16dd-131">tooget back tooit next time you log in tooAzure, look for your app's quick-start tile on hello start board (home screen).</span></span> <span data-ttu-id="f16dd-132">Lub kliknij przycisk Przeglądaj toofind go.</span><span class="sxs-lookup"><span data-stu-id="f16dd-132">Or click Browse toofind it.</span></span>

## <a name="copy-hello-instrumentation-key"></a><span data-ttu-id="f16dd-133">Skopiuj klucz Instrumentacji hello</span><span class="sxs-lookup"><span data-stu-id="f16dd-133">Copy hello instrumentation key</span></span>
<span data-ttu-id="f16dd-134">klucz Instrumentacji Hello identyfikuje hello utworzony zasób.</span><span class="sxs-lookup"><span data-stu-id="f16dd-134">hello instrumentation key identifies hello resource that you created.</span></span> <span data-ttu-id="f16dd-135">Należy go toohello toogive zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="f16dd-135">You need it toogive toohello SDK.</span></span>

![Kliknij Essentials, kliknij przycisk hello klucza Instrumentacji klawisze CTRL + C](./media/app-insights-create-new-resource/02-props.png)

## <a name="install-hello-sdk-in-your-app"></a><span data-ttu-id="f16dd-137">Zainstaluj hello zestawu SDK w aplikacji</span><span class="sxs-lookup"><span data-stu-id="f16dd-137">Install hello SDK in your app</span></span>
<span data-ttu-id="f16dd-138">Zainstaluj zestaw SDK usługi Application Insights hello w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f16dd-138">Install hello Application Insights SDK in your app.</span></span> <span data-ttu-id="f16dd-139">Ten krok zależy od silnie hello typu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f16dd-139">This step depends heavily on hello type of your application.</span></span> 

<span data-ttu-id="f16dd-140">Użyj tooconfigure klucza Instrumentacji hello [SDK zainstalowany w aplikacji hello][start].</span><span class="sxs-lookup"><span data-stu-id="f16dd-140">Use hello instrumentation key tooconfigure [hello SDK that you install in your application][start].</span></span>

<span data-ttu-id="f16dd-141">Hello zestaw SDK zawiera standardowe moduły, które wysłać dane telemetryczne bez konieczności toowrite żadnego kodu.</span><span class="sxs-lookup"><span data-stu-id="f16dd-141">hello SDK includes standard modules that send telemetry without you having toowrite any code.</span></span> <span data-ttu-id="f16dd-142">akcje użytkownika tootrack lub diagnozowanie problemów bardziej szczegółowo [za pomocą interfejsu API hello] [ api] toosend własnych danych telemetrycznych.</span><span class="sxs-lookup"><span data-stu-id="f16dd-142">tootrack user actions or diagnose issues in more detail, [use hello API][api] toosend your own telemetry.</span></span>

## <span data-ttu-id="f16dd-143"><a name="monitor"></a>Zobacz dane telemetryczne</span><span class="sxs-lookup"><span data-stu-id="f16dd-143"><a name="monitor"></a>See telemetry data</span></span>
<span data-ttu-id="f16dd-144">Zamknij hello szybkie uruchomienie bloku tooreturn tooyour aplikacji bloku w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="f16dd-144">Close hello quick start blade tooreturn tooyour application blade in hello Azure portal.</span></span>

<span data-ttu-id="f16dd-145">Kliknij przycisk hello wyszukiwania kafelka toosee [diagnostycznych wyszukiwania][diagnostic], gdzie widoczne hello pierwsze zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="f16dd-145">Click hello Search tile toosee [Diagnostic Search][diagnostic], where hello first events appear.</span></span> 

<span data-ttu-id="f16dd-146">Jeśli spodziewasz większej ilości danych, kliknij przycisk **Odśwież** po kilku sekundach.</span><span class="sxs-lookup"><span data-stu-id="f16dd-146">If you're expecting more data, click **Refresh** after a few seconds  .</span></span>

## <a name="creating-a-resource-automatically"></a><span data-ttu-id="f16dd-147">Automatyczne tworzenie zasobu</span><span class="sxs-lookup"><span data-stu-id="f16dd-147">Creating a resource automatically</span></span>
<span data-ttu-id="f16dd-148">Można napisać [skrypt programu PowerShell](app-insights-powershell.md) toocreate zasobu automatycznie.</span><span class="sxs-lookup"><span data-stu-id="f16dd-148">You can write a [PowerShell script](app-insights-powershell.md) toocreate a resource automatically.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f16dd-149">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f16dd-149">Next steps</span></span>
* [<span data-ttu-id="f16dd-150">Tworzenie pulpitu nawigacyjnego</span><span class="sxs-lookup"><span data-stu-id="f16dd-150">Create a dashboard</span></span>](app-insights-dashboards.md)
* [<span data-ttu-id="f16dd-151">Wyszukiwanie diagnostyczne</span><span class="sxs-lookup"><span data-stu-id="f16dd-151">Diagnostic Search</span></span>](app-insights-diagnostic-search.md)
* [<span data-ttu-id="f16dd-152">Eksplorowanie metryk</span><span class="sxs-lookup"><span data-stu-id="f16dd-152">Explore metrics</span></span>](app-insights-metrics-explorer.md)
* [<span data-ttu-id="f16dd-153">Pisanie zapytań analitycznych</span><span class="sxs-lookup"><span data-stu-id="f16dd-153">Write Analytics queries</span></span>](app-insights-analytics.md)

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[diagnostic]: app-insights-diagnostic-search.md
[metrics]: app-insights-metrics-explorer.md
[start]: app-insights-overview.md

