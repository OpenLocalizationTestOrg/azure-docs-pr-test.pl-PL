---
title: "Wprowadzenie do usługi Azure Mobile Engagement na potrzeby platformy Xamarin.iOS"
description: "Dowiedz się, jak używać usługi Azure Mobile Engagement z funkcją analizy i powiadomieniami wypychanymi na potrzeby aplikacji platformy Xamarin.iOS."
services: mobile-engagement
documentationcenter: xamarin
author: piyushjo
manager: erikre
editor: 
ms.assetid: 0448209e-fff6-47bd-985c-2cf074bac12f
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-ios
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 9938c3e994acf31244825b1afb347f8c9f90ebe3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-xamarinios-apps"></a><span data-ttu-id="b89bd-103">Rozpoczynanie pracy z usługą Azure Mobile Engagement na potrzeby aplikacji platformy Xamarin.iOS</span><span class="sxs-lookup"><span data-stu-id="b89bd-103">Get Started with Azure Mobile Engagement for Xamarin.iOS Apps</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="b89bd-104">W tym temacie pokazano, jak za pomocą usługi Azure Mobile Engagement można określić sposób użycia aplikacji oraz wysyłać powiadomienia wypychane do segmentowanych użytkowników aplikacji platformy Xamarin.iOS.</span><span class="sxs-lookup"><span data-stu-id="b89bd-104">This topic shows you how to use Azure Mobile Engagement to understand your app usage and send push notifications to segmented users in a Xamarin.iOS application.</span></span>
<span data-ttu-id="b89bd-105">W tym samouczku zostanie utworzona pusta aplikacja platformy Xamarin.iOS służąca do zbierania danych podstawowych i odbierania powiadomień wypychanych przy użyciu systemu Apple Push Notification System (APNS).</span><span class="sxs-lookup"><span data-stu-id="b89bd-105">In this tutorial, you create a blank Xamarin.iOS app that collects basic data and receives push notifications using Apple Push Notification System (APNS).</span></span>

