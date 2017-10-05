---
title: "Utwórz nowy zasób usługi Application Insights dla platformy Azure | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 5f8814ee943424c1c278ab3732129d4459f83819
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="create-an-application-insights-resource"></a><span data-ttu-id="98677-103">Tworzenie zasobu usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="98677-103">Create an Application Insights resource</span></span>
<span data-ttu-id="98677-104">Azure Application Insights przedstawia dane dotyczące Twojej aplikacji w systemie Microsoft Azure *zasobów*.</span><span class="sxs-lookup"><span data-stu-id="98677-104">Azure Application Insights displays data about your application in a Microsoft Azure *resource*.</span></span> <span data-ttu-id="98677-105">Tworzenie nowego zasobu w związku z tym jest częścią [konfigurowaniu usługi Application Insights do monitorowania nowej aplikacji][start].</span><span class="sxs-lookup"><span data-stu-id="98677-105">Creating a new resource is therefore part of [setting up Application Insights to monitor a new application][start].</span></span> <span data-ttu-id="98677-106">W wielu przypadkach tworzenie zasobu można automatycznie IDE.</span><span class="sxs-lookup"><span data-stu-id="98677-106">In many cases, creating a resource can be done automatically by the IDE.</span></span> <span data-ttu-id="98677-107">Ale w niektórych przypadkach należy Utwórz ręcznie zasób — na przykład mieć osobne zasobów dla rozwoju i produkcji kompilacje aplikacji.</span><span class="sxs-lookup"><span data-stu-id="98677-107">But in some cases, you create a resource manually - for example, to have separate resources for development and production builds of your application.</span></span>

<span data-ttu-id="98677-108">Po utworzeniu zasobu uzyskać jego klucza Instrumentacji i używać, aby skonfigurować zestaw SDK w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="98677-108">After you have created the resource, you get its instrumentation key and use that to configure the SDK in the application.</span></span> <span data-ttu-id="98677-109">Klucz zasobu łączy dane telemetryczne do zasobu.</span><span class="sxs-lookup"><span data-stu-id="98677-109">The resource key links the telemetry to the resource.</span></span>

