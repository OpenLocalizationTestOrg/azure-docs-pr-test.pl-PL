---
title: "aaaGet Started with Azure Mobile Engagement dla systemu iOS w języku Objective C | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse usługi Azure Mobile Engagement z analizy i powiadomieniami wypychanymi dla aplikacji systemu iOS."
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 117b5742-522b-41de-98c5-f432da2d98f8
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: hero-article
ms.date: 07/17/2017
ms.author: piyushjo
ms.openlocfilehash: 51a5013f23d2d04a7b9b30c83b47017898b2bb00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-ios-apps-in-objective-c"></a><span data-ttu-id="1d6b0-103">Wprowadzenie do usługi Azure Mobile Engagement dla aplikacji systemu iOS w języku Objective C</span><span class="sxs-lookup"><span data-stu-id="1d6b0-103">Get Started with Azure Mobile Engagement for iOS apps in Objective C</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="1d6b0-104">W tym temacie opisano sposób toounderstand usługi Azure Mobile Engagement toouse użycia aplikacji, a wysłać aplikacji dla systemu iOS tooan użytkowników toosegmented powiadomienia push.</span><span class="sxs-lookup"><span data-stu-id="1d6b0-104">This topic shows you how toouse Azure Mobile Engagement toounderstand your app usage and send push notifications toosegmented users tooan iOS application.</span></span>
<span data-ttu-id="1d6b0-105">W tym samouczku zostanie utworzona pusta aplikacja systemu iOS służąca do zbierania podstawowych danych i odbierania powiadomień wypychanych przy użyciu systemu Apple Push Notification System (APNS).</span><span class="sxs-lookup"><span data-stu-id="1d6b0-105">In this tutorial, you create a blank iOS app that collects basic data and receives push notifications using Apple Push Notification System (APNS).</span></span>

<span data-ttu-id="1d6b0-106">Ten samouczek wymaga następujących hello:</span><span class="sxs-lookup"><span data-stu-id="1d6b0-106">This tutorial requires hello following:</span></span>

* <span data-ttu-id="1d6b0-107">Edytor XCode 8, który można zainstalować ze sklepu Mac App Store</span><span class="sxs-lookup"><span data-stu-id="1d6b0-107">XCode 8, which you can install from your MAC App Store</span></span>
* <span data-ttu-id="1d6b0-108">Witaj [Mobile Engagement iOS SDK]</span><span class="sxs-lookup"><span data-stu-id="1d6b0-108">hello [Mobile Engagement iOS SDK]</span></span>

<span data-ttu-id="1d6b0-109">Wykonanie czynności opisanych w tym samouczku jest wymaganiem wstępnym dla wszystkich innych samouczków usługi Mobile Engagement dla aplikacji systemu iOS.</span><span class="sxs-lookup"><span data-stu-id="1d6b0-109">Completing this tutorial is a prerequisite for all other Mobile Engagement tutorials for iOS apps.</span></span>

> [!NOTE]
> <span data-ttu-id="1d6b0-110">toocomplete tego samouczka, musi mieć aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="1d6b0-110">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="1d6b0-111">Jeśli go nie masz, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut.</span><span class="sxs-lookup"><span data-stu-id="1d6b0-111">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="1d6b0-112">Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-ios-get-started).</span><span class="sxs-lookup"><span data-stu-id="1d6b0-112">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-ios-get-started).</span></span>
>
>

## <span data-ttu-id="1d6b0-113"><a id="setup-azme"></a>Konfigurowanie usługi Mobile Engagement dla aplikacji systemu iOS</span><span class="sxs-lookup"><span data-stu-id="1d6b0-113"><a id="setup-azme"></a>Setup Mobile Engagement for your iOS app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="1d6b0-114"><a id="connecting-app"></a>Połączenie z zapleczem usługi Mobile Engagement toohello aplikacji</span><span class="sxs-lookup"><span data-stu-id="1d6b0-114"><a id="connecting-app"></a>Connect your app toohello Mobile Engagement backend</span></span>
<span data-ttu-id="1d6b0-115">Ten samouczek przedstawia "podstawową integrację", który czy hello minimalny wymagany toocollect danych i wysyłania powiadomień wypychanych.</span><span class="sxs-lookup"><span data-stu-id="1d6b0-115">This tutorial presents a "basic integration", which is hello minimal set required toocollect data and send a push notification.</span></span> <span data-ttu-id="1d6b0-116">Witaj kompletna dokumentacja integracji znajduje się w hello [Mobile Engagement iOS SDK integration](mobile-engagement-ios-sdk-overview.md)</span><span class="sxs-lookup"><span data-stu-id="1d6b0-116">hello complete integration documentation can be found in hello [Mobile Engagement iOS SDK integration](mobile-engagement-ios-sdk-overview.md)</span></span>

