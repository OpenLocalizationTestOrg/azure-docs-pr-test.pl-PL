---
title: "aaaGet Started with Azure Mobile Engagement dla systemu iOS w języku Swift | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse usługi Azure Mobile Engagement z funkcją analizy i powiadomieniami Wypychanymi dla aplikacji systemu iOS."
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 196c282d-6f2f-4cbc-aeee-6517c5ad866d
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: swift
ms.topic: hero-article
ms.date: 09/20/2016
ms.author: piyushjo
ms.openlocfilehash: 9a3841d305745f8b80c6b0c86aabe18e0c7c0e59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-ios-apps-in-swift"></a><span data-ttu-id="114fe-103">Wprowadzenie do usługi Azure Mobile Engagement dla aplikacji systemu iOS w języku Swift</span><span class="sxs-lookup"><span data-stu-id="114fe-103">Get Started with Azure Mobile Engagement for iOS Apps in Swift</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="114fe-104">W tym temacie opisano sposób toounderstand usługi Azure Mobile Engagement toouse użycia aplikacji, a wysłać aplikacji dla systemu iOS tooan użytkowników toosegmented powiadomienia push.</span><span class="sxs-lookup"><span data-stu-id="114fe-104">This topic shows you how toouse Azure Mobile Engagement toounderstand your app usage and send push notifications toosegmented users tooan iOS application.</span></span>
<span data-ttu-id="114fe-105">W tym samouczku zostanie utworzona pusta aplikacja systemu iOS służąca do zbierania podstawowych danych i odbierania powiadomień wypychanych przy użyciu systemu Apple Push Notification System (APNS).</span><span class="sxs-lookup"><span data-stu-id="114fe-105">In this tutorial, you create a blank iOS app that collects basic data and receives push notifications using Apple Push Notification System (APNS).</span></span>

<span data-ttu-id="114fe-106">Ten samouczek wymaga następujących hello:</span><span class="sxs-lookup"><span data-stu-id="114fe-106">This tutorial requires hello following:</span></span>

* <span data-ttu-id="114fe-107">Edytor XCode 8, który można zainstalować ze sklepu Mac App Store</span><span class="sxs-lookup"><span data-stu-id="114fe-107">XCode 8, which you can install from your MAC App Store</span></span>
* <span data-ttu-id="114fe-108">Witaj [Mobile Engagement iOS SDK]</span><span class="sxs-lookup"><span data-stu-id="114fe-108">hello [Mobile Engagement iOS SDK]</span></span>
* <span data-ttu-id="114fe-109">Certyfikat powiadomień wypychanych (p12), który można uzyskać z Centrum deweloperów firmy Apple</span><span class="sxs-lookup"><span data-stu-id="114fe-109">Push notification certificate (.p12) that you can obtain on your Apple Dev Center</span></span>

> [!NOTE]
> <span data-ttu-id="114fe-110">W tym samouczku jest używany język Swift w wersji 3.0.</span><span class="sxs-lookup"><span data-stu-id="114fe-110">This tutorial uses Swift version 3.0.</span></span> 
> 
> 

<span data-ttu-id="114fe-111">Wykonanie czynności opisanych w tym samouczku jest wymaganiem wstępnym dla wszystkich innych samouczków usługi Mobile Engagement dla aplikacji systemu iOS.</span><span class="sxs-lookup"><span data-stu-id="114fe-111">Completing this tutorial is a prerequisite for all other Mobile Engagement tutorials for iOS apps.</span></span>

> [!NOTE]
> <span data-ttu-id="114fe-112">toocomplete tego samouczka, musi mieć aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="114fe-112">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="114fe-113">Jeśli go nie masz, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut.</span><span class="sxs-lookup"><span data-stu-id="114fe-113">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="114fe-114">Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-ios-swift-get-started).</span><span class="sxs-lookup"><span data-stu-id="114fe-114">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-ios-swift-get-started).</span></span>
> 
> 

