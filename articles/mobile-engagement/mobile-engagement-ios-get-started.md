---
title: "Wprowadzenie do usługi Azure Mobile Engagement dla systemu iOS w języku Objective C | Microsoft Docs"
description: "Dowiedz się, jak używać usługi Azure Mobile Engagement razem z funkcją analizy i powiadomieniami wypychanymi na potrzeby aplikacji systemu iOS."
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
ms.openlocfilehash: 1b87a2ebb35b31ee3d3139ecead6267e62eb1033
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-ios-apps-in-objective-c"></a><span data-ttu-id="603ae-103">Wprowadzenie do usługi Azure Mobile Engagement dla aplikacji systemu iOS w języku Objective C</span><span class="sxs-lookup"><span data-stu-id="603ae-103">Get Started with Azure Mobile Engagement for iOS apps in Objective C</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="603ae-104">W tym temacie pokazano, jak za pomocą usługi Azure Mobile Engagement określać użycie aplikacji i wysyłać powiadomienia wypychane do danego segmentu użytkowników aplikacji systemu iOS.</span><span class="sxs-lookup"><span data-stu-id="603ae-104">This topic shows you how to use Azure Mobile Engagement to understand your app usage and send push notifications to segmented users to an iOS application.</span></span>
<span data-ttu-id="603ae-105">W tym samouczku zostanie utworzona pusta aplikacja systemu iOS służąca do zbierania podstawowych danych i odbierania powiadomień wypychanych przy użyciu systemu Apple Push Notification System (APNS).</span><span class="sxs-lookup"><span data-stu-id="603ae-105">In this tutorial, you create a blank iOS app that collects basic data and receives push notifications using Apple Push Notification System (APNS).</span></span>

<span data-ttu-id="603ae-106">Dla tego samouczka wymagane są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="603ae-106">This tutorial requires the following:</span></span>

* <span data-ttu-id="603ae-107">Edytor XCode 8, który można zainstalować ze sklepu Mac App Store</span><span class="sxs-lookup"><span data-stu-id="603ae-107">XCode 8, which you can install from your MAC App Store</span></span>
* <span data-ttu-id="603ae-108">Zestaw [Mobile Engagement iOS SDK]</span><span class="sxs-lookup"><span data-stu-id="603ae-108">the [Mobile Engagement iOS SDK]</span></span>

<span data-ttu-id="603ae-109">Wykonanie czynności opisanych w tym samouczku jest wymaganiem wstępnym dla wszystkich innych samouczków usługi Mobile Engagement dla aplikacji systemu iOS.</span><span class="sxs-lookup"><span data-stu-id="603ae-109">Completing this tutorial is a prerequisite for all other Mobile Engagement tutorials for iOS apps.</span></span>

> [!NOTE]
> <span data-ttu-id="603ae-110">Do wykonania kroków tego samouczka potrzebne jest aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="603ae-110">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="603ae-111">Jeśli go nie masz, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut.</span><span class="sxs-lookup"><span data-stu-id="603ae-111">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="603ae-112">Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-ios-get-started).</span><span class="sxs-lookup"><span data-stu-id="603ae-112">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-ios-get-started).</span></span>
>
>

## <span data-ttu-id="603ae-113"><a id="setup-azme"></a>Konfigurowanie usługi Mobile Engagement dla aplikacji systemu iOS</span><span class="sxs-lookup"><span data-stu-id="603ae-113"><a id="setup-azme"></a>Setup Mobile Engagement for your iOS app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="603ae-114"><a id="connecting-app"></a>Łączenie aplikacji z zapleczem usługi Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="603ae-114"><a id="connecting-app"></a>Connect your app to the Mobile Engagement backend</span></span>
<span data-ttu-id="603ae-115">Ten samouczek przedstawia „podstawową integrację”, tj. minimalny zestaw wymagany do zbierania danych i wysyłania powiadomień wypychanych.</span><span class="sxs-lookup"><span data-stu-id="603ae-115">This tutorial presents a "basic integration", which is the minimal set required to collect data and send a push notification.</span></span> <span data-ttu-id="603ae-116">Kompletna dokumentacja integracji znajduje się w sekcji [Mobile Engagement iOS SDK integration](mobile-engagement-ios-sdk-overview.md) (Integracja zestawu Mobile Engagement iOS SDK).</span><span class="sxs-lookup"><span data-stu-id="603ae-116">The complete integration documentation can be found in the [Mobile Engagement iOS SDK integration](mobile-engagement-ios-sdk-overview.md)</span></span>

