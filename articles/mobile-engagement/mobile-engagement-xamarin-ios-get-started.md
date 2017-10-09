---
title: aaaGet Started with Azure Mobile Engagement na potrzeby platformy Xamarin.iOS
description: "Dowiedz się, jak toouse usługi Azure Mobile Engagement z funkcją analizy i powiadomieniami Wypychanymi dla aplikacji platformy Xamarin.iOS."
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
ms.openlocfilehash: 02340a744753dcc5cd1b6888a5fa87628be47b68
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-xamarinios-apps"></a><span data-ttu-id="19aa9-103">Rozpoczynanie pracy z usługą Azure Mobile Engagement na potrzeby aplikacji platformy Xamarin.iOS</span><span class="sxs-lookup"><span data-stu-id="19aa9-103">Get Started with Azure Mobile Engagement for Xamarin.iOS Apps</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="19aa9-104">W tym temacie opisano sposób toounderstand usługi Azure Mobile Engagement toouse Twoje użycie aplikacji i wysyłania wypychanie powiadomień toosegmented użytkowników aplikacji platformy Xamarin.iOS.</span><span class="sxs-lookup"><span data-stu-id="19aa9-104">This topic shows you how toouse Azure Mobile Engagement toounderstand your app usage and send push notifications toosegmented users in a Xamarin.iOS application.</span></span>
<span data-ttu-id="19aa9-105">W tym samouczku zostanie utworzona pusta aplikacja platformy Xamarin.iOS służąca do zbierania danych podstawowych i odbierania powiadomień wypychanych przy użyciu systemu Apple Push Notification System (APNS).</span><span class="sxs-lookup"><span data-stu-id="19aa9-105">In this tutorial, you create a blank Xamarin.iOS app that collects basic data and receives push notifications using Apple Push Notification System (APNS).</span></span>