## <span data-ttu-id="114fe-115"><a id="setup-azme"></a>Konfigurowanie usługi Mobile Engagement dla aplikacji systemu iOS</span><span class="sxs-lookup"><span data-stu-id="114fe-115"><a id="setup-azme"></a>Setup Mobile Engagement for your iOS app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="114fe-116"><a id="connecting-app"></a>Połączenie z zapleczem usługi Mobile Engagement toohello aplikacji</span><span class="sxs-lookup"><span data-stu-id="114fe-116"><a id="connecting-app"></a>Connect your app toohello Mobile Engagement backend</span></span>
<span data-ttu-id="114fe-117">Ten samouczek przedstawia "podstawową integrację", który czy hello minimalny wymagany toocollect danych i wysyłania powiadomień wypychanych.</span><span class="sxs-lookup"><span data-stu-id="114fe-117">This tutorial presents a "basic integration", which is hello minimal set required toocollect data and send a push notification.</span></span> <span data-ttu-id="114fe-118">Witaj kompletna dokumentacja integracji znajduje się w hello [Mobile Engagement iOS SDK integration](mobile-engagement-ios-sdk-overview.md)</span><span class="sxs-lookup"><span data-stu-id="114fe-118">hello complete integration documentation can be found in hello [Mobile Engagement iOS SDK integration](mobile-engagement-ios-sdk-overview.md)</span></span>

<span data-ttu-id="114fe-119">Utworzymy podstawową aplikację w środowisku XCode toodemonstrate hello integracji:</span><span class="sxs-lookup"><span data-stu-id="114fe-119">We will create a basic app with XCode toodemonstrate hello integration:</span></span>

### <a name="create-a-new-ios-project"></a><span data-ttu-id="114fe-120">Tworzenie nowego projektu systemu iOS</span><span class="sxs-lookup"><span data-stu-id="114fe-120">Create a new iOS project</span></span>
[!INCLUDE [Create a new iOS Project](../../includes/mobile-engagement-create-new-ios-app.md)]

### <a name="connect-your-app-toomobile-engagement-backend"></a><span data-ttu-id="114fe-121">Połącz zapleczu swojej aplikacji tooMobile zaangażowania</span><span class="sxs-lookup"><span data-stu-id="114fe-121">Connect your app tooMobile Engagement backend</span></span>
1. <span data-ttu-id="114fe-122">Pobierz hello [Mobile Engagement iOS SDK]</span><span class="sxs-lookup"><span data-stu-id="114fe-122">Download hello [Mobile Engagement iOS SDK]</span></span>
2. <span data-ttu-id="114fe-123">Wyodrębnij hello. tar.gz pliku tooa folderu na swoim komputerze</span><span class="sxs-lookup"><span data-stu-id="114fe-123">Extract hello .tar.gz file tooa folder in your computer</span></span>
3. <span data-ttu-id="114fe-124">Projektu powitania kliknij prawym przyciskiem myszy i wybierz opcję "Dodaj pliki zbyt..."</span><span class="sxs-lookup"><span data-stu-id="114fe-124">Right click hello project and select "Add files too..."</span></span>
   
    ![][1]
4. <span data-ttu-id="114fe-125">Przejdź do folderu toohello, którym została rozpakowana hello zestawu SDK i wybierz hello `EngagementSDK` folder, a następnie naciśnij przycisk OK.</span><span class="sxs-lookup"><span data-stu-id="114fe-125">Navigate toohello folder where you extracted hello SDK and select hello `EngagementSDK` folder then press OK.</span></span>
   
    ![][2]
5. <span data-ttu-id="114fe-126">Otwórz hello `Build Phases` kartę w hello `Link Binary With Libraries` menu Dodaj hello struktury, jak pokazano poniżej:</span><span class="sxs-lookup"><span data-stu-id="114fe-126">Open hello `Build Phases` tab and in hello `Link Binary With Libraries` menu add hello frameworks as shown below:</span></span>
   
    ![][3]
6. <span data-ttu-id="114fe-127">Utworzyć mostkowanie nagłówka toobe toouse stanie hello w celu C interfejsów API zestawu SDK, wybierając plik > Nowy > Plik > iOS > źródło > pliku nagłówka.</span><span class="sxs-lookup"><span data-stu-id="114fe-127">Create a Bridging header toobe able toouse hello SDK's Objective C APIs by choosing File > New > File > iOS > Source > Header File.</span></span>
   
    ![][4]