<span data-ttu-id="603ae-117">Aby zademonstrować integrację, utworzymy podstawową aplikację za pomocą edytora XCode.</span><span class="sxs-lookup"><span data-stu-id="603ae-117">We will create a basic app with XCode to demonstrate the integration.</span></span>

### <a name="create-a-new-ios-project"></a><span data-ttu-id="603ae-118">Tworzenie nowego projektu systemu iOS</span><span class="sxs-lookup"><span data-stu-id="603ae-118">Create a new iOS project</span></span>
[!INCLUDE [Create a new iOS Project](../../includes/mobile-engagement-create-new-ios-app.md)]

### <a name="connect-your-app-to-the-mobile-engagement-backend"></a><span data-ttu-id="603ae-119">Łączenie aplikacji z zapleczem usługi Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="603ae-119">Connect your app to the Mobile Engagement backend</span></span>
1. <span data-ttu-id="603ae-120">Pobierz zestaw [Mobile Engagement iOS SDK].</span><span class="sxs-lookup"><span data-stu-id="603ae-120">Download the [Mobile Engagement iOS SDK].</span></span>
2. <span data-ttu-id="603ae-121">Wyodrębnij plik tar.gz do folderu na swoim komputerze.</span><span class="sxs-lookup"><span data-stu-id="603ae-121">Extract the .tar.gz file to a folder in your computer.</span></span>
3. <span data-ttu-id="603ae-122">Kliknij prawym przyciskiem myszy projekt i wybierz polecenie **Add files to** (Dodaj pliki do).</span><span class="sxs-lookup"><span data-stu-id="603ae-122">Right-click the project, and then select **Add files to**.</span></span>

    ![][1]
4. <span data-ttu-id="603ae-123">Przejdź do folderu, w którym został wyodrębniony zestaw SDK, wybierz folder `EngagementSDK` i kliknij pozycję **Opcje** w lewym dolnym rogu. Następnie upewnij się, że pole wyboru **Copy items if needed** (Kopiuj elementy w razie potrzeby) i pole wyboru Twojego miejsca docelowego są zaznaczone, po czym naciśnij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="603ae-123">Navigate to the folder where you extracted the SDK, select the `EngagementSDK` folder, click **Options** on the bottom left corner and make sure that the checkbox **Copy items if needed** and the checkbox for your target are checked then press **OK**.</span></span>

    ![][2]
5. <span data-ttu-id="603ae-124">Otwórz kartę **Build Phases** (Fazy kompilacji) i w menu **Link Binary With Libraries** (Połącz plik binarny z bibliotekami) dodaj następujące platformy (patrz ilustracja):</span><span class="sxs-lookup"><span data-stu-id="603ae-124">Open the **Build Phases** tab, and in the **Link Binary With Libraries** menu, add the frameworks as shown below:</span></span>

    ![][3]
6. <span data-ttu-id="603ae-125">Wróć do witryny Azure Portal na stronie **Informacje o połączeniu** w swojej aplikacji i skopiuj parametry połączenia.</span><span class="sxs-lookup"><span data-stu-id="603ae-125">Go back to the Azure portal in your app's **Connection Info** page and copy the connection string.</span></span>

    ![][4]
7. <span data-ttu-id="603ae-126">Dodaj następujący wiersz kodu w pliku **AppDelegate.m**.</span><span class="sxs-lookup"><span data-stu-id="603ae-126">Add the following line of code in your **AppDelegate.m** file.</span></span>

        #import "EngagementAgent.h"
8. <span data-ttu-id="603ae-127">Wklej parametry połączenia w delegacie `didFinishLaunchingWithOptions`.</span><span class="sxs-lookup"><span data-stu-id="603ae-127">Now paste the connection string in the `didFinishLaunchingWithOptions` delegate.</span></span>

        - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
        {
              [...]   
              [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}"];
              [...]
        }