## <a name="sign-up-to-microsoft-azure"></a><span data-ttu-id="98677-110">Zaloguj do systemu Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="98677-110">Sign up to Microsoft Azure</span></span>
<span data-ttu-id="98677-111">Jeśli nie mam [Microsoft konto, Uzyskaj je teraz](http://live.com).</span><span class="sxs-lookup"><span data-stu-id="98677-111">If you haven't got a [Microsoft account, get one now](http://live.com).</span></span> <span data-ttu-id="98677-112">(Jeśli korzystasz z usług takich jak Outlook.com, OneDrive, Windows Phone lub XBox Live, masz już konto Microsoft.)</span><span class="sxs-lookup"><span data-stu-id="98677-112">(If you use services like Outlook.com, OneDrive, Windows Phone, or XBox Live, you already have a Microsoft account.)</span></span>

<span data-ttu-id="98677-113">Należy również subskrypcji [Microsoft Azure](http://azure.com).</span><span class="sxs-lookup"><span data-stu-id="98677-113">You also need a subscription to [Microsoft Azure](http://azure.com).</span></span> <span data-ttu-id="98677-114">Jeśli zespół lub organizacja ma subskrypcję platformy Azure, właściciel można do niej dodać, przy użyciu swojego identyfikatora Windows Live.</span><span class="sxs-lookup"><span data-stu-id="98677-114">If your team or organization has an Azure subscription, the owner can add you to it, using your Windows Live ID.</span></span> <span data-ttu-id="98677-115">Tylko są naliczane opłaty za można użyć.</span><span class="sxs-lookup"><span data-stu-id="98677-115">You're only charged for what you use.</span></span> <span data-ttu-id="98677-116">Podstawowy plan domyślny umożliwia pewnego wykorzystanie eksperymentalne bezpłatnie.</span><span class="sxs-lookup"><span data-stu-id="98677-116">The default basic plan allows for a certain amount of experimental use free of charge.</span></span>

<span data-ttu-id="98677-117">Jeśli masz dostęp do subskrypcji, zaloguj się do usługi Application Insights w [http://portal.azure.com](https://portal.azure.com)i używać swojego identyfikatora Live ID do logowania.</span><span class="sxs-lookup"><span data-stu-id="98677-117">When you've got access to a subscription, log in to Application Insights at [http://portal.azure.com](https://portal.azure.com), and use your Live ID to login.</span></span>

## <a name="create-an-application-insights-resource"></a><span data-ttu-id="98677-118">Tworzenie zasobu usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="98677-118">Create an Application Insights resource</span></span>
<span data-ttu-id="98677-119">W [portal.azure.com](https://portal.azure.com), Dodaj zasób usługi Application Insights:</span><span class="sxs-lookup"><span data-stu-id="98677-119">In the [portal.azure.com](https://portal.azure.com), add an Application Insights resource:</span></span>

![Kliknij kolejno polecenia Nowy, Application Insights](./media/app-insights-create-new-resource/01-new.png)

* <span data-ttu-id="98677-121">**Typ aplikacji** wpływa na informacje wyświetlane na bloku omówienie i właściwości, które są dostępne w [Eksploratora metryk][metrics].</span><span class="sxs-lookup"><span data-stu-id="98677-121">**Application type** affects what you see on the overview blade and the properties available in [metric explorer][metrics].</span></span> <span data-ttu-id="98677-122">Jeśli nie widzisz typ aplikacji, wybierz pozycję Ogólne.</span><span class="sxs-lookup"><span data-stu-id="98677-122">If you don't see your type of app, choose General.</span></span>
* <span data-ttu-id="98677-123">**Subskrypcja** Twojego konta płatności na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="98677-123">**Subscription** is your payment account in Azure.</span></span>
* <span data-ttu-id="98677-124">**Grupa zasobów** jest wygodne właściwości zarządzania, takich jak kontrola dostępu.</span><span class="sxs-lookup"><span data-stu-id="98677-124">**Resource group** is a convenience for managing properties like access control.</span></span> <span data-ttu-id="98677-125">Jeśli utworzono już innych zasobów platformy Azure, można umieścić tego nowego zasobu w tej samej grupie.</span><span class="sxs-lookup"><span data-stu-id="98677-125">If you have already created other Azure resources, you can choose to put this new resource in the same group.</span></span>
* <span data-ttu-id="98677-126">**Lokalizacja** jest, gdzie możemy przechowywanie danych.</span><span class="sxs-lookup"><span data-stu-id="98677-126">**Location** is where we keep your data.</span></span>
* <span data-ttu-id="98677-127">**Przypnij do pulpitu nawigacyjnego** umieszcza kafelka szybkiego dostępu dla zasobu na stronie głównej Azure.</span><span class="sxs-lookup"><span data-stu-id="98677-127">**Pin to dashboard** puts a quick-access tile for your resource on your Azure Home page.</span></span> <span data-ttu-id="98677-128">Zalecane.</span><span class="sxs-lookup"><span data-stu-id="98677-128">Recommended.</span></span>

<span data-ttu-id="98677-129">Po utworzeniu aplikacji, zostanie otwarty nowy blok.</span><span class="sxs-lookup"><span data-stu-id="98677-129">When your app has been created, a new blade opens.</span></span> <span data-ttu-id="98677-130">Ten blok jest, gdzie zobaczyć dane wydajności i użycia dotyczące Twojej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="98677-130">This blade is where you see performance and usage data about your app.</span></span> 

<span data-ttu-id="98677-131">Aby wrócić do niej następnym zalogowaniu się do platformy Azure, poszukaj aplikacji szybki start kafelka na tablicy start (ekranu).</span><span class="sxs-lookup"><span data-stu-id="98677-131">To get back to it next time you log in to Azure, look for your app's quick-start tile on the start board (home screen).</span></span> <span data-ttu-id="98677-132">Lub kliknij przycisk Przeglądaj, aby go znaleźć.</span><span class="sxs-lookup"><span data-stu-id="98677-132">Or click Browse to find it.</span></span>

## <a name="copy-the-instrumentation-key"></a><span data-ttu-id="98677-133">Skopiuj klucz Instrumentacji</span><span class="sxs-lookup"><span data-stu-id="98677-133">Copy the instrumentation key</span></span>
<span data-ttu-id="98677-134">Klucz Instrumentacji identyfikatorem zasobu, który został utworzony.</span><span class="sxs-lookup"><span data-stu-id="98677-134">The instrumentation key identifies the resource that you created.</span></span> <span data-ttu-id="98677-135">Należy go ma zostać przypisany do zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="98677-135">You need it to give to the SDK.</span></span>

![Kliknij Essentials, kliknij przycisk klucza Instrumentacji klawisze CTRL + C](./media/app-insights-create-new-resource/02-props.png)

## <a name="install-the-sdk-in-your-app"></a><span data-ttu-id="98677-137">Zainstaluj zestaw SDK w aplikacji</span><span class="sxs-lookup"><span data-stu-id="98677-137">Install the SDK in your app</span></span>
<span data-ttu-id="98677-138">Zainstaluj zestaw SDK usługi Application Insights w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="98677-138">Install the Application Insights SDK in your app.</span></span> <span data-ttu-id="98677-139">Ten krok stopniu zależne od typu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="98677-139">This step depends heavily on the type of your application.</span></span> 

<span data-ttu-id="98677-140">Umożliwia skonfigurowanie klucza Instrumentacji [instalowanej aplikacji zestawu SDK][start].</span><span class="sxs-lookup"><span data-stu-id="98677-140">Use the instrumentation key to configure [the SDK that you install in your application][start].</span></span>

<span data-ttu-id="98677-141">Zestaw SDK zawiera standardowe moduły, które wysłać dane telemetryczne bez konieczności pisania kodu.</span><span class="sxs-lookup"><span data-stu-id="98677-141">The SDK includes standard modules that send telemetry without you having to write any code.</span></span> <span data-ttu-id="98677-142">Śledzenie działań użytkownika lub diagnozowanie problemów bardziej szczegółowo [za pomocą interfejsu API] [ api] do wysyłania własnych danych telemetrycznych.</span><span class="sxs-lookup"><span data-stu-id="98677-142">To track user actions or diagnose issues in more detail, [use the API][api] to send your own telemetry.</span></span>

## <span data-ttu-id="98677-143"><a name="monitor"></a>Zobacz dane telemetryczne</span><span class="sxs-lookup"><span data-stu-id="98677-143"><a name="monitor"></a>See telemetry data</span></span>
<span data-ttu-id="98677-144">Zamknij bloku szybki start, aby powrócić do bloku Twojej aplikacji w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="98677-144">Close the quick start blade to return to your application blade in the Azure portal.</span></span>

<span data-ttu-id="98677-145">Kliknij pole wyszukiwania, aby zobaczyć [diagnostycznych wyszukiwania][diagnostic], gdy pojawi się pierwsze zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="98677-145">Click the Search tile to see [Diagnostic Search][diagnostic], where the first events appear.</span></span> 

<span data-ttu-id="98677-146">Jeśli spodziewasz większej ilości danych, kliknij przycisk **Odśwież** po kilku sekundach.</span><span class="sxs-lookup"><span data-stu-id="98677-146">If you're expecting more data, click **Refresh** after a few seconds  .</span></span>

## <a name="creating-a-resource-automatically"></a><span data-ttu-id="98677-147">Automatyczne tworzenie zasobu</span><span class="sxs-lookup"><span data-stu-id="98677-147">Creating a resource automatically</span></span>
<span data-ttu-id="98677-148">Można napisać [skrypt programu PowerShell](app-insights-powershell.md) automatyczne tworzenie zasobu.</span><span class="sxs-lookup"><span data-stu-id="98677-148">You can write a [PowerShell script](app-insights-powershell.md) to create a resource automatically.</span></span>

## <a name="next-steps"></a><span data-ttu-id="98677-149">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="98677-149">Next steps</span></span>
* [<span data-ttu-id="98677-150">Tworzenie pulpitu nawigacyjnego</span><span class="sxs-lookup"><span data-stu-id="98677-150">Create a dashboard</span></span>](app-insights-dashboards.md)
* [<span data-ttu-id="98677-151">Wyszukiwanie diagnostyczne</span><span class="sxs-lookup"><span data-stu-id="98677-151">Diagnostic Search</span></span>](app-insights-diagnostic-search.md)
* [<span data-ttu-id="98677-152">Eksplorowanie metryk</span><span class="sxs-lookup"><span data-stu-id="98677-152">Explore metrics</span></span>](app-insights-metrics-explorer.md)
* [<span data-ttu-id="98677-153">Pisanie zapytań analitycznych</span><span class="sxs-lookup"><span data-stu-id="98677-153">Write Analytics queries</span></span>](app-insights-analytics.md)

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[diagnostic]: app-insights-diagnostic-search.md
[metrics]: app-insights-metrics-explorer.md
[start]: app-insights-overview.md