7. <span data-ttu-id="114fe-128">Edytuj hello mostkowanie nagłówka pliku tooexpose Mobile Engagement Objective-C kod tooyour kod Swift, Dodaj hello importuje następujące:</span><span class="sxs-lookup"><span data-stu-id="114fe-128">Edit hello bridging header file tooexpose Mobile Engagement Objective-C code tooyour Swift code, add hello following imports :</span></span>
   
        /* Mobile Engagement Agent */
        #import "AEModule.h"
        #import "AEPushMessage.h"
        #import "AEStorage.h"
        #import "EngagementAgent.h"
        #import "EngagementTableViewController.h"
        #import "EngagementViewController.h"
        #import "AEUserNotificationHandler.h"
        #import "AEIdfaProvider.h"
8. <span data-ttu-id="114fe-129">W ustawieniach kompilacji upewnij się, że ustawienie w obszarze Swift kompilatora - generowania kodu kompilacji nagłówków mostkowania języka Objective-C hello ma nagłówek toothis ścieżki.</span><span class="sxs-lookup"><span data-stu-id="114fe-129">Under Build Settings, make sure hello Objective-C Bridging Header build setting under Swift Compiler - Code Generation has a path toothis header.</span></span> <span data-ttu-id="114fe-130">Oto przykład ścieżki: **$(SRCROOT)/MySuperApp/MySuperApp-Bridging-Header.h (w zależności od ścieżki hello)**</span><span class="sxs-lookup"><span data-stu-id="114fe-130">Here is a path example: **$(SRCROOT)/MySuperApp/MySuperApp-Bridging-Header.h (depending on hello path)**</span></span>
   
   ![][6]
9. <span data-ttu-id="114fe-131">Przejdź wstecz toohello portalu Azure w Twojej aplikacji *informacje o połączeniu* strony i skopiuj parametry połączenia hello</span><span class="sxs-lookup"><span data-stu-id="114fe-131">Go back toohello Azure portal in your app's *Connection Info* page and copy hello Connection String</span></span>
   
   ![][5]
10. <span data-ttu-id="114fe-132">Teraz Wklej parametry połączenia hello hello `didFinishLaunchingWithOptions` delegowanie</span><span class="sxs-lookup"><span data-stu-id="114fe-132">Now paste hello connection string in hello `didFinishLaunchingWithOptions` delegate</span></span>
    
        func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplicationLaunchOptionsKey: Any]?) -> Bool
        {
              [...]
                EngagementAgent.init("Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}")
              [...]
        }

## <span data-ttu-id="114fe-133"><a id="monitor"></a>Włączanie monitorowania w czasie rzeczywistym</span><span class="sxs-lookup"><span data-stu-id="114fe-133"><a id="monitor"></a>Enabling real-time monitoring</span></span>
<span data-ttu-id="114fe-134">W kolejności toostart wysyłanie danych i zapewnienie, że hello użytkownicy są aktywni konieczne jest wysłanie co najmniej jeden zapleczem usługi Mobile Engagement toohello ekranu (działanie).</span><span class="sxs-lookup"><span data-stu-id="114fe-134">In order toostart sending data and ensuring that hello users are active, you must send at least one screen (Activity) toohello Mobile Engagement backend.</span></span>

1. <span data-ttu-id="114fe-135">Otwórz hello **ViewController.swift** plików i Zastąp klasę podstawową hello **ViewController** toobe **EngagementViewController**:</span><span class="sxs-lookup"><span data-stu-id="114fe-135">Open hello **ViewController.swift** file and replace hello base class of **ViewController** toobe **EngagementViewController**:</span></span>
   
    `class ViewController : EngagementViewController {`