9. <span data-ttu-id="603ae-128">Instrukcja `setTestLogEnabled` jest instrukcją opcjonalną, która umożliwia włączenie dzienników zestawu SDK w celu identyfikowania problemów.</span><span class="sxs-lookup"><span data-stu-id="603ae-128">`setTestLogEnabled` is an optional statement which enables SDK logs for you to identify issues.</span></span>

## <span data-ttu-id="603ae-129"><a id="monitor"></a>Włączanie monitorowania w czasie rzeczywistym</span><span class="sxs-lookup"><span data-stu-id="603ae-129"><a id="monitor"></a>Enable real-time monitoring</span></span>
<span data-ttu-id="603ae-130">Aby rozpocząć wysyłanie danych i upewnić się, że użytkownicy są aktywni, konieczne jest wysłanie co najmniej jednego ekranu (Działanie) do zaplecza usługi Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="603ae-130">In order to start sending data and ensuring that the users are active, you must send at least one screen (Activity) to the Mobile Engagement backend.</span></span>

1. <span data-ttu-id="603ae-131">Otwórz plik **ViewController.h** i zaimportuj element **EngagementViewController.h**:</span><span class="sxs-lookup"><span data-stu-id="603ae-131">Open the **ViewController.h** file and import **EngagementViewController.h**:</span></span>

    `#import "EngagementViewController.h"`
2. <span data-ttu-id="603ae-132">Następnie zastąp superklasę interfejsu **ViewController** elementem `EngagementViewController`:</span><span class="sxs-lookup"><span data-stu-id="603ae-132">Now replace the super class of the **ViewController** interface by `EngagementViewController`:</span></span>

    `@interface ViewController : EngagementViewController`

## <span data-ttu-id="603ae-133"><a id="monitor"></a>Łączenie aplikacji z funkcją monitorowania w czasie rzeczywistym</span><span class="sxs-lookup"><span data-stu-id="603ae-133"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="603ae-134"><a id="integrate-push"></a>Włączanie powiadomień wypychanych i funkcji komunikatów w aplikacji</span><span class="sxs-lookup"><span data-stu-id="603ae-134"><a id="integrate-push"></a>Enable push notifications and in-app messaging</span></span>
<span data-ttu-id="603ae-135">Usługa Mobile Engagement umożliwia wchodzenie w interakcję z użytkownikami i modułem REACH przy użyciu powiadomień wypychanych i komunikatów w aplikacji w kontekście kampanii.</span><span class="sxs-lookup"><span data-stu-id="603ae-135">Mobile Engagement allows you to interact with your users and REACH with push notifications and in-app messaging in the context of campaigns.</span></span> <span data-ttu-id="603ae-136">Ten moduł w portalu Mobile Engagement ma nazwę REACH.</span><span class="sxs-lookup"><span data-stu-id="603ae-136">This module is called REACH in the Mobile Engagement portal.</span></span>
<span data-ttu-id="603ae-137">W poniższych sekcjach aplikacja zostanie skonfigurowana do ich odbierania.</span><span class="sxs-lookup"><span data-stu-id="603ae-137">The following sections set up your app to receive them.</span></span>

### <a name="enable-your-app-to-receive-silent-push-notifications"></a><span data-ttu-id="603ae-138">Umożliwianie aplikacji otrzymywania cichych powiadomień wypychanych</span><span class="sxs-lookup"><span data-stu-id="603ae-138">Enable your app to receive Silent Push Notifications</span></span>
[!INCLUDE [mobile-engagement-ios-silent-push](../../includes/mobile-engagement-ios-silent-push.md)]

### <a name="add-the-reach-library-to-your-project"></a><span data-ttu-id="603ae-139">Dodawanie biblioteki Reach do projektu</span><span class="sxs-lookup"><span data-stu-id="603ae-139">Add the Reach library to your project</span></span>
1. <span data-ttu-id="603ae-140">Kliknij prawym przyciskiem myszy projekt.</span><span class="sxs-lookup"><span data-stu-id="603ae-140">Right-click your project.</span></span>
2. <span data-ttu-id="603ae-141">Wybierz pozycję **Add file to** (Dodaj plik do).</span><span class="sxs-lookup"><span data-stu-id="603ae-141">Select **Add file to**.</span></span>
3. <span data-ttu-id="603ae-142">Przejdź do folderu, w którym został wyodrębniony zestaw SDK.</span><span class="sxs-lookup"><span data-stu-id="603ae-142">Navigate to the folder where you extracted the SDK.</span></span>
4. <span data-ttu-id="603ae-143">Wybierz folder `EngagementReach`.</span><span class="sxs-lookup"><span data-stu-id="603ae-143">Select the `EngagementReach` folder.</span></span>
5. <span data-ttu-id="603ae-144">Kliknij pozycję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="603ae-144">Click **Add**.</span></span>

