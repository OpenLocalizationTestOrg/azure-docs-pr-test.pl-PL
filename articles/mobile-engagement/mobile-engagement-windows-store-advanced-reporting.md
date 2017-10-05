---
title: "Zaawansowane raporty dzięki zaangażowania MobileApps aplikacje uniwersalne systemu Windows"
description: "Integrowanie usługi Azure Mobile Engagement z uniwersalnych aplikacji systemu Windows"
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
ms.openlocfilehash: feac309db1ffce0945012e293bfc1df417aed876
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="advanced-reporting-with-the-windows-universal-apps-engagement-sdk"></a><span data-ttu-id="d65e3-103">Zaawansowane raporty dzięki zaangażowania uniwersalnych aplikacji systemu Windows SDK</span><span class="sxs-lookup"><span data-stu-id="d65e3-103">Advanced Reporting with the Windows Universal Apps Engagement SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d65e3-104">Platforma uniwersalna systemu Windows</span><span class="sxs-lookup"><span data-stu-id="d65e3-104">Universal Windows</span></span>](mobile-engagement-windows-store-advanced-reporting.md)
> * [<span data-ttu-id="d65e3-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="d65e3-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md)
> * [<span data-ttu-id="d65e3-106">iOS</span><span class="sxs-lookup"><span data-stu-id="d65e3-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md)
> * [<span data-ttu-id="d65e3-107">Android</span><span class="sxs-lookup"><span data-stu-id="d65e3-107">Android</span></span>](mobile-engagement-android-advanced-reporting.md)
> 
> 

<span data-ttu-id="d65e3-108">W tym temacie opisano dodatkowe scenariusze raportowania w aplikacji uniwersalnych systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="d65e3-108">This topic describes additional reporting scenarios in your Windows Universal application.</span></span> <span data-ttu-id="d65e3-109">Te scenariusze obejmują opcje, które można zastosować do aplikacji utworzonych w [wprowadzenie](mobile-engagement-windows-store-dotnet-get-started.md) samouczka.</span><span class="sxs-lookup"><span data-stu-id="d65e3-109">These scenarios include options that you can choose to apply to the app created in the [Getting Started](mobile-engagement-windows-store-dotnet-get-started.md) tutorial.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d65e3-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="d65e3-110">Prerequisites</span></span>
[!INCLUDE [Prereqs](../../includes/mobile-engagement-windows-store-prereqs.md)]

<span data-ttu-id="d65e3-111">Przed rozpoczęciem tego samouczka, należy najpierw wykonać [wprowadzenie](mobile-engagement-windows-store-dotnet-get-started.md) samouczka jest celowo bezpośredniego i prosty.</span><span class="sxs-lookup"><span data-stu-id="d65e3-111">Before starting this tutorial, you must first complete the [Getting Started](mobile-engagement-windows-store-dotnet-get-started.md) tutorial, which is deliberately direct and simple.</span></span> <span data-ttu-id="d65e3-112">Ten samouczek obejmuje dodatkowe opcje, które są dostępne.</span><span class="sxs-lookup"><span data-stu-id="d65e3-112">This tutorial covers additional options you can choose from.</span></span>

## <a name="specifying-engagement-configuration-at-runtime"></a><span data-ttu-id="d65e3-113">Określenie konfiguracji zaangażowania w czasie wykonywania</span><span class="sxs-lookup"><span data-stu-id="d65e3-113">Specifying engagement configuration at runtime</span></span>
<span data-ttu-id="d65e3-114">Konfiguracja zaangażowania jest scentralizowana w `Resources\EngagementConfiguration.xml` pliku projektu jest, gdzie została określona w [wprowadzenie](mobile-engagement-windows-store-dotnet-get-started.md) tematu.</span><span class="sxs-lookup"><span data-stu-id="d65e3-114">The Engagement configuration is centralized in the `Resources\EngagementConfiguration.xml` file of your project, which is where it was specified in the [Getting Started](mobile-engagement-windows-store-dotnet-get-started.md) topic.</span></span>

<span data-ttu-id="d65e3-115">Można jednak również określić go w czasie wykonywania: należy wywołać przed zainicjowaniem agenta zaangażowania następującą metodę:</span><span class="sxs-lookup"><span data-stu-id="d65e3-115">But you can also specify it at runtime: you can call the following method before the Engagement agent initialization:</span></span>

          /* Engagement configuration. */
          EngagementConfiguration engagementConfiguration = new EngagementConfiguration();

          /* Set the Engagement connection string. */
          engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

          /* Initialize Engagement angent with above configuration. */
          EngagementAgent.Instance.Init(e, engagementConfiguration);



## <a name="recommended-method-overload-your-page-classes"></a><span data-ttu-id="d65e3-116">Zalecana metoda: przeciążenia sieci `Page` klas</span><span class="sxs-lookup"><span data-stu-id="d65e3-116">Recommended method: overload your `Page` classes</span></span>
<span data-ttu-id="d65e3-117">Aktywować raportowania wszystkie dzienniki wymagane przez zaangażowania można obliczyć użytkowników, sesji, działania, awarii (Crash) i statystyki technicznych, aby wszystkie Twoje `Page` klasy podrzędne dziedziczą `EngagementPage` klasy.</span><span class="sxs-lookup"><span data-stu-id="d65e3-117">To activate the reporting of all the logs required by Engagement to compute Users, Sessions, Activities, Crashes and Technical statistics, make all your `Page` sub-classes inherit from the `EngagementPage` classes.</span></span>

<span data-ttu-id="d65e3-118">Oto przykład strony aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d65e3-118">Here is an example for a page of your application.</span></span> <span data-ttu-id="d65e3-119">Możesz to zrobić to samo dla wszystkich stron w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d65e3-119">You can do the same thing for all pages of your application.</span></span>

### <a name="c-source-file"></a><span data-ttu-id="d65e3-120">Plik źródłowy języka C#</span><span class="sxs-lookup"><span data-stu-id="d65e3-120">C# Source file</span></span>
<span data-ttu-id="d65e3-121">Zmodyfikuj stronę `.xaml.cs` pliku:</span><span class="sxs-lookup"><span data-stu-id="d65e3-121">Modify your page `.xaml.cs` file:</span></span>

* <span data-ttu-id="d65e3-122">Dodaj do Twojej `using` instrukcji:</span><span class="sxs-lookup"><span data-stu-id="d65e3-122">Add to your `using` statements:</span></span>
  
      using Microsoft.Azure.Engagement;
* <span data-ttu-id="d65e3-123">Zastąp `Page` z `EngagementPage`:</span><span class="sxs-lookup"><span data-stu-id="d65e3-123">Replace `Page` with `EngagementPage`:</span></span>

<span data-ttu-id="d65e3-124">**Bez usługi Engagement:**</span><span class="sxs-lookup"><span data-stu-id="d65e3-124">**Without Engagement:**</span></span>

        namespace Example
        {
          public sealed partial class ExamplePage : Page
          {
            [...]
          }
        }

<span data-ttu-id="d65e3-125">**Z usługi Engagement:**</span><span class="sxs-lookup"><span data-stu-id="d65e3-125">**With Engagement:**</span></span>

        using Microsoft.Azure.Engagement;

        namespace Example
        {
          public sealed partial class ExamplePage : EngagementPage
          {
            [...]
          }
        }

> [!IMPORTANT]
> <span data-ttu-id="d65e3-126">Jeśli strona zastępuje metodę `OnNavigatedTo`, nie zapomnij wywołać metody `base.OnNavigatedTo(e)`.</span><span class="sxs-lookup"><span data-stu-id="d65e3-126">If your page overrides the `OnNavigatedTo` method, be sure to call `base.OnNavigatedTo(e)`.</span></span> <span data-ttu-id="d65e3-127">W przeciwnym razie działanie nie został zgłoszony ( `EngagementPage` wywołania `StartActivity` wewnątrz jego `OnNavigatedTo` metody).</span><span class="sxs-lookup"><span data-stu-id="d65e3-127">Otherwise, the activity is not be reported (the `EngagementPage` calls `StartActivity` inside its `OnNavigatedTo` method).</span></span>
> 
> 

### <a name="xaml-file"></a><span data-ttu-id="d65e3-128">Plik XAML</span><span class="sxs-lookup"><span data-stu-id="d65e3-128">XAML file</span></span>
<span data-ttu-id="d65e3-129">Zmodyfikuj stronę `.xaml` pliku:</span><span class="sxs-lookup"><span data-stu-id="d65e3-129">Modify your page `.xaml` file:</span></span>

* <span data-ttu-id="d65e3-130">Dodaj deklaracje przestrzeni nazw:</span><span class="sxs-lookup"><span data-stu-id="d65e3-130">Add to your namespaces declarations:</span></span>
  
      xmlns:engagement="using:Microsoft.Azure.Engagement"
* <span data-ttu-id="d65e3-131">Zastąp `Page` z `engagement:EngagementPage`:</span><span class="sxs-lookup"><span data-stu-id="d65e3-131">Replace `Page` with `engagement:EngagementPage`:</span></span>

<span data-ttu-id="d65e3-132">**Bez usługi Engagement:**</span><span class="sxs-lookup"><span data-stu-id="d65e3-132">**Without Engagement:**</span></span>

        <Page>
            <!-- layout -->
            ...
        </Page>

<span data-ttu-id="d65e3-133">**Z usługi Engagement:**</span><span class="sxs-lookup"><span data-stu-id="d65e3-133">**With Engagement:**</span></span>

        <engagement:EngagementPage
            xmlns:engagement="using:Microsoft.Azure.Engagement">
            <!-- layout -->
            ...
        </engagement:EngagementPage >

### <a name="override-the-default-behaviour"></a><span data-ttu-id="d65e3-134">Zastąpienie zachowania domyślnego</span><span class="sxs-lookup"><span data-stu-id="d65e3-134">Override the default behaviour</span></span>
<span data-ttu-id="d65e3-135">Domyślnie nazwa klasy strony został zgłoszony jako nazwę działania, bez dodatkowych.</span><span class="sxs-lookup"><span data-stu-id="d65e3-135">By default, the class name of the page is reported as the activity name, with no extra.</span></span> <span data-ttu-id="d65e3-136">Jeśli klasa korzysta z sufiksem "Page", Engagement usuwa go.</span><span class="sxs-lookup"><span data-stu-id="d65e3-136">If the class uses the "Page" suffix, Engagement removes it.</span></span>

<span data-ttu-id="d65e3-137">Aby zastąpić domyślne zachowanie dla nazwy, Dodaj ten kod:</span><span class="sxs-lookup"><span data-stu-id="d65e3-137">To override the default behavior for the name, add this code:</span></span>

        // in the .xaml.cs file
        protected override string GetEngagementPageName()
        {
          /* your code */
          return "new name";
        }

<span data-ttu-id="d65e3-138">Aby zgłosić dodatkowe informacje o Twoich działaniach, Dodaj ten kod:</span><span class="sxs-lookup"><span data-stu-id="d65e3-138">To report extra information with your activity, add this code:</span></span>

        // in the .xaml.cs file
        protected override Dictionary<object,object> GetEngagementPageExtra()
        {
          /* your code */
          return extra;
        }

<span data-ttu-id="d65e3-139">Te metody są wywoływane z poziomu `OnNavigatedTo` metody na stronie.</span><span class="sxs-lookup"><span data-stu-id="d65e3-139">These methods are called from within the `OnNavigatedTo` method of your page.</span></span>

### <a name="alternate-method-call-startactivity-manually"></a><span data-ttu-id="d65e3-140">Alternatywna metoda: wywołanie `StartActivity()` ręcznie</span><span class="sxs-lookup"><span data-stu-id="d65e3-140">Alternate method: call `StartActivity()` manually</span></span>
<span data-ttu-id="d65e3-141">Jeśli nie możesz lub nie było przeciążyć Twojej `Page` klas, zamiast tego można uruchomić działań przez wywołanie metody `EngagementAgent` metody bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="d65e3-141">If you cannot or do not want to overload your `Page` classes, you can instead start your activities by calling `EngagementAgent` methods directly.</span></span>

<span data-ttu-id="d65e3-142">Firma Microsoft zaleca wywoływania `StartActivity` wewnątrz sieci `OnNavigatedTo` metody na stronie.</span><span class="sxs-lookup"><span data-stu-id="d65e3-142">We recommend calling `StartActivity` inside your `OnNavigatedTo` method of your Page.</span></span>

            protected override void OnNavigatedTo(NavigationEventArgs e)
            {
              base.OnNavigatedTo(e);
              EngagementAgent.Instance.StartActivity("MyPage");
            }

> [!IMPORTANT]
> <span data-ttu-id="d65e3-143">Upewnij się, że prawidłowo zakończyć sesję.</span><span class="sxs-lookup"><span data-stu-id="d65e3-143">Ensure you end your session correctly.</span></span>
> 
> <span data-ttu-id="d65e3-144">Uniwersalny zestaw SDK systemu Windows automatycznie wywołuje `EndActivity` metody, gdy aplikacja zostanie zamknięta.</span><span class="sxs-lookup"><span data-stu-id="d65e3-144">The Windows Universal SDK automatically calls the `EndActivity` method when the application is closed.</span></span> <span data-ttu-id="d65e3-145">W związku z tym jest **wysokiej** zaleca, aby wywołać `StartActivity` metody zmianie aktywności użytkownika i **nigdy** wywołać `EndActivity` — metoda.</span><span class="sxs-lookup"><span data-stu-id="d65e3-145">Thus, it is **HIGHLY** recommended to call the `StartActivity` method whenever the activity of the user change, and to **NEVER** call the `EndActivity` method.</span></span> <span data-ttu-id="d65e3-146">Ta metoda powiadamia serwer zaangażowania, że bieżący użytkownik opuścił aplikacji, która będzie miało wpływ na wszystkie dzienniki aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d65e3-146">This method notifies the Engagement server that the current user has left the application, which will impact all application logs.</span></span>
> 
> 

## <a name="advanced-reporting"></a><span data-ttu-id="d65e3-147">Zaawansowane raportowanie</span><span class="sxs-lookup"><span data-stu-id="d65e3-147">Advanced reporting</span></span>
<span data-ttu-id="d65e3-148">Opcjonalnie, warto zgłaszać zdarzenia specyficzne dla aplikacji, błędy i zadań, aby to zrobić, użyj metody znaleziono w inne `EngagementAgent` klasy.</span><span class="sxs-lookup"><span data-stu-id="d65e3-148">Optionally, you may want to report application-specific events, errors and jobs, to do so, use the others methods found in the `EngagementAgent` class.</span></span> <span data-ttu-id="d65e3-149">Interfejs API usługi Engagement umożliwia korzystanie z zaawansowanych możliwości wszystkich zaangażowania.</span><span class="sxs-lookup"><span data-stu-id="d65e3-149">The Engagement API allows use of all Engagement's advanced capabilities.</span></span>

<span data-ttu-id="d65e3-150">Aby uzyskać więcej informacji, zobacz [sposobu korzystania z zaawansowanych Mobile Engagement znakowanie interfejsu API w aplikacji uniwersalnych systemu Windows](mobile-engagement-windows-store-use-engagement-api.md).</span><span class="sxs-lookup"><span data-stu-id="d65e3-150">For further information, see [How to use the advanced Mobile Engagement tagging API in your Windows Universal app](mobile-engagement-windows-store-use-engagement-api.md).</span></span>