## <span data-ttu-id="114fe-136"><a id="monitor"></a>Łączenie aplikacji z funkcją monitorowania w czasie rzeczywistym</span><span class="sxs-lookup"><span data-stu-id="114fe-136"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="114fe-137"><a id="integrate-push"></a>Włączanie powiadomień wypychanych i funkcji komunikatów w aplikacji</span><span class="sxs-lookup"><span data-stu-id="114fe-137"><a id="integrate-push"></a>Enabling Push Notifications and in-app messaging</span></span>
<span data-ttu-id="114fe-138">Usługa Mobile Engagement umożliwia toointeract i ZASIĘGU z użytkownikami przy użyciu powiadomień wypychanych i komunikatów w aplikacji w kontekście hello kampanii.</span><span class="sxs-lookup"><span data-stu-id="114fe-138">Mobile Engagement allows you toointeract and REACH with your users with Push Notifications and In-app Messaging in hello context of campaigns.</span></span> <span data-ttu-id="114fe-139">Ten moduł ma nazwę REACH w portalu Mobile Engagement hello.</span><span class="sxs-lookup"><span data-stu-id="114fe-139">This module is called REACH in hello Mobile Engagement portal.</span></span>
<span data-ttu-id="114fe-140">Witaj poniższe sekcje umożliwią skonfigurowanie tooreceive Twojej aplikacji je.</span><span class="sxs-lookup"><span data-stu-id="114fe-140">hello following sections will setup your app tooreceive them.</span></span>

### <a name="enable-your-app-tooreceive-silent-push-notifications"></a><span data-ttu-id="114fe-141">Włącz tooreceive Twojej aplikacji cichych powiadomień wypychanych</span><span class="sxs-lookup"><span data-stu-id="114fe-141">Enable your app tooreceive Silent Push Notifications</span></span>
[!INCLUDE [mobile-engagement-ios-silent-push](../../includes/mobile-engagement-ios-silent-push.md)]

### <a name="add-hello-reach-library-tooyour-project"></a><span data-ttu-id="114fe-142">Dodaj projekt tooyour biblioteki Reach hello</span><span class="sxs-lookup"><span data-stu-id="114fe-142">Add hello Reach library tooyour project</span></span>
1. <span data-ttu-id="114fe-143">Kliknij prawym przyciskiem projekt.</span><span class="sxs-lookup"><span data-stu-id="114fe-143">Right click your project</span></span>
2. <span data-ttu-id="114fe-144">Wybierz pozycję `Add file too...`</span><span class="sxs-lookup"><span data-stu-id="114fe-144">Select `Add file too...`</span></span>
3. <span data-ttu-id="114fe-145">Przejdź do folderu toohello, w którym wyodrębniono hello zestawu SDK</span><span class="sxs-lookup"><span data-stu-id="114fe-145">Navigate toohello folder where you extracted hello SDK</span></span>
4. <span data-ttu-id="114fe-146">Wybierz hello `EngagementReach` folderu</span><span class="sxs-lookup"><span data-stu-id="114fe-146">Select hello `EngagementReach` folder</span></span>
5. <span data-ttu-id="114fe-147">Kliknij pozycję Dodaj.</span><span class="sxs-lookup"><span data-stu-id="114fe-147">Click Add</span></span>
6. <span data-ttu-id="114fe-148">Edytuj hello mostkowanie nagłówków Reach usługi Mobile Engagement Objective-C nagłówka pliku tooexpose i Dodaj hello importuje następujące:</span><span class="sxs-lookup"><span data-stu-id="114fe-148">Edit hello bridging header file tooexpose Mobile Engagement Objective-C Reach headers and add hello following imports :</span></span>
   
        /* Mobile Engagement Reach */
        #import "AEAnnouncementViewController.h"
        #import "AEAutorotateView.h"
        #import "AEContentViewController.h"
        #import "AEDefaultAnnouncementViewController.h"
        #import "AEDefaultNotifier.h"
        #import "AEDefaultPollViewController.h"
        #import "AEInteractiveContent.h"
        #import "AENotificationView.h"
        #import "AENotifier.h"
        #import "AEPollViewController.h"
        #import "AEReachAbstractAnnouncement.h"
        #import "AEReachAnnouncement.h"
        #import "AEReachContent.h"
        #import "AEReachDataPush.h"
        #import "AEReachDataPushDelegate.h"
        #import "AEReachModule.h"
        #import "AEReachNotifAnnouncement.h"
        #import "AEReachPoll.h"
        #import "AEReachPollQuestion.h"
        #import "AEViewControllerUtil.h"
        #import "AEWebAnnouncementJsBridge.h"