> [!NOTE]
> <span data-ttu-id="b89bd-106">Usługa Azure Mobile Engagement zostanie wycofana w marcu 2018 r. i jest obecnie dostępna wyłącznie dla dotychczasowych klientów.</span><span class="sxs-lookup"><span data-stu-id="b89bd-106">The Azure Mobile Engagement service will be retired March 2018 and is currently only available to existing customers.</span></span> <span data-ttu-id="b89bd-107">Aby uzyskać więcej informacji, zobacz [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span><span class="sxs-lookup"><span data-stu-id="b89bd-107">For more information, see [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span></span>

<span data-ttu-id="b89bd-108">Dla tego samouczka wymagane są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="b89bd-108">This tutorial requires the following:</span></span>

* <span data-ttu-id="b89bd-109">Program [Xamarin Studio](http://xamarin.com/studio).</span><span class="sxs-lookup"><span data-stu-id="b89bd-109">[Xamarin Studio](http://xamarin.com/studio).</span></span> <span data-ttu-id="b89bd-110">Można również użyć programu Visual Studio z platformą Xamarin, ale w tym samouczku używany jest program Xamarin Studio.</span><span class="sxs-lookup"><span data-stu-id="b89bd-110">You can also use Visual Studio with Xamarin but this tutorial uses Xamarin Studio.</span></span> <span data-ttu-id="b89bd-111">Aby uzyskać instrukcje dotyczące instalowania, zobacz [Instalator i instalacja programu Visual Studio i platformy Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).</span><span class="sxs-lookup"><span data-stu-id="b89bd-111">For installation instructions, see [Setup and Install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).</span></span> 
* [<span data-ttu-id="b89bd-112">Zestaw SDK platformy Xamarin usługi Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="b89bd-112">Mobile Engagement Xamarin SDK</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Engagement.Xamarin/)

> [!NOTE]
> <span data-ttu-id="b89bd-113">Do wykonania kroków tego samouczka potrzebne jest aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="b89bd-113">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="b89bd-114">Jeśli go nie masz, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut.</span><span class="sxs-lookup"><span data-stu-id="b89bd-114">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="b89bd-115">Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-xamarin-ios-get-started).</span><span class="sxs-lookup"><span data-stu-id="b89bd-115">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-xamarin-ios-get-started).</span></span>
> 
> 

## <span data-ttu-id="b89bd-116"><a id="setup-azme"></a>Konfigurowanie usługi Mobile Engagement dla aplikacji systemu iOS</span><span class="sxs-lookup"><span data-stu-id="b89bd-116"><a id="setup-azme"></a>Setup Mobile Engagement for your iOS app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="b89bd-117"><a id="connecting-app"></a>Łączenie aplikacji z zapleczem usługi Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="b89bd-117"><a id="connecting-app"></a>Connect your app to the Mobile Engagement backend</span></span>
<span data-ttu-id="b89bd-118">Ten samouczek przedstawia „podstawową integrację”, tj. minimalny zestaw wymagany do zbierania danych i wysyłania powiadomień wypychanych.</span><span class="sxs-lookup"><span data-stu-id="b89bd-118">This tutorial presents a "basic integration" which is the minimal set required to collect data and send a push notification.</span></span>

<span data-ttu-id="b89bd-119">Aby zademonstrować integrację, utworzona zostanie podstawowa aplikacja za pomocą platformy Xamarin:</span><span class="sxs-lookup"><span data-stu-id="b89bd-119">We will create a basic app with Xamarin to demonstrate the integration:</span></span>

### <a name="create-a-new-xamarinios-project"></a><span data-ttu-id="b89bd-120">Tworzenie nowego projektu platformy Xamarin.iOS</span><span class="sxs-lookup"><span data-stu-id="b89bd-120">Create a new Xamarin.iOS project</span></span>
1. <span data-ttu-id="b89bd-121">Uruchom program Xamarin Studio.</span><span class="sxs-lookup"><span data-stu-id="b89bd-121">Launch Xamarin Studio.</span></span> <span data-ttu-id="b89bd-122">Wybierz pozycję **File** (Plik)  -> **New** (Nowy) -> **Solution** (Rozwiązanie).</span><span class="sxs-lookup"><span data-stu-id="b89bd-122">Go to **File** -> **New** -> **Solution**</span></span> 
   
    ![][1]
2. <span data-ttu-id="b89bd-123">Wybierz pozycję **Single View App** (Aplikacja z jednym widokiem), upewnij się, że wybrany język to **C#**, a następnie kliknij przycisk **Next** (Dalej).</span><span class="sxs-lookup"><span data-stu-id="b89bd-123">Select **Single View App**, make sure the selected language is **C#** and then click **Next**.</span></span>
   
    ![][2]
3. <span data-ttu-id="b89bd-124">Wypełnij pole **App Name** (Nazwa aplikacji) i **Organization Identifier** (Identyfikator organizacji), a następnie kliknij przycisk **Next** (Dalej).</span><span class="sxs-lookup"><span data-stu-id="b89bd-124">Fill in the **App Name** and the **Organization Identifier** and then click **Next**.</span></span> 
   
    ![][3]
   
   > [!IMPORTANT]
   > <span data-ttu-id="b89bd-125">Upewnij się, że profil publikowania, który ostatecznie zostanie użyty do wdrożenia aplikacji systemu iOS używa identyfikatora aplikacji zgodnego z identyfikatorem pakietu z tej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b89bd-125">Make sure that the publishing profile you eventually use to deploy your iOS app is using an App ID which matches exactly with the Bundle Identifier you have here.</span></span> 
   > 
   > 
4. <span data-ttu-id="b89bd-126">Jeśli to będzie konieczne, zaktualizuj pola **Project Name** (Nazwa projektu), **Solution Name** (Nazwa rozwiązania) i **Location** (Lokalizacja), a następnie kliknij pozycję **Create** (Utwórz).</span><span class="sxs-lookup"><span data-stu-id="b89bd-126">Update the **Project Name**, **Solution Name** and **Location** if required and click **Create**.</span></span>
   
    ![][4]

<span data-ttu-id="b89bd-127">Za pomocą platformy Xamarin Studio zostanie utworzona aplikacja demonstracyjna, w której zostanie zintegrowana usługa Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="b89bd-127">Xamarin Studio will create the demo app in which we will integrate Mobile Engagement.</span></span> 

### <a name="connect-your-app-to-mobile-engagement-backend"></a><span data-ttu-id="b89bd-128">Łączenie aplikacji z zapleczem usługi Mobile Engagement </span><span class="sxs-lookup"><span data-stu-id="b89bd-128">Connect your app to Mobile Engagement backend</span></span>
1. <span data-ttu-id="b89bd-129">Kliknij prawym przyciskiem myszy folder **Packages** w oknie Solution (Rozwiązanie), a następnie wybierz pozycję **Add Packages** (Dodaj pakiety).</span><span class="sxs-lookup"><span data-stu-id="b89bd-129">Right click the **Packages** folder in the Solution windows and select **Add Packages...**</span></span>
   
    ![][5]
2. <span data-ttu-id="b89bd-130">Wyszukaj zestaw **Microsoft Azure Mobile Engagement Xamarin SDK** i dodaj go do swojego rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="b89bd-130">Search for the **Microsoft Azure Mobile Engagement Xamarin SDK** and add it to your solution.</span></span>  
   
    ![][6]
3. <span data-ttu-id="b89bd-131">Otwórz plik **AppDelegate.cs** i dodaj następującą instrukcję using:</span><span class="sxs-lookup"><span data-stu-id="b89bd-131">Open **AppDelegate.cs** and add the following using statement:</span></span>
   
        using Microsoft.Azure.Engagement.Xamarin;
4. <span data-ttu-id="b89bd-132">W metodzie **FinishedLaunching** dodaj następujący kod, aby zainicjować połączenie z zapleczem usługi Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="b89bd-132">In the **FinishedLaunching** method, add the following to initialize the connection with Mobile Engagement backend.</span></span> <span data-ttu-id="b89bd-133">Upewnij się, że został dodany element **ConnectionString**.</span><span class="sxs-lookup"><span data-stu-id="b89bd-133">Make sure to add your **ConnectionString**.</span></span> <span data-ttu-id="b89bd-134">Ten kod zawiera również zastępczy element **NotificationIcon** dodawany przez zestaw SDK usługi Mobile Engagement Mobile, który można zastąpić.</span><span class="sxs-lookup"><span data-stu-id="b89bd-134">This code also uses a dummy **NotificationIcon** which is added by the Mobile Engagement SDK which you may want to replace.</span></span> 
   
        EngagementConfiguration config = new EngagementConfiguration {
                        ConnectionString = "YourConnectionStringFromAzurePortal",
                        NotificationIcon = UIImage.FromBundle("close")
                    };
        EngagementAgent.Init (config);

## <span data-ttu-id="b89bd-135"><a id="monitor"></a>Włączanie monitorowania w czasie rzeczywistym</span><span class="sxs-lookup"><span data-stu-id="b89bd-135"><a id="monitor"></a>Enabling real-time monitoring</span></span>
<span data-ttu-id="b89bd-136">Aby rozpocząć wysyłanie danych i sprawdzić, czy użytkownicy są aktywni, konieczne jest wysłanie co najmniej jednego ekranu do zaplecza usługi Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="b89bd-136">In order to start sending data and ensuring the users are active, you must send at least one screen to the Mobile Engagement backend.</span></span>

1. <span data-ttu-id="b89bd-137">Otwórz plik **ViewController.cs** i dodaj następującą instrukcję using:</span><span class="sxs-lookup"><span data-stu-id="b89bd-137">Open **ViewController.cs** and add the following using statement:</span></span>
   
        using Microsoft.Azure.Engagement.Xamarin;
2. <span data-ttu-id="b89bd-138">Zastąp klasy, w których klasa `ViewController` dziedziczy z klasy `UIViewController`, klasą `EngagementViewController`.</span><span class="sxs-lookup"><span data-stu-id="b89bd-138">Replace the class from which `ViewController` inherits from `UIViewController` to `EngagementViewController`.</span></span> 

## <span data-ttu-id="b89bd-139"><a id="monitor"></a>Łączenie aplikacji z funkcją monitorowania w czasie rzeczywistym</span><span class="sxs-lookup"><span data-stu-id="b89bd-139"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="b89bd-140"><a id="integrate-push"></a>Włączanie powiadomień wypychanych i funkcji komunikatów w aplikacji</span><span class="sxs-lookup"><span data-stu-id="b89bd-140"><a id="integrate-push"></a>Enable push notifications and in-app messaging</span></span>
<span data-ttu-id="b89bd-141">Usługa Mobile Engagement umożliwia wchodzenie w interakcję z użytkownikami i modułem REACH przy użyciu powiadomień wypychanych i komunikatów w aplikacji w kontekście kampanii.</span><span class="sxs-lookup"><span data-stu-id="b89bd-141">Mobile Engagement allows you to interact with your users and REACH with push notifications and in-app messaging in the context of campaigns.</span></span> <span data-ttu-id="b89bd-142">Ten moduł w portalu Mobile Engagement ma nazwę REACH.</span><span class="sxs-lookup"><span data-stu-id="b89bd-142">This module is called REACH in the Mobile Engagement portal.</span></span>
<span data-ttu-id="b89bd-143">W poniższych sekcjach aplikacja zostanie skonfigurowana do ich odbierania.</span><span class="sxs-lookup"><span data-stu-id="b89bd-143">The following sections set up your app to receive them.</span></span>

### <a name="modify-your-application-delegate"></a><span data-ttu-id="b89bd-144">Modyfikowanie delegata aplikacji</span><span class="sxs-lookup"><span data-stu-id="b89bd-144">Modify your Application Delegate</span></span>
1. <span data-ttu-id="b89bd-145">Otwórz plik **AppDelegate.cs** i dodaj następującą instrukcję using:</span><span class="sxs-lookup"><span data-stu-id="b89bd-145">Open the **AppDelegate.cs** and add the following using statement:</span></span>
   
        using System; 
2. <span data-ttu-id="b89bd-146">Teraz wewnątrz metody `FinishedLaunching` dodaj następujący kod służący do rejestrowania wiadomości wypychanych poniżej metody `EngagementAgent.init(...)`</span><span class="sxs-lookup"><span data-stu-id="b89bd-146">Now inside the `FinishedLaunching` method, add the following to register for push messages after `EngagementAgent.init(...)`</span></span>
   
        if (UIDevice.CurrentDevice.CheckSystemVersion(8,0))
        {
            var pushSettings = UIUserNotificationSettings.GetSettingsForTypes (
                (UIUserNotificationType.Badge |
                    UIUserNotificationType.Sound |
                    UIUserNotificationType.Alert),
                null);
            UIApplication.SharedApplication.RegisterUserNotificationSettings (pushSettings);
            UIApplication.SharedApplication.RegisterForRemoteNotifications ();
        }
        else
        {
            UIApplication.SharedApplication.RegisterForRemoteNotificationTypes (
                UIRemoteNotificationType.Badge |
                UIRemoteNotificationType.Sound |
                UIRemoteNotificationType.Alert);
        }
3. <span data-ttu-id="b89bd-147">Na koniec zaktualizuj lub dodaj następujące metody:</span><span class="sxs-lookup"><span data-stu-id="b89bd-147">Finally - update or add the following methods:</span></span>
   
        public override void DidReceiveRemoteNotification (UIApplication application, NSDictionary userInfo, 
            Action<UIBackgroundFetchResult> completionHandler)
        {
            EngagementAgent.ApplicationDidReceiveRemoteNotification(userInfo, completionHandler);
        }
   
        public override void RegisteredForRemoteNotifications (UIApplication application, NSData deviceToken)
        {
            // Register device token on Engagement
            EngagementAgent.RegisterDeviceToken(deviceToken);
        }
   
        public override void FailedToRegisterForRemoteNotifications(UIApplication application, NSError error)
        {
            Console.WriteLine("Failed to register for remote notifications: Error '{0}'", error);
        }
4. <span data-ttu-id="b89bd-148">Upewnij się, że na liście właściwości **Info.plist** rozwiązania wartość pozycji **Bundle Identifier** (Identyfikator pakietu) jest zgodna z **identyfikatorem aplikacji** znajdującym się w profilu aprowizacji w Centrum deweloperów firmy Apple.</span><span class="sxs-lookup"><span data-stu-id="b89bd-148">In your **Info.plist** file in the solution, confirm that the **Bundle Identifier** matches with the **App ID** you have in your provisioning profile in the Apple Dev Center.</span></span> 
   
    ![][7]
5. <span data-ttu-id="b89bd-149">Upewnij się również, że na tej samej liście właściwości **Info.plist** zaznaczono pole wyboru **Enable Background Modes** (Włącz tryby w tle) i **Remote Notifications** (Powiadomienia zdalne).</span><span class="sxs-lookup"><span data-stu-id="b89bd-149">In the same **Info.plist** file, make sure that you have checked the **Enable Background Modes** and **Remote Notifications**.</span></span> 
   
     ![][8]
6. <span data-ttu-id="b89bd-150">Uruchom aplikację na urządzeniu skojarzonym z tym profilem publikowania.</span><span class="sxs-lookup"><span data-stu-id="b89bd-150">Run the app on the device you have associated with this publishing profile.</span></span> 

[!INCLUDE [mobile-engagement-ios-send-push-push](../../includes/mobile-engagement-ios-send-push.md)]

<!-- Images. -->
[1]: ./media/mobile-engagement-xamarin-ios-get-started/new-solution.png
[2]: ./media/mobile-engagement-xamarin-ios-get-started/app-type.png
[3]: ./media/mobile-engagement-xamarin-ios-get-started/configure-project-name.png
[4]: ./media/mobile-engagement-xamarin-ios-get-started/configure-project-confirm.png
[5]: ./media/mobile-engagement-xamarin-ios-get-started/add-nuget.png
[6]: ./media/mobile-engagement-xamarin-ios-get-started/add-nuget-azme.png
[7]: ./media/mobile-engagement-xamarin-ios-get-started/info-plist-confirm-bundle.png
[8]: ./media/mobile-engagement-xamarin-ios-get-started/info-plist-configure-push.png
