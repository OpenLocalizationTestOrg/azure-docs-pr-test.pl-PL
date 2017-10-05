---
title: "Wprowadzenie do usługi Azure Mobile Engagement na potrzeby aplikacji platformy Silverlight systemu Windows Phone"
description: "Dowiedz się, jak używać usługi Azure Mobile Engagement z funkcją analizy i powiadomieniami wypychanymi na potrzeby aplikacji platformy Silverlight systemu Windows Phone."
services: mobile-engagement
documentationcenter: windows
author: piyushjo
manager: erikre
editor: 
ms.assetid: aa34692f-87f7-47c6-a20c-a1972750bc25
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: d2334a59d83c90bdd02c4fa29261d36aad292892
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-windows-phone-silverlight-apps"></a><span data-ttu-id="ebd5b-103">Wprowadzenie do usługi Azure Mobile Engagement na potrzeby aplikacji platformy Silverlight systemu Windows Phone</span><span class="sxs-lookup"><span data-stu-id="ebd5b-103">Get started with Azure Mobile Engagement for Windows Phone Silverlight apps</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="ebd5b-104">W tym temacie pokazano, jak za pomocą usługi Azure Mobile Engagement można określić sposób użycia aplikacji oraz wysyłać powiadomienia wypychane do segmentowanych użytkowników aplikacji platformy Silverlight systemu Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="ebd5b-104">This topic shows you how to use Azure Mobile Engagement to understand your app usage and send push notifications to segmented users of a Windows Phone Silverlight application.</span></span>
<span data-ttu-id="ebd5b-105">W tym samouczku został omówiony prosty scenariusz emisji przy użyciu usługi Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="ebd5b-105">This tutorial demonstrates the simple broadcast scenario using Mobile Engagement.</span></span> <span data-ttu-id="ebd5b-106">W ramach tego samouczka utworzona zostanie pusta aplikacja platformy Silverlight systemu Windows Phone, za pomocą której będą zbierane podstawowe dane i odbierane powiadomienia wypychane przy użyciu Usługi powiadomień systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="ebd5b-106">In it, you create a blank Windows Phone Silverlight app that collects basic data and receives push notifications using Microsoft Push Notification Service (MPNS).</span></span>