### <a name="modify-your-application-delegate"></a><span data-ttu-id="603ae-145">Modyfikowanie delegata aplikacji</span><span class="sxs-lookup"><span data-stu-id="603ae-145">Modify your Application Delegate</span></span>
1. <span data-ttu-id="603ae-146">Wróć do pliku **AppDelegate.m** i zaimportuj moduł Reach usługi Engagement.</span><span class="sxs-lookup"><span data-stu-id="603ae-146">Back in **AppDeletegate.m** file, import the Engagement Reach module.</span></span>

        #import "AEReachModule.h"
        #import <UserNotifications/UserNotifications.h>
2. <span data-ttu-id="603ae-147">Wewnątrz metody `application:didFinishLaunchingWithOptions` utwórz moduł Reach i uwzględnij go w istniejącym wierszu inicjowania usługi Engagement:</span><span class="sxs-lookup"><span data-stu-id="603ae-147">Inside the `application:didFinishLaunchingWithOptions` method, create a Reach module and pass it to your existing Engagement initialization line:</span></span>

        - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
            AEReachModule * reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
            [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}" modules:reach, nil];
            [...]
            return YES;
        }

### <a name="enable-your-app-to-receive-apns-push-notifications"></a><span data-ttu-id="603ae-148">Umożliwianie aplikacji otrzymywania powiadomień wypychanych usługi APNS</span><span class="sxs-lookup"><span data-stu-id="603ae-148">Enable your app to receive APNS Push Notifications</span></span>
1. <span data-ttu-id="603ae-149">Dodaj następujący wiersz do metody `application:didFinishLaunchingWithOptions`:</span><span class="sxs-lookup"><span data-stu-id="603ae-149">Add the following line to the `application:didFinishLaunchingWithOptions` method:</span></span>

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
2. <span data-ttu-id="603ae-150">Dodaj metodę `application:didRegisterForRemoteNotificationsWithDeviceToken` w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="603ae-150">Add the `application:didRegisterForRemoteNotificationsWithDeviceToken` method as follows:</span></span>

        - (void)application:(UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken
        {
             [[EngagementAgent shared] registerDeviceToken:deviceToken];
            NSLog(@"Registered Token: %@", deviceToken);
        }
3. <span data-ttu-id="603ae-151">Dodaj metodę `didFailToRegisterForRemoteNotificationsWithError` w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="603ae-151">Add the `didFailToRegisterForRemoteNotificationsWithError` method as follows:</span></span>

        - (void)application:(UIApplication*)application didFailToRegisterForRemoteNotificationsWithError:(NSError*)error
        {
           NSLog(@"Failed to get token, error: %@", error);
        }
4. <span data-ttu-id="603ae-152">Dodaj metodę `didReceiveRemoteNotification:fetchCompletionHandler` w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="603ae-152">Add the `didReceiveRemoteNotification:fetchCompletionHandler` method as follows:</span></span>

        - (void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult result))handler
        {
            [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:handler];
        }

[!INCLUDE [mobile-engagement-ios-send-push-push](../../includes/mobile-engagement-ios-send-push.md)]

<!-- URLs. -->
<span data-ttu-id="603ae-153">[Mobile Engagement iOS SDK]: http://aka.ms/qk2rnj</span><span class="sxs-lookup"><span data-stu-id="603ae-153">[Mobile Engagement iOS SDK]: http://aka.ms/qk2rnj</span></span>

<!-- Images. -->
[1]: ./media/mobile-engagement-ios-get-started/xcode-add-files.png
[2]: ./media/mobile-engagement-ios-get-started/xcode-select-engagement-sdk.png
[3]: ./media/mobile-engagement-ios-get-started/xcode-build-phases.png
[4]: ./media/mobile-engagement-ios-get-started/app-connection-info-page.png