<span data-ttu-id="1d6b0-117">Utworzymy podstawową aplikację w środowisku XCode toodemonstrate hello integracji.</span><span class="sxs-lookup"><span data-stu-id="1d6b0-117">We will create a basic app with XCode toodemonstrate hello integration.</span></span>

### <a name="create-a-new-ios-project"></a><span data-ttu-id="1d6b0-118">Tworzenie nowego projektu systemu iOS</span><span class="sxs-lookup"><span data-stu-id="1d6b0-118">Create a new iOS project</span></span>
[!INCLUDE [Create a new iOS Project](../../includes/mobile-engagement-create-new-ios-app.md)]

### <a name="connect-your-app-toohello-mobile-engagement-backend"></a><span data-ttu-id="1d6b0-119">Połączenie z zapleczem usługi Mobile Engagement toohello aplikacji</span><span class="sxs-lookup"><span data-stu-id="1d6b0-119">Connect your app toohello Mobile Engagement backend</span></span>
1. <span data-ttu-id="1d6b0-120">Pobierz hello [Mobile Engagement iOS SDK].</span><span class="sxs-lookup"><span data-stu-id="1d6b0-120">Download hello [Mobile Engagement iOS SDK].</span></span>
2. <span data-ttu-id="1d6b0-121">Wyodrębnij hello. tar.gz pliku tooa folderu na swoim komputerze.</span><span class="sxs-lookup"><span data-stu-id="1d6b0-121">Extract hello .tar.gz file tooa folder in your computer.</span></span>
3. <span data-ttu-id="1d6b0-122">Kliknij prawym przyciskiem myszy projekt hello, a następnie wybierz **Dodaj pliki do**.</span><span class="sxs-lookup"><span data-stu-id="1d6b0-122">Right-click hello project, and then select **Add files to**.</span></span>

    ![][1]
4. <span data-ttu-id="1d6b0-123">Przejdź do folderu toohello, w którym wyodrębniono hello zestawu SDK, wybierz hello `EngagementSDK` folderu, kliknij przycisk **opcje** hello lewym dolnym rogu i upewnij się, że pole wyboru hello **skopiować elementy w razie potrzeby** i hello pole wyboru docelowego są sprawdzane, a następnie naciśnij klawisz **OK**.</span><span class="sxs-lookup"><span data-stu-id="1d6b0-123">Navigate toohello folder where you extracted hello SDK, select hello `EngagementSDK` folder, click **Options** on hello bottom left corner and make sure that hello checkbox **Copy items if needed** and hello checkbox for your target are checked then press **OK**.</span></span>

    ![][2]
5. <span data-ttu-id="1d6b0-124">Otwórz hello **fazy kompilacji** karcie w hello **binarny z bibliotekami** menu Dodaj hello struktury, jak pokazano poniżej:</span><span class="sxs-lookup"><span data-stu-id="1d6b0-124">Open hello **Build Phases** tab, and in hello **Link Binary With Libraries** menu, add hello frameworks as shown below:</span></span>

    ![][3]
6. <span data-ttu-id="1d6b0-125">Przejdź wstecz toohello portalu Azure w Twojej aplikacji **informacje o połączeniu** strony i skopiuj parametry połączenia hello.</span><span class="sxs-lookup"><span data-stu-id="1d6b0-125">Go back toohello Azure portal in your app's **Connection Info** page and copy hello connection string.</span></span>

    ![][4]
7. <span data-ttu-id="1d6b0-126">Dodaj powitania po wierszu kodu w Twojej **AppDelegate.m** pliku.</span><span class="sxs-lookup"><span data-stu-id="1d6b0-126">Add hello following line of code in your **AppDelegate.m** file.</span></span>

        #import "EngagementAgent.h"
8. <span data-ttu-id="1d6b0-127">Teraz Wklej parametry połączenia hello hello `didFinishLaunchingWithOptions` delegowanie.</span><span class="sxs-lookup"><span data-stu-id="1d6b0-127">Now paste hello connection string in hello `didFinishLaunchingWithOptions` delegate.</span></span>

        - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
        {
              [...]   
              [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}"];
              [...]
        }
9. <span data-ttu-id="1d6b0-128">`setTestLogEnabled`jest instrukcją opcjonalną, która umożliwia dzienników zestawu SDK dla Ciebie tooidentify problemów.</span><span class="sxs-lookup"><span data-stu-id="1d6b0-128">`setTestLogEnabled` is an optional statement which enables SDK logs for you tooidentify issues.</span></span>