> [!NOTE]
> <span data-ttu-id="ebd5b-107">Usługa Azure Mobile Engagement zostanie wycofana w marcu 2018 r. i jest obecnie dostępna wyłącznie dla dotychczasowych klientów.</span><span class="sxs-lookup"><span data-stu-id="ebd5b-107">The Azure Mobile Engagement service will be retired March 2018 and is currently only available to existing customers.</span></span> <span data-ttu-id="ebd5b-108">Aby uzyskać więcej informacji, zobacz [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span><span class="sxs-lookup"><span data-stu-id="ebd5b-108">For more information, see [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span></span>

> [!NOTE]
> <span data-ttu-id="ebd5b-109">Projekty systemu Windows Phone 8.1 i wcześniejszych nie są obsługiwane w programie Visual Studio 2017 r.</span><span class="sxs-lookup"><span data-stu-id="ebd5b-109">Windows Phone 8.1 and prior version projects are not supported in Visual Studio 2017.</span></span>  <span data-ttu-id="ebd5b-110">Aby uzyskać więcej informacji, zobacz [Obsługiwane platformy i zgodność programu Visual Studio 2017](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span><span class="sxs-lookup"><span data-stu-id="ebd5b-110">For more information, see [Visual Studio 2017 Platform Targeting and Compatibility](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span></span>

> [!NOTE]
> <span data-ttu-id="ebd5b-111">Jeśli aplikacja ma być przeznaczona zarówno dla systemu Windows Phone 8.1 (bez użycia platformy Silverlight), dodatkowe informacje można zawiera [Samouczek aplikacji uniwersalnych systemu Windows](mobile-engagement-windows-store-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="ebd5b-111">If you are targeting Windows Phone 8.1 (non-Silverlight), refer to the [Windows Universal tutorial](mobile-engagement-windows-store-dotnet-get-started.md).</span></span>
> 
> 

<span data-ttu-id="ebd5b-112">Dla tego samouczka wymagane są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="ebd5b-112">This tutorial requires the following:</span></span>

* <span data-ttu-id="ebd5b-113">Program Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="ebd5b-113">Visual Studio 2013</span></span>
* <span data-ttu-id="ebd5b-114">Pakiet NuGet [MicrosoftAzure.MobileEngagement]</span><span class="sxs-lookup"><span data-stu-id="ebd5b-114">[MicrosoftAzure.MobileEngagement] Nuget package</span></span>

> [!NOTE]
> <span data-ttu-id="ebd5b-115">Do wykonania kroków tego samouczka potrzebne jest aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ebd5b-115">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="ebd5b-116">Jeśli go nie masz, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut.</span><span class="sxs-lookup"><span data-stu-id="ebd5b-116">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="ebd5b-117">Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-windows-phone-get-started).</span><span class="sxs-lookup"><span data-stu-id="ebd5b-117">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-windows-phone-get-started).</span></span>
> 
> 

## <span data-ttu-id="ebd5b-118"><a id="setup-azme"></a>Konfigurowanie usługi Mobile Engagement dla aplikacji systemu Windows Phone</span><span class="sxs-lookup"><span data-stu-id="ebd5b-118"><a id="setup-azme"></a>Setup Mobile Engagement for your Windows Phone app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="ebd5b-119"><a id="connecting-app"></a>Łączenie aplikacji z zapleczem usługi Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="ebd5b-119"><a id="connecting-app"></a>Connect your app to the Mobile Engagement backend</span></span>
<span data-ttu-id="ebd5b-120">Ten samouczek przedstawia „podstawową integrację”, tj. minimalny zestaw wymagany do zbierania danych i wysyłania powiadomień wypychanych.</span><span class="sxs-lookup"><span data-stu-id="ebd5b-120">This tutorial presents a "basic integration", which is the minimal set required to collect data and send a push notification.</span></span> <span data-ttu-id="ebd5b-121">Kompletna dokumentacja integracji znajduje się w sekcji [Mobile Engagement Windows Phone SDK integration](mobile-engagement-windows-phone-sdk-overview.md) (Integracja zestawu SDK dla systemu Windows Phone usługi Mobile Engagement).</span><span class="sxs-lookup"><span data-stu-id="ebd5b-121">The complete integration documentation can be found in the [Mobile Engagement Windows Phone SDK integration](mobile-engagement-windows-phone-sdk-overview.md)</span></span>

<span data-ttu-id="ebd5b-122">Aby zademonstrować integrację, utworzona zostanie podstawowa aplikacja za pomocą programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ebd5b-122">We will create a basic app with Visual Studio to demonstrate the integration.</span></span>

### <a name="create-a-new-windows-phone-silverlight-project"></a><span data-ttu-id="ebd5b-123">Tworzenie nowego projektu platformy Silverlight systemu Windows Phone</span><span class="sxs-lookup"><span data-stu-id="ebd5b-123">Create a new Windows Phone Silverlight project</span></span>
<span data-ttu-id="ebd5b-124">W następujących krokach założono korzystanie z programu Visual Studio 2015, chociaż kroki są podobne także w przypadku wcześniejszych wersji programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ebd5b-124">The following steps assume the use of Visual Studio 2015 though the steps are similar in earlier versions of Visual Studio.</span></span> 

1. <span data-ttu-id="ebd5b-125">Uruchom program Visual Studio i na ekranie **Strona główna** wybierz pozycję **Nowy projekt**.</span><span class="sxs-lookup"><span data-stu-id="ebd5b-125">Start Visual Studio, and in the **Home** screen, select **New Project**.</span></span>
2. <span data-ttu-id="ebd5b-126">W oknie podręcznym wybierz pozycję **Windows 8** -> **Windows Phone** -> **Pusta aplikacja (Windows Phone Silverlight)**.</span><span class="sxs-lookup"><span data-stu-id="ebd5b-126">In the pop-up, select **Windows 8** -> **Windows Phone** -> **Blank App (Windows Phone Silverlight)**.</span></span> <span data-ttu-id="ebd5b-127">Wypełnij pola **Nazwa** i **Nazwa rozwiązania**, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="ebd5b-127">Fill in the app **Name** and **Solution name**, and then click **OK**.</span></span>
   
    ![][1]
3. <span data-ttu-id="ebd5b-128">Można wybrać system docelowy: **Windows Phone 8.0** lub **Windows Phone 8.1**.</span><span class="sxs-lookup"><span data-stu-id="ebd5b-128">You can choose to target either **Windows Phone 8.0** or **Windows Phone 8.1**.</span></span>

<span data-ttu-id="ebd5b-129">Została utworzona nowa aplikacja platformy Silverlight systemu Windows Phone, z którą zostanie zintegrowany zestaw SDK usługi Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="ebd5b-129">You have now created a new Windows Phone Silverlight app into which we will integrate the Azure Mobile Engagement SDK.</span></span>

### <a name="connect-your-app-to-the-mobile-engagement-backend"></a><span data-ttu-id="ebd5b-130">Łączenie aplikacji z zapleczem usługi Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="ebd5b-130">Connect your app to the Mobile Engagement backend</span></span>
1. <span data-ttu-id="ebd5b-131">Zainstaluj pakiet NuGet [MicrosoftAzure.MobileEngagement] w projekcie.</span><span class="sxs-lookup"><span data-stu-id="ebd5b-131">Install the [MicrosoftAzure.MobileEngagement] nuget package in your project.</span></span>
2. <span data-ttu-id="ebd5b-132">Otwórz plik `WMAppManifest.xml` (w folderze Właściwości) i upewnij się, że w znaczniku `<Capabilities />` został zadeklarowany następujący kod:</span><span class="sxs-lookup"><span data-stu-id="ebd5b-132">Open `WMAppManifest.xml` (under the Properties folder) and make sure the following are declared (add them if they are not) in the `<Capabilities />` tag:</span></span>
   
        <Capability Name="ID_CAP_NETWORKING" />
        <Capability Name="ID_CAP_IDENTITY_DEVICE" />
   
    ![][2]
3. <span data-ttu-id="ebd5b-133">Teraz wklej parametry połączenia, które wcześniej zostały skopiowane dla aplikacji usługi Mobile Engagement, a następnie wklej je do pliku `Resources\EngagementConfiguration.xml` między znaczniki `<connectionString>` i `</connectionString>`:</span><span class="sxs-lookup"><span data-stu-id="ebd5b-133">Now paste the connection string that you copied earlier for your Mobile Engagement app and paste it in the `Resources\EngagementConfiguration.xml` file, between the `<connectionString>` and `</connectionString>` tags:</span></span>
   
    ![][3]
4. <span data-ttu-id="ebd5b-134">W pliku `App.xaml.cs`:</span><span class="sxs-lookup"><span data-stu-id="ebd5b-134">In the `App.xaml.cs` file:</span></span>
   
    <span data-ttu-id="ebd5b-135">a.</span><span class="sxs-lookup"><span data-stu-id="ebd5b-135">a.</span></span> <span data-ttu-id="ebd5b-136">Dodaj instrukcję `using`:</span><span class="sxs-lookup"><span data-stu-id="ebd5b-136">Add the `using` statement:</span></span>
   
            using Microsoft.Azure.Engagement;
   
    <span data-ttu-id="ebd5b-137">b.</span><span class="sxs-lookup"><span data-stu-id="ebd5b-137">b.</span></span> <span data-ttu-id="ebd5b-138">Zainicjuj zestaw SDK w metodzie `Application_Launching`:</span><span class="sxs-lookup"><span data-stu-id="ebd5b-138">Initialize the SDK in the `Application_Launching` method:</span></span>
   
            private void Application_Launching(object sender, LaunchingEventArgs e)
            {
              EngagementAgent.Instance.Init();
            }
   
    <span data-ttu-id="ebd5b-139">c.</span><span class="sxs-lookup"><span data-stu-id="ebd5b-139">c.</span></span> <span data-ttu-id="ebd5b-140">Wstaw następujący kod w metodzie `Application_Activated`:</span><span class="sxs-lookup"><span data-stu-id="ebd5b-140">Insert the following in the `Application_Activated`:</span></span>
   
            private void Application_Activated(object sender, ActivatedEventArgs e)
            {
               EngagementAgent.Instance.OnActivated(e);
            }

## <span data-ttu-id="ebd5b-141"><a id="monitor"></a>Włączanie monitorowania w czasie rzeczywistym</span><span class="sxs-lookup"><span data-stu-id="ebd5b-141"><a id="monitor"></a>Enable real-time monitoring</span></span>
<span data-ttu-id="ebd5b-142">Aby rozpocząć wysyłanie danych i upewnić się, że użytkownicy są aktywni, konieczne jest wysłanie co najmniej jednego ekranu (Działanie) do zaplecza usługi Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="ebd5b-142">In order to start sending data and ensuring that the users are active, you must send at least one screen (Activity) to the Mobile Engagement backend.</span></span>

1. <span data-ttu-id="ebd5b-143">W pliku MainPage.xaml.cs dodaj instrukcję `using`:</span><span class="sxs-lookup"><span data-stu-id="ebd5b-143">In the MainPage.xaml.cs, add the `using` statement:</span></span>
   
        using Microsoft.Azure.Engagement;
2. <span data-ttu-id="ebd5b-144">Zastąp klasę podstawową **MainPage**, którą wcześniej była **PhoneApplicationPage**, klasą **EngagementPage**.</span><span class="sxs-lookup"><span data-stu-id="ebd5b-144">Replace the base class of **MainPage**, which is before **PhoneApplicationPage**, with **EngagementPage**.</span></span>
   
        class MainPage : EngagementPage 
3. <span data-ttu-id="ebd5b-145">W pliku `MainPage.xml`:</span><span class="sxs-lookup"><span data-stu-id="ebd5b-145">In your `MainPage.xml` file:</span></span>
   
    <span data-ttu-id="ebd5b-146">a.</span><span class="sxs-lookup"><span data-stu-id="ebd5b-146">a.</span></span> <span data-ttu-id="ebd5b-147">Dodaj deklaracje przestrzeni nazw:</span><span class="sxs-lookup"><span data-stu-id="ebd5b-147">Add to your namespaces declarations:</span></span>
   
            xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP"
   
    <span data-ttu-id="ebd5b-148">b.</span><span class="sxs-lookup"><span data-stu-id="ebd5b-148">b.</span></span> <span data-ttu-id="ebd5b-149">Zastąp element `phone:PhoneApplicationPage` w nazwie tagu XML elementem `engagement:EngagementPage`.</span><span class="sxs-lookup"><span data-stu-id="ebd5b-149">Replace `phone:PhoneApplicationPage` in the XML tag name with `engagement:EngagementPage`.</span></span>

## <span data-ttu-id="ebd5b-150"><a id="monitor"></a>Łączenie aplikacji z funkcją monitorowania w czasie rzeczywistym</span><span class="sxs-lookup"><span data-stu-id="ebd5b-150"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="ebd5b-151"><a id="integrate-push"></a>Włączanie powiadomień wypychanych i funkcji komunikatów w aplikacji</span><span class="sxs-lookup"><span data-stu-id="ebd5b-151"><a id="integrate-push"></a>Enable push notifications and in-app messaging</span></span>
<span data-ttu-id="ebd5b-152">Usługa Mobile Engagement umożliwia wchodzenie w interakcję z użytkownikami przy użyciu powiadomień wypychanych i komunikatów w aplikacji w kontekście kampanii.</span><span class="sxs-lookup"><span data-stu-id="ebd5b-152">Mobile Engagement allows you to interact and reach your users with Push Notifications and in-app Messaging in the context of campaigns.</span></span> <span data-ttu-id="ebd5b-153">Ten moduł w portalu Mobile Engagement ma nazwę REACH.</span><span class="sxs-lookup"><span data-stu-id="ebd5b-153">This module is called REACH in the Mobile Engagement portal.</span></span>
<span data-ttu-id="ebd5b-154">W poniższych sekcjach aplikacja zostanie skonfigurowana do ich odbierania.</span><span class="sxs-lookup"><span data-stu-id="ebd5b-154">The following sections set up your app to receive them.</span></span>

### <a name="enable-your-app-to-receive-mpns-push-notifications"></a><span data-ttu-id="ebd5b-155">Umożliwianie aplikacji otrzymywanie powiadomień wypychanych usługi MPNS</span><span class="sxs-lookup"><span data-stu-id="ebd5b-155">Enable your app to receive MPNS Push Notifications</span></span>
<span data-ttu-id="ebd5b-156">Dodaj nowe funkcje do pliku `WMAppManifest.xml`:</span><span class="sxs-lookup"><span data-stu-id="ebd5b-156">Add new Capabilities to your `WMAppManifest.xml` file:</span></span>

        ID_CAP_PUSH_NOTIFICATION
        ID_CAP_WEBBROWSERCOMPONENT

   ![][5]

### <a name="initialize-the-reach-sdk"></a><span data-ttu-id="ebd5b-157">Inicjowanie zestawu SDK modułu REACH</span><span class="sxs-lookup"><span data-stu-id="ebd5b-157">Initialize the REACH SDK</span></span>
1. <span data-ttu-id="ebd5b-158">W pliku `App.xaml.cs` wywołaj funkcję `EngagementReach.Instance.Init();` w funkcji **Application_Launching** bezpośrednio po zainicjowaniu agenta:</span><span class="sxs-lookup"><span data-stu-id="ebd5b-158">In `App.xaml.cs`, call `EngagementReach.Instance.Init();` in the **Application_Launching** function, right after the agent initialization:</span></span>
   
        private void Application_Launching(object sender, LaunchingEventArgs e)
        {
           EngagementAgent.Instance.Init();
           EngagementReach.Instance.Init();
        }
2. <span data-ttu-id="ebd5b-159">W pliku `App.xaml.cs` wywołaj funkcję `EngagementReach.Instance.OnActivated(e);` w funkcji **Application_Activated** bezpośrednio po zainicjowaniu agenta:</span><span class="sxs-lookup"><span data-stu-id="ebd5b-159">In `App.xaml.cs`, call `EngagementReach.Instance.OnActivated(e);` in the **Application_Activated** function, right after the agent initialization:</span></span>
   
        private void Application_Activated(object sender, ActivatedEventArgs e)
        {
           EngagementAgent.Instance.OnActivated(e);
           EngagementReach.Instance.OnActivated(e);
        }

<span data-ttu-id="ebd5b-160">Wszystko jest gotowe.</span><span class="sxs-lookup"><span data-stu-id="ebd5b-160">You're all set.</span></span> <span data-ttu-id="ebd5b-161">Teraz zostanie zweryfikowane, czy podstawowa integracja została przeprowadzona prawidłowo.</span><span class="sxs-lookup"><span data-stu-id="ebd5b-161">Now we will verify that you have correctly cried out this basic integration.</span></span>

## <span data-ttu-id="ebd5b-162"><a id="send"></a>Wysyłanie powiadomienia do aplikacji</span><span class="sxs-lookup"><span data-stu-id="ebd5b-162"><a id="send"></a>Send a notification to your app</span></span>
[!INCLUDE [Create Windows Push campaign](../../includes/mobile-engagement-windows-push-campaign.md)]

<span data-ttu-id="ebd5b-163">Na urządzeniu powinno zostać wyświetlone powiadomienie, które będzie widoczne jako powiadomienie w aplikacji, jeśli aplikacja jest otwarta, lub jeśli nie jest, jako powiadomienie wyskakujące mające postać zbliżoną do następującej:</span><span class="sxs-lookup"><span data-stu-id="ebd5b-163">You should now see a notification on your device which will show up as an in-app notification if the app is open otherwise as a toast notification like the following:</span></span> 

![][6]

<!-- URLs. -->
<span data-ttu-id="ebd5b-164">[MicrosoftAzure.MobileEngagement]: http://go.microsoft.com/?linkid=9874664</span><span class="sxs-lookup"><span data-stu-id="ebd5b-164">[MicrosoftAzure.MobileEngagement]: http://go.microsoft.com/?linkid=9874664</span></span>
[Mobile Engagement Windows Phone SDK documentation]: ../mobile-engagement-windows-phone-integrate-engagement/

<!-- Images. -->
[1]: ./media/mobile-engagement-windows-phone-get-started/project-properties.png
[2]: ./media/mobile-engagement-windows-phone-get-started/wmappmanifest-capabilities.png
[3]: ./media/mobile-engagement-windows-phone-get-started/add-connection-string.png
[5]: ./media/mobile-engagement-windows-phone-get-started/reach-capabilities.png
[6]: ./media/mobile-engagement-windows-phone-get-started/push-screenshot.png