> [!NOTE]
> <span data-ttu-id="19aa9-106">Usługa Azure Mobile Engagement Hello zostaną wycofane 2018 marca i jest obecnie tylko dostępne tooexisting klientów.</span><span class="sxs-lookup"><span data-stu-id="19aa9-106">hello Azure Mobile Engagement service will be retired March 2018 and is currently only available tooexisting customers.</span></span> <span data-ttu-id="19aa9-107">Aby uzyskać więcej informacji, zobacz [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span><span class="sxs-lookup"><span data-stu-id="19aa9-107">For more information, see [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span></span>

<span data-ttu-id="19aa9-108">Ten samouczek wymaga następujących hello:</span><span class="sxs-lookup"><span data-stu-id="19aa9-108">This tutorial requires hello following:</span></span>

* <span data-ttu-id="19aa9-109">Program [Xamarin Studio](http://xamarin.com/studio).</span><span class="sxs-lookup"><span data-stu-id="19aa9-109">[Xamarin Studio](http://xamarin.com/studio).</span></span> <span data-ttu-id="19aa9-110">Można również użyć programu Visual Studio z platformą Xamarin, ale w tym samouczku używany jest program Xamarin Studio.</span><span class="sxs-lookup"><span data-stu-id="19aa9-110">You can also use Visual Studio with Xamarin but this tutorial uses Xamarin Studio.</span></span> <span data-ttu-id="19aa9-111">Aby uzyskać instrukcje dotyczące instalowania, zobacz [Instalator i instalacja programu Visual Studio i platformy Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).</span><span class="sxs-lookup"><span data-stu-id="19aa9-111">For installation instructions, see [Setup and Install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).</span></span> 
* [<span data-ttu-id="19aa9-112">Zestaw SDK platformy Xamarin usługi Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="19aa9-112">Mobile Engagement Xamarin SDK</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Engagement.Xamarin/)

> [!NOTE]
> <span data-ttu-id="19aa9-113">toocomplete tego samouczka, musi mieć aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="19aa9-113">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="19aa9-114">Jeśli go nie masz, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut.</span><span class="sxs-lookup"><span data-stu-id="19aa9-114">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="19aa9-115">Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-xamarin-ios-get-started).</span><span class="sxs-lookup"><span data-stu-id="19aa9-115">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-xamarin-ios-get-started).</span></span>
> 
> 

## <span data-ttu-id="19aa9-116"><a id="setup-azme"></a>Konfigurowanie usługi Mobile Engagement dla aplikacji systemu iOS</span><span class="sxs-lookup"><span data-stu-id="19aa9-116"><a id="setup-azme"></a>Setup Mobile Engagement for your iOS app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="19aa9-117"><a id="connecting-app"></a>Połączenie z zapleczem usługi Mobile Engagement toohello aplikacji</span><span class="sxs-lookup"><span data-stu-id="19aa9-117"><a id="connecting-app"></a>Connect your app toohello Mobile Engagement backend</span></span>
<span data-ttu-id="19aa9-118">Ten samouczek przedstawia "podstawową integrację", który czy hello minimalny wymagany toocollect danych i wysyłania powiadomień wypychanych.</span><span class="sxs-lookup"><span data-stu-id="19aa9-118">This tutorial presents a "basic integration" which is hello minimal set required toocollect data and send a push notification.</span></span>

<span data-ttu-id="19aa9-119">Utworzymy podstawową aplikację z integracją hello toodemonstrate Xamarin:</span><span class="sxs-lookup"><span data-stu-id="19aa9-119">We will create a basic app with Xamarin toodemonstrate hello integration:</span></span>

### <a name="create-a-new-xamarinios-project"></a><span data-ttu-id="19aa9-120">Tworzenie nowego projektu platformy Xamarin.iOS</span><span class="sxs-lookup"><span data-stu-id="19aa9-120">Create a new Xamarin.iOS project</span></span>
1. <span data-ttu-id="19aa9-121">Uruchom program Xamarin Studio.</span><span class="sxs-lookup"><span data-stu-id="19aa9-121">Launch Xamarin Studio.</span></span> <span data-ttu-id="19aa9-122">Przejdź za**pliku** -> **nowy** -> **rozwiązania**</span><span class="sxs-lookup"><span data-stu-id="19aa9-122">Go too**File** -> **New** -> **Solution**</span></span> 
   
    ![][1]
2. <span data-ttu-id="19aa9-123">Wybierz **jednej aplikacji widoku**, upewnij się, że hello wybrany język to **C#** , a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="19aa9-123">Select **Single View App**, make sure hello selected language is **C#** and then click **Next**.</span></span>
   
    ![][2]
3. <span data-ttu-id="19aa9-124">Wypełnij hello **Nazwa aplikacji** i hello **identyfikator organizacji** , a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="19aa9-124">Fill in hello **App Name** and hello **Organization Identifier** and then click **Next**.</span></span> 
   
    ![][3]
   
   > [!IMPORTANT]
   > <span data-ttu-id="19aa9-125">Upewnij się, tym hello, możesz użyć aplikacji systemu iOS używa identyfikator aplikacji, która jest zgodna z hello identyfikator pakietu w tym miejscu masz toodeploy profilu publikowania.</span><span class="sxs-lookup"><span data-stu-id="19aa9-125">Make sure that hello publishing profile you eventually use toodeploy your iOS app is using an App ID which matches exactly with hello Bundle Identifier you have here.</span></span> 
   > 
   > 
4. <span data-ttu-id="19aa9-126">Aktualizacja hello **Nazwa projektu**, **Nazwa rozwiązania** i **lokalizacji** wymagane, a następnie kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="19aa9-126">Update hello **Project Name**, **Solution Name** and **Location** if required and click **Create**.</span></span>
   
    ![][4]

<span data-ttu-id="19aa9-127">Program Xamarin Studio zostanie utworzona aplikacja demonstracyjna hello, w której zostanie zintegrowana usługa Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="19aa9-127">Xamarin Studio will create hello demo app in which we will integrate Mobile Engagement.</span></span> 

### <a name="connect-your-app-toomobile-engagement-backend"></a><span data-ttu-id="19aa9-128">Połącz zapleczu swojej aplikacji tooMobile zaangażowania</span><span class="sxs-lookup"><span data-stu-id="19aa9-128">Connect your app tooMobile Engagement backend</span></span>
1. <span data-ttu-id="19aa9-129">Kliknij prawym przyciskiem myszy hello **pakiety** folder w systemie windows rozwiązania hello i wybierz **Dodawanie pakietów...**</span><span class="sxs-lookup"><span data-stu-id="19aa9-129">Right click hello **Packages** folder in hello Solution windows and select **Add Packages...**</span></span>
   
    ![][5]
2. <span data-ttu-id="19aa9-130">Wyszukaj hello **Microsoft Azure Mobile Engagement Xamarin SDK** i dodaj go tooyour rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="19aa9-130">Search for hello **Microsoft Azure Mobile Engagement Xamarin SDK** and add it tooyour solution.</span></span>  
   
    ![][6]
3. <span data-ttu-id="19aa9-131">Otwórz **AppDelegate.cs** i dodaj następujące hello instrukcję using:</span><span class="sxs-lookup"><span data-stu-id="19aa9-131">Open **AppDelegate.cs** and add hello following using statement:</span></span>
   
        using Microsoft.Azure.Engagement.Xamarin;
4. <span data-ttu-id="19aa9-132">W hello **FinishedLaunching** metody, Dodaj powitania po tooinitialize hello połączenia z zapleczem usługi Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="19aa9-132">In hello **FinishedLaunching** method, add hello following tooinitialize hello connection with Mobile Engagement backend.</span></span> <span data-ttu-id="19aa9-133">Upewnij się, że tooadd Twojego **ConnectionString**.</span><span class="sxs-lookup"><span data-stu-id="19aa9-133">Make sure tooadd your **ConnectionString**.</span></span> <span data-ttu-id="19aa9-134">Ten kod zawiera również **NotificationIcon** dodawany przez hello zestaw Mobile Engagement SDK, który może być tooreplace.</span><span class="sxs-lookup"><span data-stu-id="19aa9-134">This code also uses a dummy **NotificationIcon** which is added by hello Mobile Engagement SDK which you may want tooreplace.</span></span> 
   
        EngagementConfiguration config = new EngagementConfiguration {
                        ConnectionString = "YourConnectionStringFromAzurePortal",
                        NotificationIcon = UIImage.FromBundle("close")
                    };
        EngagementAgent.Init (config);

## <span data-ttu-id="19aa9-135"><a id="monitor"></a>Włączanie monitorowania w czasie rzeczywistym</span><span class="sxs-lookup"><span data-stu-id="19aa9-135"><a id="monitor"></a>Enabling real-time monitoring</span></span>
<span data-ttu-id="19aa9-136">W kolejności toostart wysyłanie danych i zapewnienie, że hello użytkownicy są aktywni konieczne jest wysłanie co najmniej jeden zapleczem usługi Mobile Engagement toohello ekranu.</span><span class="sxs-lookup"><span data-stu-id="19aa9-136">In order toostart sending data and ensuring hello users are active, you must send at least one screen toohello Mobile Engagement backend.</span></span>

1. <span data-ttu-id="19aa9-137">Otwórz **ViewController.cs** i dodaj następujące hello instrukcję using:</span><span class="sxs-lookup"><span data-stu-id="19aa9-137">Open **ViewController.cs** and add hello following using statement:</span></span>
   
        using Microsoft.Azure.Engagement.Xamarin;
2. <span data-ttu-id="19aa9-138">Zastąp klasę hello, z której `ViewController` dziedziczy `UIViewController` zbyt`EngagementViewController`.</span><span class="sxs-lookup"><span data-stu-id="19aa9-138">Replace hello class from which `ViewController` inherits from `UIViewController` too`EngagementViewController`.</span></span> 

## <span data-ttu-id="19aa9-139"><a id="monitor"></a>Łączenie aplikacji z funkcją monitorowania w czasie rzeczywistym</span><span class="sxs-lookup"><span data-stu-id="19aa9-139"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="19aa9-140"><a id="integrate-push"></a>Włączanie powiadomień wypychanych i funkcji komunikatów w aplikacji</span><span class="sxs-lookup"><span data-stu-id="19aa9-140"><a id="integrate-push"></a>Enable push notifications and in-app messaging</span></span>
<span data-ttu-id="19aa9-141">Usługa Mobile Engagement umożliwia toointeract z użytkownikami i ZASIĘGU z powiadomień wypychanych i komunikatów w kontekście kampanii hello w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="19aa9-141">Mobile Engagement allows you toointeract with your users and REACH with push notifications and in-app messaging in hello context of campaigns.</span></span> <span data-ttu-id="19aa9-142">Ten moduł ma nazwę REACH w portalu Mobile Engagement hello.</span><span class="sxs-lookup"><span data-stu-id="19aa9-142">This module is called REACH in hello Mobile Engagement portal.</span></span>
<span data-ttu-id="19aa9-143">Witaj sekcje skonfigurować tooreceive Twojej aplikacji je.</span><span class="sxs-lookup"><span data-stu-id="19aa9-143">hello following sections set up your app tooreceive them.</span></span>

### <a name="modify-your-application-delegate"></a><span data-ttu-id="19aa9-144">Modyfikowanie delegata aplikacji</span><span class="sxs-lookup"><span data-stu-id="19aa9-144">Modify your Application Delegate</span></span>
1. <span data-ttu-id="19aa9-145">Otwórz hello **AppDelegate.cs** i dodaj następujące hello instrukcję using:</span><span class="sxs-lookup"><span data-stu-id="19aa9-145">Open hello **AppDelegate.cs** and add hello following using statement:</span></span>
   
        using System; 
2. <span data-ttu-id="19aa9-146">Teraz wewnątrz hello `FinishedLaunching` metody, Dodaj następujące tooregister wiadomości wypychanych hello`EngagementAgent.init(...)`</span><span class="sxs-lookup"><span data-stu-id="19aa9-146">Now inside hello `FinishedLaunching` method, add hello following tooregister for push messages after `EngagementAgent.init(...)`</span></span>
   
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
3. <span data-ttu-id="19aa9-147">Na koniec — aktualizacja lub Dodaj hello następujące metody:</span><span class="sxs-lookup"><span data-stu-id="19aa9-147">Finally - update or add hello following methods:</span></span>
   
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
            Console.WriteLine("Failed tooregister for remote notifications: Error '{0}'", error);
        }
