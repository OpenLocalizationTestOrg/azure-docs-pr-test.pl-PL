---
title: "aaaWindows uniwersalnych zaawansowane raporty dzięki MobileApps zaangażowania"
description: "Jak tooIntegrate usługi Azure Mobile Engagement z uniwersalnych aplikacji systemu Windows"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: ea5030bf-73ac-49b7-bc3e-c25fc10e945a
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 08/12/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: 20968f238ef7ae9dc0b8bb6dac3fb8bdb9bc3a10
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-reporting-with-hello-windows-universal-apps-engagement-sdk"></a><span data-ttu-id="97739-103">Zaawansowane raportowanie z hello SDK zaangażowania aplikacji uniwersalnych systemu Windows</span><span class="sxs-lookup"><span data-stu-id="97739-103">Advanced Reporting with hello Windows Universal Apps Engagement SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="97739-104">Platforma uniwersalna systemu Windows</span><span class="sxs-lookup"><span data-stu-id="97739-104">Universal Windows</span></span>](mobile-engagement-windows-store-advanced-reporting.md)
> * [<span data-ttu-id="97739-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="97739-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md)
> * [<span data-ttu-id="97739-106">iOS</span><span class="sxs-lookup"><span data-stu-id="97739-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md)
> * [<span data-ttu-id="97739-107">Android</span><span class="sxs-lookup"><span data-stu-id="97739-107">Android</span></span>](mobile-engagement-android-advanced-reporting.md)
> 
> 

<span data-ttu-id="97739-108">W tym temacie opisano dodatkowe scenariusze raportowania w aplikacji uniwersalnych systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="97739-108">This topic describes additional reporting scenarios in your Windows Universal application.</span></span> <span data-ttu-id="97739-109">Te scenariusze obejmują opcje, które można wybrać tooapply toohello aplikacji utworzonych w hello [wprowadzenie](mobile-engagement-windows-store-dotnet-get-started.md) samouczka.</span><span class="sxs-lookup"><span data-stu-id="97739-109">These scenarios include options that you can choose tooapply toohello app created in hello [Getting Started](mobile-engagement-windows-store-dotnet-get-started.md) tutorial.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="97739-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="97739-110">Prerequisites</span></span>
[!INCLUDE [Prereqs](../../includes/mobile-engagement-windows-store-prereqs.md)]

<span data-ttu-id="97739-111">Przed rozpoczęciem tego samouczka, należy najpierw wykonać hello [wprowadzenie](mobile-engagement-windows-store-dotnet-get-started.md) samouczka jest celowo bezpośredniego i prosty.</span><span class="sxs-lookup"><span data-stu-id="97739-111">Before starting this tutorial, you must first complete hello [Getting Started](mobile-engagement-windows-store-dotnet-get-started.md) tutorial, which is deliberately direct and simple.</span></span> <span data-ttu-id="97739-112">Ten samouczek obejmuje dodatkowe opcje, które są dostępne.</span><span class="sxs-lookup"><span data-stu-id="97739-112">This tutorial covers additional options you can choose from.</span></span>

## <a name="specifying-engagement-configuration-at-runtime"></a><span data-ttu-id="97739-113">Określenie konfiguracji zaangażowania w czasie wykonywania</span><span class="sxs-lookup"><span data-stu-id="97739-113">Specifying engagement configuration at runtime</span></span>
<span data-ttu-id="97739-114">konfiguracji usługi Engagement Hello jest scentralizowana w hello `Resources\EngagementConfiguration.xml` pliku projektu jest, gdzie został określony w hello [wprowadzenie](mobile-engagement-windows-store-dotnet-get-started.md) tematu.</span><span class="sxs-lookup"><span data-stu-id="97739-114">hello Engagement configuration is centralized in hello `Resources\EngagementConfiguration.xml` file of your project, which is where it was specified in hello [Getting Started](mobile-engagement-windows-store-dotnet-get-started.md) topic.</span></span>

<span data-ttu-id="97739-115">Można jednak również określić go w czasie wykonywania: należy wywołać hello następujące metody przed zainicjowaniem agenta zaangażowania hello:</span><span class="sxs-lookup"><span data-stu-id="97739-115">But you can also specify it at runtime: you can call hello following method before hello Engagement agent initialization:</span></span>

          /* Engagement configuration. */
          EngagementConfiguration engagementConfiguration = new EngagementConfiguration();

          /* Set hello Engagement connection string. */
          engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

          /* Initialize Engagement angent with above configuration. */
          EngagementAgent.Instance.Init(e, engagementConfiguration);



## <a name="recommended-method-overload-your-page-classes"></a><span data-ttu-id="97739-116">Zalecana metoda: przeciążenia sieci `Page` klas</span><span class="sxs-lookup"><span data-stu-id="97739-116">Recommended method: overload your `Page` classes</span></span>
<span data-ttu-id="97739-117">tooactivate hello raportowanie wszystkie dzienniki hello wymagane przez zaangażowania toocompute użytkowników, sesji, działania, awarii (Crash) i statystyki technicznych, wprowadź wszystkie Twoje `Page` klasy podrzędne dziedziczą hello `EngagementPage` klasy.</span><span class="sxs-lookup"><span data-stu-id="97739-117">tooactivate hello reporting of all hello logs required by Engagement toocompute Users, Sessions, Activities, Crashes and Technical statistics, make all your `Page` sub-classes inherit from hello `EngagementPage` classes.</span></span>

<span data-ttu-id="97739-118">Oto przykład strony aplikacji.</span><span class="sxs-lookup"><span data-stu-id="97739-118">Here is an example for a page of your application.</span></span> <span data-ttu-id="97739-119">Możesz zrobić hello samo dla wszystkich stron w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="97739-119">You can do hello same thing for all pages of your application.</span></span>

### <a name="c-source-file"></a><span data-ttu-id="97739-120">Plik źródłowy języka C#</span><span class="sxs-lookup"><span data-stu-id="97739-120">C# Source file</span></span>
<span data-ttu-id="97739-121">Zmodyfikuj stronę `.xaml.cs` pliku:</span><span class="sxs-lookup"><span data-stu-id="97739-121">Modify your page `.xaml.cs` file:</span></span>

* <span data-ttu-id="97739-122">Dodaj tooyour `using` instrukcji:</span><span class="sxs-lookup"><span data-stu-id="97739-122">Add tooyour `using` statements:</span></span>
  
      using Microsoft.Azure.Engagement;
* <span data-ttu-id="97739-123">Zastąp `Page` z `EngagementPage`:</span><span class="sxs-lookup"><span data-stu-id="97739-123">Replace `Page` with `EngagementPage`:</span></span>

<span data-ttu-id="97739-124">**Bez usługi Engagement:**</span><span class="sxs-lookup"><span data-stu-id="97739-124">**Without Engagement:**</span></span>

        namespace Example
        {
          public sealed partial class ExamplePage : Page
          {
            [...]
          }
        }

<span data-ttu-id="97739-125">**Z usługi Engagement:**</span><span class="sxs-lookup"><span data-stu-id="97739-125">**With Engagement:**</span></span>

        using Microsoft.Azure.Engagement;

        namespace Example
        {
          public sealed partial class ExamplePage : EngagementPage
          {
            [...]
          }
        }

> [!IMPORTANT]
> <span data-ttu-id="97739-126">Jeśli strona zastępuje hello `OnNavigatedTo` metody, należy się toocall `base.OnNavigatedTo(e)`.</span><span class="sxs-lookup"><span data-stu-id="97739-126">If your page overrides hello `OnNavigatedTo` method, be sure toocall `base.OnNavigatedTo(e)`.</span></span> <span data-ttu-id="97739-127">W przeciwnym razie hello działania nie został zgłoszony (hello `EngagementPage` wywołania `StartActivity` wewnątrz jego `OnNavigatedTo` metody).</span><span class="sxs-lookup"><span data-stu-id="97739-127">Otherwise, hello activity is not be reported (hello `EngagementPage` calls `StartActivity` inside its `OnNavigatedTo` method).</span></span>
> 
> 

### <a name="xaml-file"></a><span data-ttu-id="97739-128">Plik XAML</span><span class="sxs-lookup"><span data-stu-id="97739-128">XAML file</span></span>
<span data-ttu-id="97739-129">Zmodyfikuj stronę `.xaml` pliku:</span><span class="sxs-lookup"><span data-stu-id="97739-129">Modify your page `.xaml` file:</span></span>

* <span data-ttu-id="97739-130">Dodaj deklaracje przestrzeni nazw tooyour:</span><span class="sxs-lookup"><span data-stu-id="97739-130">Add tooyour namespaces declarations:</span></span>
  
      xmlns:engagement="using:Microsoft.Azure.Engagement"
* <span data-ttu-id="97739-131">Zastąp `Page` z `engagement:EngagementPage`:</span><span class="sxs-lookup"><span data-stu-id="97739-131">Replace `Page` with `engagement:EngagementPage`:</span></span>

<span data-ttu-id="97739-132">**Bez usługi Engagement:**</span><span class="sxs-lookup"><span data-stu-id="97739-132">**Without Engagement:**</span></span>

        <Page>
            <!-- layout -->
            ...
        </Page>

<span data-ttu-id="97739-133">**Z usługi Engagement:**</span><span class="sxs-lookup"><span data-stu-id="97739-133">**With Engagement:**</span></span>

        <engagement:EngagementPage
            xmlns:engagement="using:Microsoft.Azure.Engagement">
            <!-- layout -->
            ...
        </engagement:EngagementPage >

### <a name="override-hello-default-behaviour"></a><span data-ttu-id="97739-134">Zastąpienie zachowania domyślnego hello</span><span class="sxs-lookup"><span data-stu-id="97739-134">Override hello default behaviour</span></span>
<span data-ttu-id="97739-135">Domyślnie nazwa klasy hello strony hello został zgłoszony jako nazwę działania hello, bez dodatkowych.</span><span class="sxs-lookup"><span data-stu-id="97739-135">By default, hello class name of hello page is reported as hello activity name, with no extra.</span></span> <span data-ttu-id="97739-136">Jeśli klasa hello korzysta z sufiksem "Page" hello, Engagement usuwa go.</span><span class="sxs-lookup"><span data-stu-id="97739-136">If hello class uses hello "Page" suffix, Engagement removes it.</span></span>

<span data-ttu-id="97739-137">toooverride hello domyślne zachowanie dla nazwy hello, Dodaj ten kod:</span><span class="sxs-lookup"><span data-stu-id="97739-137">toooverride hello default behavior for hello name, add this code:</span></span>

        // in hello .xaml.cs file
        protected override string GetEngagementPageName()
        {
          /* your code */
          return "new name";
        }

<span data-ttu-id="97739-138">tooreport dodatkowe informacje o Twoich działaniach, Dodaj ten kod:</span><span class="sxs-lookup"><span data-stu-id="97739-138">tooreport extra information with your activity, add this code:</span></span>

        // in hello .xaml.cs file
        protected override Dictionary<object,object> GetEngagementPageExtra()
        {
          /* your code */
          return extra;
        }

<span data-ttu-id="97739-139">Te metody są wywoływane z wewnątrz hello `OnNavigatedTo` metody na stronie.</span><span class="sxs-lookup"><span data-stu-id="97739-139">These methods are called from within hello `OnNavigatedTo` method of your page.</span></span>

### <a name="alternate-method-call-startactivity-manually"></a><span data-ttu-id="97739-140">Alternatywna metoda: wywołanie `StartActivity()` ręcznie</span><span class="sxs-lookup"><span data-stu-id="97739-140">Alternate method: call `StartActivity()` manually</span></span>
<span data-ttu-id="97739-141">Jeśli nie możesz lub nie ma toooverload Twojego `Page` klas, zamiast tego można uruchomić działań przez wywołanie metody `EngagementAgent` metody bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="97739-141">If you cannot or do not want toooverload your `Page` classes, you can instead start your activities by calling `EngagementAgent` methods directly.</span></span>

<span data-ttu-id="97739-142">Firma Microsoft zaleca wywoływania `StartActivity` wewnątrz sieci `OnNavigatedTo` metody na stronie.</span><span class="sxs-lookup"><span data-stu-id="97739-142">We recommend calling `StartActivity` inside your `OnNavigatedTo` method of your Page.</span></span>

            protected override void OnNavigatedTo(NavigationEventArgs e)
            {
              base.OnNavigatedTo(e);
              EngagementAgent.Instance.StartActivity("MyPage");
            }

> [!IMPORTANT]
> <span data-ttu-id="97739-143">Upewnij się, że prawidłowo zakończyć sesję.</span><span class="sxs-lookup"><span data-stu-id="97739-143">Ensure you end your session correctly.</span></span>
> 
> <span data-ttu-id="97739-144">Witaj uniwersalnego zestawu SDK automatycznie wywołuje hello `EndActivity` metody, gdy aplikacja hello jest zamknięty.</span><span class="sxs-lookup"><span data-stu-id="97739-144">hello Windows Universal SDK automatically calls hello `EndActivity` method when hello application is closed.</span></span> <span data-ttu-id="97739-145">W związku z tym jest **wysokiej** zalecane toocall hello `StartActivity` metody zmianie działania hello hello użytkownika i zbyt**nigdy** hello wywołania `EndActivity` — metoda.</span><span class="sxs-lookup"><span data-stu-id="97739-145">Thus, it is **HIGHLY** recommended toocall hello `StartActivity` method whenever hello activity of hello user change, and too**NEVER** call hello `EndActivity` method.</span></span> <span data-ttu-id="97739-146">Ta metoda powiadamia hello zaangażowania serwera bieżącego użytkownika hello opuścił aplikacji hello, która będzie miało wpływ na wszystkie dzienniki aplikacji.</span><span class="sxs-lookup"><span data-stu-id="97739-146">This method notifies hello Engagement server that hello current user has left hello application, which will impact all application logs.</span></span>
> 
> 

## <a name="advanced-reporting"></a><span data-ttu-id="97739-147">Zaawansowane raportowanie</span><span class="sxs-lookup"><span data-stu-id="97739-147">Advanced reporting</span></span>
<span data-ttu-id="97739-148">Opcjonalnie możesz tooreport zdarzenia specyficzne dla aplikacji, błędy i zadań, toodo tak, użyj hello innych metod znalezione w hello `EngagementAgent` klasy.</span><span class="sxs-lookup"><span data-stu-id="97739-148">Optionally, you may want tooreport application-specific events, errors and jobs, toodo so, use hello others methods found in hello `EngagementAgent` class.</span></span> <span data-ttu-id="97739-149">Hello zaangażowania API umożliwia korzystanie z zaawansowanych możliwości wszystkich zaangażowania.</span><span class="sxs-lookup"><span data-stu-id="97739-149">hello Engagement API allows use of all Engagement's advanced capabilities.</span></span>

<span data-ttu-id="97739-150">Aby uzyskać więcej informacji, zobacz [jak toouse hello zaawansowane znakowanie interfejsu API w aplikacji uniwersalnych systemu Windows usługi Mobile Engagement](mobile-engagement-windows-store-use-engagement-api.md).</span><span class="sxs-lookup"><span data-stu-id="97739-150">For further information, see [How toouse hello advanced Mobile Engagement tagging API in your Windows Universal app](mobile-engagement-windows-store-use-engagement-api.md).</span></span>