## <span data-ttu-id="1d6b0-129"><a id="monitor"></a>Włączanie monitorowania w czasie rzeczywistym</span><span class="sxs-lookup"><span data-stu-id="1d6b0-129"><a id="monitor"></a>Enable real-time monitoring</span></span>
<span data-ttu-id="1d6b0-130">W kolejności toostart wysyłanie danych i zapewnienie, że hello użytkownicy są aktywni konieczne jest wysłanie co najmniej jeden zapleczem usługi Mobile Engagement toohello ekranu (działanie).</span><span class="sxs-lookup"><span data-stu-id="1d6b0-130">In order toostart sending data and ensuring that hello users are active, you must send at least one screen (Activity) toohello Mobile Engagement backend.</span></span>

1. <span data-ttu-id="1d6b0-131">Otwórz hello **ViewController.h** pliku i zaimportować **EngagementViewController.h**:</span><span class="sxs-lookup"><span data-stu-id="1d6b0-131">Open hello **ViewController.h** file and import **EngagementViewController.h**:</span></span>

    `#import "EngagementViewController.h"`
2. <span data-ttu-id="1d6b0-132">Teraz Zastąp hello superklasę hello **ViewController** interfejsu `EngagementViewController`:</span><span class="sxs-lookup"><span data-stu-id="1d6b0-132">Now replace hello super class of hello **ViewController** interface by `EngagementViewController`:</span></span>

    `@interface ViewController : EngagementViewController`

## <span data-ttu-id="1d6b0-133"><a id="monitor"></a>Łączenie aplikacji z funkcją monitorowania w czasie rzeczywistym</span><span class="sxs-lookup"><span data-stu-id="1d6b0-133"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="1d6b0-134"><a id="integrate-push"></a>Włączanie powiadomień wypychanych i funkcji komunikatów w aplikacji</span><span class="sxs-lookup"><span data-stu-id="1d6b0-134"><a id="integrate-push"></a>Enable push notifications and in-app messaging</span></span>
<span data-ttu-id="1d6b0-135">Usługa Mobile Engagement umożliwia toointeract z użytkownikami i ZASIĘGU z powiadomień wypychanych i komunikatów w kontekście kampanii hello w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1d6b0-135">Mobile Engagement allows you toointeract with your users and REACH with push notifications and in-app messaging in hello context of campaigns.</span></span> <span data-ttu-id="1d6b0-136">Ten moduł ma nazwę REACH w portalu Mobile Engagement hello.</span><span class="sxs-lookup"><span data-stu-id="1d6b0-136">This module is called REACH in hello Mobile Engagement portal.</span></span>
<span data-ttu-id="1d6b0-137">Witaj sekcje skonfigurować tooreceive Twojej aplikacji je.</span><span class="sxs-lookup"><span data-stu-id="1d6b0-137">hello following sections set up your app tooreceive them.</span></span>

### <a name="enable-your-app-tooreceive-silent-push-notifications"></a><span data-ttu-id="1d6b0-138">Włącz tooreceive Twojej aplikacji cichych powiadomień wypychanych</span><span class="sxs-lookup"><span data-stu-id="1d6b0-138">Enable your app tooreceive Silent Push Notifications</span></span>
[!INCLUDE [mobile-engagement-ios-silent-push](../../includes/mobile-engagement-ios-silent-push.md)]

### <a name="add-hello-reach-library-tooyour-project"></a><span data-ttu-id="1d6b0-139">Dodaj projekt tooyour biblioteki Reach hello</span><span class="sxs-lookup"><span data-stu-id="1d6b0-139">Add hello Reach library tooyour project</span></span>
1. <span data-ttu-id="1d6b0-140">Kliknij prawym przyciskiem myszy projekt.</span><span class="sxs-lookup"><span data-stu-id="1d6b0-140">Right-click your project.</span></span>
2. <span data-ttu-id="1d6b0-141">Wybierz pozycję **Add file to** (Dodaj plik do).</span><span class="sxs-lookup"><span data-stu-id="1d6b0-141">Select **Add file to**.</span></span>
3. <span data-ttu-id="1d6b0-142">Przejdź toohello folder, w którym wyodrębniono hello zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="1d6b0-142">Navigate toohello folder where you extracted hello SDK.</span></span>
4. <span data-ttu-id="1d6b0-143">Wybierz hello `EngagementReach` folderu.</span><span class="sxs-lookup"><span data-stu-id="1d6b0-143">Select hello `EngagementReach` folder.</span></span>
5. <span data-ttu-id="1d6b0-144">Kliknij pozycję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="1d6b0-144">Click **Add**.</span></span>