4. <span data-ttu-id="19aa9-148">W Twojej **Info.plist** pliku w rozwiązaniu hello, upewnij się, że hello **identyfikator pakietu** jest zgodny z hello **identyfikator aplikacji** ma w Twoim profilu inicjowania obsługi administracyjnej w hello deweloperów firmy Apple Centrum.</span><span class="sxs-lookup"><span data-stu-id="19aa9-148">In your **Info.plist** file in hello solution, confirm that hello **Bundle Identifier** matches with hello **App ID** you have in your provisioning profile in hello Apple Dev Center.</span></span> 
   
    ![][7]
5. <span data-ttu-id="19aa9-149">W hello sam **Info.plist** plików, upewnij się, że zaznaczono hello **Włącz tryby tła** i **zdalnego powiadomienia**.</span><span class="sxs-lookup"><span data-stu-id="19aa9-149">In hello same **Info.plist** file, make sure that you have checked hello **Enable Background Modes** and **Remote Notifications**.</span></span> 
   
     ![][8]
6. <span data-ttu-id="19aa9-150">Uruchamianie aplikacji hello na urządzeniu hello, który został skojarzony z tym profilem publikowania.</span><span class="sxs-lookup"><span data-stu-id="19aa9-150">Run hello app on hello device you have associated with this publishing profile.</span></span> 

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