### <a name="modify-your-application-delegate"></a><span data-ttu-id="114fe-149">Modyfikowanie delegata aplikacji</span><span class="sxs-lookup"><span data-stu-id="114fe-149">Modify your Application Delegate</span></span>
1. <span data-ttu-id="114fe-150">Witaj wewnątrz `didFinishLaunchingWithOptions` — Utwórz moduł reach i przekaż go tooyour istniejącego wiersza inicjowania usługi Engagement:</span><span class="sxs-lookup"><span data-stu-id="114fe-150">Inside  hello `didFinishLaunchingWithOptions` -  create a reach module and pass it tooyour existing Engagement initialization line:</span></span>
   
        func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplicationLaunchOptionsKey: Any]?) -> Bool 
        {
            let reach = AEReachModule.module(withNotificationIcon: UIImage(named:"icon.png")) as! AEReachModule
            EngagementAgent.init("Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}", modulesArray:[reach])
            [...]
            return true
        }

### <a name="enable-your-app-tooreceive-apns-push-notifications"></a><span data-ttu-id="114fe-151">Włącz tooreceive Twojej aplikacji powiadomień wypychanych usługi APNS</span><span class="sxs-lookup"><span data-stu-id="114fe-151">Enable your app tooreceive APNS Push Notifications</span></span>
1. <span data-ttu-id="114fe-152">Dodaj powitania po wierszu toohello `didFinishLaunchingWithOptions` metody:</span><span class="sxs-lookup"><span data-stu-id="114fe-152">Add hello following line toohello `didFinishLaunchingWithOptions` method:</span></span>
   
        if #available(iOS 8.0, *)
        {
            if #available(iOS 10.0, *)
            {
                UNUserNotificationCenter.current().requestAuthorization(options: [.alert, .badge, .sound]) { (granted, error) in }
            }else
            {
                let settings = UIUserNotificationSettings(types: [.alert, .badge, .sound], categories: nil)
                application.registerUserNotificationSettings(settings)
            }
            application.registerForRemoteNotifications()
        }
        else
        {
            application.registerForRemoteNotifications(matching: [.alert, .badge, .sound])
        }
2. <span data-ttu-id="114fe-153">Dodaj hello `didRegisterForRemoteNotificationsWithDeviceToken` metody w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="114fe-153">Add hello `didRegisterForRemoteNotificationsWithDeviceToken` method as follows:</span></span>
   
        func application(_ application: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: Data) {
            EngagementAgent.shared().registerDeviceToken(deviceToken)
        }
3. <span data-ttu-id="114fe-154">Dodaj hello `didReceiveRemoteNotification:fetchCompletionHandler:` metody w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="114fe-154">Add hello `didReceiveRemoteNotification:fetchCompletionHandler:` method as follows:</span></span>
   
        func application(_ application: UIApplication, didReceiveRemoteNotification userInfo: [AnyHashable : Any], fetchCompletionHandler completionHandler: @escaping (UIBackgroundFetchResult) -> Void) {
            EngagementAgent.shared().applicationDidReceiveRemoteNotification(userInfo, fetchCompletionHandler:completionHandler)
        }

[!INCLUDE [mobile-engagement-ios-send-push-push](../../includes/mobile-engagement-ios-send-push.md)]

<!-- URLs. -->
[Mobile Engagement iOS SDK]: http://aka.ms/qk2rnj

<!-- Images. -->
[1]: ./media/mobile-engagement-ios-get-started/xcode-add-files.png
[2]: ./media/mobile-engagement-ios-get-started/xcode-select-engagement-sdk.png
[3]: ./media/mobile-engagement-ios-get-started/xcode-build-phases.png
[4]: ./media/mobile-engagement-ios-swift-get-started/add-header-file.png
[5]: ./media/mobile-engagement-ios-get-started/app-connection-info-page.png
[6]: ./media/mobile-engagement-ios-swift-get-started/add-bridging-header.png