### <a name="modify-your-application-delegate"></a><span data-ttu-id="1d6b0-145">Modyfikowanie delegata aplikacji</span><span class="sxs-lookup"><span data-stu-id="1d6b0-145">Modify your Application Delegate</span></span>
1. <span data-ttu-id="1d6b0-146">W **Appdelegate.m** plików, zaimportuj moduł Reach usługi Engagement hello.</span><span class="sxs-lookup"><span data-stu-id="1d6b0-146">Back in **AppDeletegate.m** file, import hello Engagement Reach module.</span></span>

        #import "AEReachModule.h"
        #import <UserNotifications/UserNotifications.h>
2. <span data-ttu-id="1d6b0-147">Witaj wewnątrz `application:didFinishLaunchingWithOptions` metody, Utwórz moduł Reach i przekaż go tooyour istniejącego wiersza inicjowania usługi Engagement:</span><span class="sxs-lookup"><span data-stu-id="1d6b0-147">Inside hello `application:didFinishLaunchingWithOptions` method, create a Reach module and pass it tooyour existing Engagement initialization line:</span></span>

        - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
            AEReachModule * reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
            [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}" modules:reach, nil];
            [...]
            return YES;
        }

### <a name="enable-your-app-tooreceive-apns-push-notifications"></a><span data-ttu-id="1d6b0-148">Włącz tooreceive Twojej aplikacji powiadomień wypychanych usługi APNS</span><span class="sxs-lookup"><span data-stu-id="1d6b0-148">Enable your app tooreceive APNS Push Notifications</span></span>
1. <span data-ttu-id="1d6b0-149">Dodaj powitania po wierszu toohello `application:didFinishLaunchingWithOptions` metody:</span><span class="sxs-lookup"><span data-stu-id="1d6b0-149">Add hello following line toohello `application:didFinishLaunchingWithOptions` method:</span></span>

        if (NSFoundationVersionNumber >= NSFoundationVersionNumber_iOS_8_0)
        {
            if (NSFoundationVersionNumber > NSFoundationVersionNumber_iOS_9_x_Max)
            {
                [UNUserNotificationCenter.currentNotificationCenter requestAuthorizationWithOptions:(UNAuthorizationOptionBadge | UNAuthorizationOptionSound | UNAuthorizationOptionAlert) completionHandler:^(BOOL granted, NSError * _Nullable error) {}];
            }else
            {
                [application registerUserNotificationSettings:[UIUserNotificationSettings settingsForTypes:(UIUserNotificationTypeBadge | UIUserNotificationTypeSound | UIUserNotificationTypeAlert)   categories:nil]];
            }
            [application registerForRemoteNotifications];
        }
        else
        {
            [application registerForRemoteNotificationTypes:(UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound | UIRemoteNotificationTypeAlert)];
        }
2. <span data-ttu-id="1d6b0-150">Dodaj hello `application:didRegisterForRemoteNotificationsWithDeviceToken` metody w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="1d6b0-150">Add hello `application:didRegisterForRemoteNotificationsWithDeviceToken` method as follows:</span></span>

        - (void)application:(UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken
        {
             [[EngagementAgent shared] registerDeviceToken:deviceToken];
            NSLog(@"Registered Token: %@", deviceToken);
        }
3. <span data-ttu-id="1d6b0-151">Dodaj hello `didFailToRegisterForRemoteNotificationsWithError` metody w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="1d6b0-151">Add hello `didFailToRegisterForRemoteNotificationsWithError` method as follows:</span></span>

        - (void)application:(UIApplication*)application didFailToRegisterForRemoteNotificationsWithError:(NSError*)error
        {
           NSLog(@"Failed tooget token, error: %@", error);
        }
4. <span data-ttu-id="1d6b0-152">Dodaj hello `didReceiveRemoteNotification:fetchCompletionHandler` metody w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="1d6b0-152">Add hello `didReceiveRemoteNotification:fetchCompletionHandler` method as follows:</span></span>

        - (void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult result))handler
        {
            [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:handler];
        }

[!INCLUDE [mobile-engagement-ios-send-push-push](../../includes/mobile-engagement-ios-send-push.md)]

<!-- URLs. -->
[Mobile Engagement iOS SDK]: http://aka.ms/qk2rnj

<!-- Images. -->
[1]: ./media/mobile-engagement-ios-get-started/xcode-add-files.png
[2]: ./media/mobile-engagement-ios-get-started/xcode-select-engagement-sdk.png
[3]: ./media/mobile-engagement-ios-get-started/xcode-build-phases.png
[4]: ./media/mobile-engagement-ios-get-started/app-connection-info-page.png
