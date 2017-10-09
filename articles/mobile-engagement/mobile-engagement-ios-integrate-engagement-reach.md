---
title: "aaaAzure Mobile Engagement iOS SDK Integration osiągnąć | Dokumentacja firmy Microsoft"
description: "Najnowsze aktualizacje i procedury dla systemu iOS SDK dla usługi Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 1f5f5857-867c-40c5-9d76-675a343a0296
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 12/13/2016
ms.author: piyushjo
ms.openlocfilehash: 40c9bfbdb475ab0b97bdbc9cea798a59cb8a71ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toointegrate-engagement-reach-on-ios"></a><span data-ttu-id="ee920-103">W jaki sposób Reach usługi Engagement tooIntegrate w systemie iOS</span><span class="sxs-lookup"><span data-stu-id="ee920-103">How tooIntegrate Engagement Reach on iOS</span></span>
<span data-ttu-id="ee920-104">Musisz wykonać procedurę integracji hello opisanego w hello [jak tooIntegrate Engagement iOS dokumentu](mobile-engagement-ios-integrate-engagement.md) przed wykonaniem tego przewodnika.</span><span class="sxs-lookup"><span data-stu-id="ee920-104">You must follow hello integration procedure described in hello [How tooIntegrate Engagement on iOS document](mobile-engagement-ios-integrate-engagement.md) before following this guide.</span></span>

<span data-ttu-id="ee920-105">Ta dokumentacja wymaga XCode 8.</span><span class="sxs-lookup"><span data-stu-id="ee920-105">This documentation requires XCode 8.</span></span> <span data-ttu-id="ee920-106">Jeśli naprawdę są zależne od XCode 7, możesz użyć hello [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh).</span><span class="sxs-lookup"><span data-stu-id="ee920-106">If you really depend on XCode 7 then you may use hello [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh).</span></span> <span data-ttu-id="ee920-107">Jest znaną usterką w poprzedniej podczas uruchamiania na urządzeniach z systemem iOS 10: powiadomień systemowych nie są których wykonano akcje.</span><span class="sxs-lookup"><span data-stu-id="ee920-107">There is a known bug on this previous version while running on iOS 10 devices:  system notifications are not actioned.</span></span> <span data-ttu-id="ee920-108">toofix to będzie miał tooimplement hello przestarzałe interfejsu API `application:didReceiveRemoteNotification:` w aplikacji delegowanie w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="ee920-108">toofix this you will have tooimplement hello deprecated API `application:didReceiveRemoteNotification:` in your app delegate as follows:</span></span>

    - (void)application:(UIApplication*)application
    didReceiveRemoteNotification:(NSDictionary*)userInfo
    {
        [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:nil];
    }

> [!IMPORTANT]
> <span data-ttu-id="ee920-109">**Nie zaleca się rozwiązanie** jak to zachowanie można zmienić w jakiegokolwiek uaktualnienia wersji nadchodzących iOS (nawet pomocnicze), ponieważ ten iOS interfejsu API jest przestarzały.</span><span class="sxs-lookup"><span data-stu-id="ee920-109">**We do not recommend this workaround** as this behavior can change in any upcoming (even minor) iOS version upgrade because this iOS API is deprecated.</span></span> <span data-ttu-id="ee920-110">Należy jak najszybciej przełącznika tooXCode 8.</span><span class="sxs-lookup"><span data-stu-id="ee920-110">You should switch tooXCode 8 as soon as possible.</span></span>
>
>

### <a name="enable-your-app-tooreceive-silent-push-notifications"></a><span data-ttu-id="ee920-111">Włącz tooreceive Twojej aplikacji cichych powiadomień wypychanych</span><span class="sxs-lookup"><span data-stu-id="ee920-111">Enable your app tooreceive Silent Push Notifications</span></span>
[!INCLUDE [mobile-engagement-ios-silent-push](../../includes/mobile-engagement-ios-silent-push.md)]

## <a name="integration-steps"></a><span data-ttu-id="ee920-112">Kroki integracji</span><span class="sxs-lookup"><span data-stu-id="ee920-112">Integration steps</span></span>
### <a name="embed-hello-engagement-reach-sdk-into-your-ios-project"></a><span data-ttu-id="ee920-113">Osadź hello Engagement Reach SDK do projektu systemu iOS</span><span class="sxs-lookup"><span data-stu-id="ee920-113">Embed hello Engagement Reach SDK into your iOS project</span></span>
* <span data-ttu-id="ee920-114">Dodawanie zestawu sdk modułu Reach hello w projekcie Xcode.</span><span class="sxs-lookup"><span data-stu-id="ee920-114">Add hello Reach sdk in your Xcode project.</span></span> <span data-ttu-id="ee920-115">W środowisku Xcode Przejdź zbyt**projektu \> dodać tooproject** i wybierz polecenie hello `EngagementReach` folderu.</span><span class="sxs-lookup"><span data-stu-id="ee920-115">In Xcode, go too**Project \> Add tooproject** and choose hello `EngagementReach` folder.</span></span>

### <a name="modify-your-application-delegate"></a><span data-ttu-id="ee920-116">Modyfikowanie delegata aplikacji</span><span class="sxs-lookup"><span data-stu-id="ee920-116">Modify your Application Delegate</span></span>
* <span data-ttu-id="ee920-117">U góry hello pliku implementacji Zaimportuj moduł Reach usługi Engagement hello:</span><span class="sxs-lookup"><span data-stu-id="ee920-117">At hello top of your implementation file, import hello Engagement Reach module:</span></span>

      [...]
      #import "AEReachModule.h"
* <span data-ttu-id="ee920-118">Wewnątrz metody `applicationDidFinishLaunching:` lub `application:didFinishLaunchingWithOptions:`, Utwórz moduł reach i przekaż go tooyour istniejącego wiersza inicjowania usługi Engagement:</span><span class="sxs-lookup"><span data-stu-id="ee920-118">Inside method `applicationDidFinishLaunching:` or `application:didFinishLaunchingWithOptions:`, create a reach module and pass it tooyour existing Engagement initialization line:</span></span>

      - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
        AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
        [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}" modules:reach, nil];
        [...]

        return YES;
      }
* <span data-ttu-id="ee920-119">Modyfikowanie **"icon.png"** ciągu o nazwie obraz powitania ma jako ikonę powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="ee920-119">Modify **'icon.png'** string with hello image name you want as your notification icon.</span></span>
* <span data-ttu-id="ee920-120">Jeśli chcesz, aby opcja hello toouse *wartość wskaźnika aktualizacji* kampanie Zasięgowe lub jeśli chcesz natywnych powiadomień wypychanych toouse \<SaaS/Reach interfejsu API/kampanii format/Native Push\> kampanie, należy przeprowadzić moduł Reach hello Zarządzanie Witaj wskaźnika ikona sam (zostanie automatycznie usunięty wskaźnika aplikacji hello i również zresetować wartość hello przechowywane przez zaangażowania za każdym razem, gdy aplikacja hello jest uruchomiony lub foregrounded).</span><span class="sxs-lookup"><span data-stu-id="ee920-120">If you want toouse hello option *Update badge value* in Reach campaigns or if you want toouse native push \</SaaS/Reach API/Campaign format/Native Push\> campaigns, you must let hello Reach module manage hello badge icon itself (it will automatically clear hello application badge and also reset hello value stored by Engagement every time hello application is started or foregrounded).</span></span> <span data-ttu-id="ee920-121">Można to zrobić przez dodanie następującego wiersza po zainicjowaniu modułu Reach hello:</span><span class="sxs-lookup"><span data-stu-id="ee920-121">This is done by adding hello following line after Reach module initialization:</span></span>

      [reach setAutoBadgeEnabled:YES];
* <span data-ttu-id="ee920-122">Jeśli chcesz wypychanie danych Reach toohandle musi umożliwić delegata aplikacji jest zgodna z toohello `AEReachDataPushDelegate` protokołu.</span><span class="sxs-lookup"><span data-stu-id="ee920-122">If you want toohandle Reach data push, you must let your Application delegate conform toohello `AEReachDataPushDelegate` protocol.</span></span> <span data-ttu-id="ee920-123">Dodaj następującego wiersza po zainicjowaniu modułu Reach hello:</span><span class="sxs-lookup"><span data-stu-id="ee920-123">Add hello following line after Reach module initialization:</span></span>

      [reach setDataPushDelegate:self];
* <span data-ttu-id="ee920-124">Następnie można zaimplementować metody hello `onDataPushStringReceived:` i `onDataPushBase64ReceivedWithDecodedBody:andEncodedBody:` w delegata aplikacji:</span><span class="sxs-lookup"><span data-stu-id="ee920-124">Then you can implement hello methods `onDataPushStringReceived:` and `onDataPushBase64ReceivedWithDecodedBody:andEncodedBody:` in your application delegate:</span></span>

      -(BOOL)didReceiveStringDataPushWithCategory:(NSString*)category body:(NSString*)body
      {
         NSLog(@"String data push message with category <%@> received: %@", category, body);
         return YES;
      }

      -(BOOL)didReceiveBase64DataPushWithCategory:(NSString*)category decodedBody:(NSData *)decodedBody encodedBody:(NSString *)encodedBody
      {
         NSLog(@"Base64 data push message with category <%@> received: %@", category, encodedBody);
         // Do something useful with decodedBody like updating an image view
         return YES;
      }

### <a name="category"></a><span data-ttu-id="ee920-125">Kategoria</span><span class="sxs-lookup"><span data-stu-id="ee920-125">Category</span></span>
<span data-ttu-id="ee920-126">Witaj kategorii parametr jest opcjonalny, podczas tworzenia kampanii wypychania danych i umożliwia wypychanie danych toofilter.</span><span class="sxs-lookup"><span data-stu-id="ee920-126">hello category parameter is optional when you create a Data Push campaign and allows you toofilter data pushes.</span></span> <span data-ttu-id="ee920-127">Jest to przydatne w przypadku różnych rodzajów toopush z `Base64` tooidentify danych i chcesz ich typu przed ich analizowania.</span><span class="sxs-lookup"><span data-stu-id="ee920-127">This is useful if you want toopush different kinds of `Base64` data and want tooidentify their type before parsing them.</span></span>

<span data-ttu-id="ee920-128">**Aplikacja jest teraz gotowy tooreceive i wyświetlanie osiągnąć zawartość!**</span><span class="sxs-lookup"><span data-stu-id="ee920-128">**Your application is now ready tooreceive and display reach contents!**</span></span>

## <a name="how-tooreceive-announcements-and-polls-at-any-time"></a><span data-ttu-id="ee920-129">Jak tooreceive anonsów i sond w dowolnym momencie</span><span class="sxs-lookup"><span data-stu-id="ee920-129">How tooreceive announcements and polls at any time</span></span>
<span data-ttu-id="ee920-130">Zaangażowania można wysłać powiadomienia Reach tooyour użytkowników końcowych w dowolnym momencie przy użyciu hello Apple Push Notification Service.</span><span class="sxs-lookup"><span data-stu-id="ee920-130">Engagement can send Reach notifications tooyour end users at any time by using hello Apple Push Notification Service.</span></span>

<span data-ttu-id="ee920-131">tooenable ta funkcja zostanie tooprepare aplikacji dla powiadomień wypychanych firmy Apple oraz modyfikowanie delegata aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ee920-131">tooenable this functionality, you'll have tooprepare your application for Apple push notifications and modify your application delegate.</span></span>

### <a name="prepare-your-application-for-apple-push-notifications"></a><span data-ttu-id="ee920-132">Przygotowanie aplikacji dla powiadomień wypychanych firmy Apple</span><span class="sxs-lookup"><span data-stu-id="ee920-132">Prepare your application for Apple push notifications</span></span>
<span data-ttu-id="ee920-133">Wykonaj przewodnik hello: [jak tooPrepare aplikacji dla powiadomień wypychanych firmy Apple](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html#//apple_ref/doc/uid/TP40012582-CH26-SW6)</span><span class="sxs-lookup"><span data-stu-id="ee920-133">Please follow hello guide : [How tooPrepare your Application for Apple Push Notifications](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html#//apple_ref/doc/uid/TP40012582-CH26-SW6)</span></span>

### <a name="add-hello-necessary-client-code"></a><span data-ttu-id="ee920-134">Dodaj kod klienta konieczne hello</span><span class="sxs-lookup"><span data-stu-id="ee920-134">Add hello necessary client code</span></span>
<span data-ttu-id="ee920-135">*W tym momencie aplikacji powinien mieć zarejestrowany certyfikat usługi Apple push hello zaangażowania frontonu.*</span><span class="sxs-lookup"><span data-stu-id="ee920-135">*At this point your application should have a registered Apple push certificate in hello Engagement frontend.*</span></span>

<span data-ttu-id="ee920-136">Jeśli nie jest jeszcze zrobione, należy tooregister powiadomień wypychanych tooreceive aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ee920-136">If it's not done already, you need tooregister your application tooreceive push notifications.</span></span>

* <span data-ttu-id="ee920-137">Importuj hello `User Notification` framework:</span><span class="sxs-lookup"><span data-stu-id="ee920-137">Import hello `User Notification` framework:</span></span>

        #import <UserNotifications/UserNotifications.h>
* <span data-ttu-id="ee920-138">Dodaj powitania po wierszu, po uruchomieniu aplikacji (zwykle w `application:didFinishLaunchingWithOptions:`):</span><span class="sxs-lookup"><span data-stu-id="ee920-138">Add hello following line when your application starts (typically in `application:didFinishLaunchingWithOptions:`):</span></span>

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

<span data-ttu-id="ee920-139">Następnie należy tooprovide tooEngagement hello urządzenia tokenów zwracanych przez serwery firmy Apple.</span><span class="sxs-lookup"><span data-stu-id="ee920-139">Then, You need tooprovide tooEngagement hello device token returned by Apple servers.</span></span> <span data-ttu-id="ee920-140">Odbywa się w metodzie hello o nazwie `application:didRegisterForRemoteNotificationsWithDeviceToken:` w delegata aplikacji:</span><span class="sxs-lookup"><span data-stu-id="ee920-140">This is done in hello method named `application:didRegisterForRemoteNotificationsWithDeviceToken:` in your application delegate:</span></span>

    - (void)application:(UIApplication*)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData*)deviceToken
    {
        [[EngagementAgent shared] registerDeviceToken:deviceToken];
    }

<span data-ttu-id="ee920-141">Koniec mamy jeszcze hello tooinform Engagement SDK, gdy aplikacja otrzyma powiadomienie zdalnego.</span><span class="sxs-lookup"><span data-stu-id="ee920-141">Finally, you have tooinform hello Engagement SDK when your application receives a remote notification.</span></span> <span data-ttu-id="ee920-142">toodo, który wywołać hello metody `applicationDidReceiveRemoteNotification:fetchCompletionHandler:` w delegata aplikacji:</span><span class="sxs-lookup"><span data-stu-id="ee920-142">toodo that, call hello method `applicationDidReceiveRemoteNotification:fetchCompletionHandler:` in your application delegate:</span></span>

    - (void)application:(UIApplication*)application didReceiveRemoteNotification:(NSDictionary*)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult result))handler
    {
        [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:handler];
    }

> [!IMPORTANT]
> <span data-ttu-id="ee920-143">Domyślnie Reach usługi Engagement steruje hello completionHandler.</span><span class="sxs-lookup"><span data-stu-id="ee920-143">By default, Engagement Reach controls hello completionHandler.</span></span> <span data-ttu-id="ee920-144">Jeśli chcesz, aby toohello odpowiedź toomanually `handler` bloków w kodzie, można przekazać nil dla hello `handler` argumentu i kontroli uzupełniania hello zablokować samodzielnie.</span><span class="sxs-lookup"><span data-stu-id="ee920-144">If you want toomanually respond toohello `handler` block in your code, you can pass nil for hello `handler` argument and control hello completion block yourself.</span></span> <span data-ttu-id="ee920-145">Zobacz hello `UIBackgroundFetchResult` typu listę możliwych wartości.</span><span class="sxs-lookup"><span data-stu-id="ee920-145">See hello `UIBackgroundFetchResult` type for a list of possible values.</span></span>
>
>

### <a name="full-example"></a><span data-ttu-id="ee920-146">Pełny przykład</span><span class="sxs-lookup"><span data-stu-id="ee920-146">Full example</span></span>
<span data-ttu-id="ee920-147">Oto pełny przykład integracji:</span><span class="sxs-lookup"><span data-stu-id="ee920-147">Here is a full example of integration:</span></span>

    #pragma mark -
    #pragma mark Application lifecycle

    - (BOOL)application:(UIApplication*)application didFinishLaunchingWithOptions:(NSDictionary*)launchOptions
    {
      /* Reach module */
      AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
      [reach setAutoBadgeEnabled:YES];

      /* Engagement initialization */
      [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}" modules:reach, nil];
      [[EngagementAgent shared] setPushDelegate:self];

      /* Views */
      [window addSubview:[tabBarController view]];
      [window makeKeyAndVisible];

      [application registerForRemoteNotificationTypes:UIRemoteNotificationTypeAlert|UIRemoteNotificationTypeBadge|UIRemoteNotificationTypeSound];
      return YES;
    }

    - (void)application:(UIApplication*)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData*)deviceToken
    {
      [[EngagementAgent shared] registerDeviceToken:deviceToken];
    }

    - (void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult result))handler
    {
        [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:handler];
    }

### <a name="resolve-unusernotificationcenter-delegate-conflicts"></a><span data-ttu-id="ee920-148">Rozwiązywanie konfliktów delegata UNUserNotificationCenter</span><span class="sxs-lookup"><span data-stu-id="ee920-148">Resolve UNUserNotificationCenter delegate conflicts</span></span>

<span data-ttu-id="ee920-149">*Jeśli implementuje jednej z bibliotek innych firm ani aplikacji `UNUserNotificationCenterDelegate` , a następnie można pominąć tej części.*</span><span class="sxs-lookup"><span data-stu-id="ee920-149">*If neither your application or one of your third party libraries implements a `UNUserNotificationCenterDelegate` then you can skip this part.*</span></span>

<span data-ttu-id="ee920-150">A `UNUserNotificationCenter` delegata jest używany przez hello SDK toomonitor hello cyklu życia zaangażowania powiadomienia na urządzeniach z systemem iOS, 10 lub nowszy.</span><span class="sxs-lookup"><span data-stu-id="ee920-150">A `UNUserNotificationCenter` delegate is used by hello SDK toomonitor hello life cycle of Engagement notifications on devices running on iOS 10 or greater.</span></span> <span data-ttu-id="ee920-151">Witaj SDK ma własną implementację hello `UNUserNotificationCenterDelegate` protokołu, ale może istnieć tylko jedna `UNUserNotificationCenter` delegować na aplikację.</span><span class="sxs-lookup"><span data-stu-id="ee920-151">hello SDK has its own implementation of hello `UNUserNotificationCenterDelegate` protocol but there can be only one `UNUserNotificationCenter` delegate per application.</span></span> <span data-ttu-id="ee920-152">Inne delegata dodane toohello `UNUserNotificationCenter` obiektu może powodować konflikt z hello zaangażowania jeden.</span><span class="sxs-lookup"><span data-stu-id="ee920-152">Any other delegate added toohello `UNUserNotificationCenter` object will conflict with hello Engagement one.</span></span> <span data-ttu-id="ee920-153">Jeśli hello SDK wykryje użytkownika lub dowolnej innej strony trzeciej na delegata nie zastosuje toogive własną implementację możesz tooresolve szansy hello konfliktów.</span><span class="sxs-lookup"><span data-stu-id="ee920-153">If hello SDK detects your or any other third party's delegate then it will not use its own implementation toogive you a chance tooresolve hello conflicts.</span></span> <span data-ttu-id="ee920-154">Konieczne będzie tooadd hello zaangażowania logiki tooyour właścicielem delegata w kolejności tooresolve hello konfliktów.</span><span class="sxs-lookup"><span data-stu-id="ee920-154">You will have tooadd hello Engagement logic tooyour own delegate in order tooresolve hello conflicts.</span></span>

<span data-ttu-id="ee920-155">Istnieją dwa sposoby tooachieve to.</span><span class="sxs-lookup"><span data-stu-id="ee920-155">There are two ways tooachieve this.</span></span>

<span data-ttu-id="ee920-156">Wniosek 1, po prostu przesyłając pełnomocnika wywołuje toohello zestawu SDK:</span><span class="sxs-lookup"><span data-stu-id="ee920-156">Proposal 1, simply by forwarding your delegate calls toohello SDK:</span></span>

    #import <UIKit/UIKit.h>
    #import "EngagementAgent.h"
    #import <UserNotifications/UserNotifications.h>


    @interface MyAppDelegate : NSObject <UIApplicationDelegate, UNUserNotificationCenterDelegate>
    @end

    @implementation MyAppDelegate

    - (void)userNotificationCenter:(UNUserNotificationCenter *)center willPresentNotification:(UNNotification *)notification withCompletionHandler:(void (^)(UNNotificationPresentationOptions options))completionHandler
    {
      // Your own logic.

      [[EngagementAgent shared] userNotificationCenterWillPresentNotification:notification withCompletionHandler:completionHandler]
    }

    - (void)userNotificationCenter:(UNUserNotificationCenter *)center didReceiveNotificationResponse:(UNNotificationResponse *)response withCompletionHandler:(void(^)())completionHandler
    {
      // Your own logic.

      [[EngagementAgent shared] userNotificationCenterDidReceiveNotificationResponse:response withCompletionHandler:completionHandler]
    }
    @end

<span data-ttu-id="ee920-157">Lub propozycji 2, dziedziczenie z hello `AEUserNotificationHandler` — klasa</span><span class="sxs-lookup"><span data-stu-id="ee920-157">Or proposal 2, by inheriting from hello `AEUserNotificationHandler` class</span></span>

    #import "AEUserNotificationHandler.h"
    #import "EngagementAgent.h"

    @interface CustomUserNotificationHandler :AEUserNotificationHandler
    @end

    @implementation CustomUserNotificationHandler

    - (void)userNotificationCenter:(UNUserNotificationCenter *)center willPresentNotification:(UNNotification *)notification withCompletionHandler:(void (^)(UNNotificationPresentationOptions options))completionHandler
    {
      // Your own logic.

      [super userNotificationCenter:center willPresentNotification:notification withCompletionHandler:completionHandler];
    }

    - (void)userNotificationCenter:(UNUserNotificationCenter *)center didReceiveNotificationResponse: UNNotificationResponse *)response withCompletionHandler:(void(^)())completionHandler
    {
      // Your own logic.

      [super userNotificationCenter:center didReceiveNotificationResponse:response withCompletionHandler:completionHandler];
    }

    @end

> [!NOTE]
> <span data-ttu-id="ee920-158">Można określić, czy powiadomienie jest dostarczany z zaangażowania lub nie przez przekazanie jej `userInfo` toohello słownika agenta `isEngagementPushPayload:` metoda klasy.</span><span class="sxs-lookup"><span data-stu-id="ee920-158">You can determine whether a notification comes from Engagement or not by passing its `userInfo` dictionary toohello Agent `isEngagementPushPayload:` class method.</span></span>

<span data-ttu-id="ee920-159">Upewnij się, że hello `UNUserNotificationCenter` obiektu delegowanego ustawiono tooyour delegata w obu hello `application:willFinishLaunchingWithOptions:` lub hello `application:didFinishLaunchingWithOptions:` metody delegata aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ee920-159">Make sure that hello `UNUserNotificationCenter` object's delegate is set tooyour delegate within either hello `application:willFinishLaunchingWithOptions:` or hello `application:didFinishLaunchingWithOptions:` method of your application delegate.</span></span>
<span data-ttu-id="ee920-160">Na przykład jeśli zaimplementowano hello powyżej wniosek 1:</span><span class="sxs-lookup"><span data-stu-id="ee920-160">For instance, if you implemented hello above proposal 1:</span></span>

      - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
        // Any other code

        [UNUserNotificationCenter currentNotificationCenter].delegate = self;
        return YES;
      }

## <a name="how-toocustomize-campaigns"></a><span data-ttu-id="ee920-161">Jak toocustomize kampanii</span><span class="sxs-lookup"><span data-stu-id="ee920-161">How toocustomize campaigns</span></span>
### <a name="notifications"></a><span data-ttu-id="ee920-162">Powiadomienia</span><span class="sxs-lookup"><span data-stu-id="ee920-162">Notifications</span></span>
<span data-ttu-id="ee920-163">Istnieją dwa typy powiadomień: powiadomień systemowych i w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ee920-163">There are two types of notifications: system and in-app notifications.</span></span>

<span data-ttu-id="ee920-164">Powiadomienia systemowe są obsługiwane przez system iOS i nie można dostosować.</span><span class="sxs-lookup"><span data-stu-id="ee920-164">System notifications are handled by iOS, and cannot be customized.</span></span>

<span data-ttu-id="ee920-165">W aplikacji zawiadomienia widoku, który jest dodawane dynamicznie toohello bieżące okno aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ee920-165">In-app notifications are made of a view that is dynamically added toohello current application window.</span></span> <span data-ttu-id="ee920-166">Jest to nakładce powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="ee920-166">This is called a notification overlay.</span></span> <span data-ttu-id="ee920-167">Nakładki powiadomienia są bardzo szybkiego integracji, ponieważ wymagają one, nie możesz toomodify dowolnym widoku w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ee920-167">Notification overlays are great for a fast integration because they does not require you toomodify any view in your application.</span></span>

#### <a name="layout"></a><span data-ttu-id="ee920-168">Układ</span><span class="sxs-lookup"><span data-stu-id="ee920-168">Layout</span></span>
<span data-ttu-id="ee920-169">wygląd hello toomodify powiadomienia w aplikacji, wystarczy zmodyfikować plik hello `AENotificationView.xib` tooyour musi, tak długo, jak zabezpieczyć hello wartości tagów i typy widoków istniejących podrzędnych hello.</span><span class="sxs-lookup"><span data-stu-id="ee920-169">toomodify hello look of your in-app notifications, you can simply modify hello file `AENotificationView.xib` tooyour needs, as long as you keep hello tag values and types of hello existing subviews.</span></span>

<span data-ttu-id="ee920-170">Domyślnie powiadomienia w aplikacji są prezentowane u dołu hello hello ekranu.</span><span class="sxs-lookup"><span data-stu-id="ee920-170">By default, in-app notifications are presented at hello bottom of hello screen.</span></span> <span data-ttu-id="ee920-171">Jeśli wolisz toodisplay je u góry ekranu, Edytuj hello hello udostępnione `AENotificationView.xib` i zmień hello `AutoSizing` właściwości hello widoku głównego, mogą być przechowywane na górze hello jego superview.</span><span class="sxs-lookup"><span data-stu-id="ee920-171">If you prefer toodisplay them at hello top of screen, edit hello provided `AENotificationView.xib` and change hello `AutoSizing` property of hello main view so it can be kept at hello top of its superview.</span></span>

#### <a name="categories"></a><span data-ttu-id="ee920-172">Kategorie</span><span class="sxs-lookup"><span data-stu-id="ee920-172">Categories</span></span>
<span data-ttu-id="ee920-173">Po zmodyfikowaniu hello podane układu, możesz zmodyfikować wygląd hello wszystkich powiadomień.</span><span class="sxs-lookup"><span data-stu-id="ee920-173">When you modify hello provided layout, you modify hello look of all your notifications.</span></span> <span data-ttu-id="ee920-174">Kategorie dopuszczać toodefine możesz przez różne docelowe szuka powiadomienia (prawdopodobnie zachowania).</span><span class="sxs-lookup"><span data-stu-id="ee920-174">Categories allow you toodefine various targeted looks (possibly behaviors) for notifications.</span></span> <span data-ttu-id="ee920-175">Po utworzeniu kampanii Reach można określić kategorię.</span><span class="sxs-lookup"><span data-stu-id="ee920-175">A category can be specified when you create a Reach campaign.</span></span> <span data-ttu-id="ee920-176">Należy pamiętać, że kategorie pozwalają również dostosować anonsów i sond, opisane w dalszej części tego dokumentu.</span><span class="sxs-lookup"><span data-stu-id="ee920-176">Keep in mind that categories also let you customize announcements and polls, that is described later in this document.</span></span>

<span data-ttu-id="ee920-177">tooregister kategorii Obsługa powiadomienia, należy tooadd wywołania po modułu reach hello jest zainicjowana.</span><span class="sxs-lookup"><span data-stu-id="ee920-177">tooregister a category handler for your notifications, you need tooadd a call once hello reach module is initialized.</span></span>

    AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
    [reach registerNotifier:myNotifier forCategory:@"my_category"];
    ...

<span data-ttu-id="ee920-178">`myNotifier`musi być wystąpieniem obiektu, który jest zgodny z protokołem toohello `AENotifier`.</span><span class="sxs-lookup"><span data-stu-id="ee920-178">`myNotifier` must be an instance of an object that conforms toohello protocol `AENotifier`.</span></span>

<span data-ttu-id="ee920-179">Można zaimplementować metody protokołu hello samodzielnie lub możesz wybrać tooreimplement hello istniejącej klasy `AEDefaultNotifier` którego już wykonuje większość pracy hello.</span><span class="sxs-lookup"><span data-stu-id="ee920-179">You can implement hello protocol methods by yourself or you can choose tooreimplement hello existing class `AEDefaultNotifier` which already performs most of hello work.</span></span>

<span data-ttu-id="ee920-180">Na przykład jeśli chcesz widok powiadomienia hello tooredefine dla określonej kategorii, należy wykonać w tym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="ee920-180">For example, if you want tooredefine hello notification view for a specific category, you can follow this example:</span></span>

    #import "AEDefaultNotifier.h"
    #import "AENotificationView.h"
    @interface MyNotifier : AEDefaultNotifier
    @end

    @implementation MyNotifier

    -(NSString*)nibNameForCategory:(NSString*)category
    {
      return "MyNotificationView";
    }

    @end

<span data-ttu-id="ee920-181">Ten prosty przykład kategorii założono, że istnieje plik o nazwie `MyNotificationView.xib` w Twojego pakietu aplikacji głównej.</span><span class="sxs-lookup"><span data-stu-id="ee920-181">This simple example of category assume that you have a file named `MyNotificationView.xib` in your main application bundle.</span></span> <span data-ttu-id="ee920-182">Jeśli metoda hello nie jest możliwe toofind odpowiadającego `.xib`, nie będą wyświetlane powiadomienia hello i zaangażowania dane wyjściowe obejmują wiadomość hello konsoli.</span><span class="sxs-lookup"><span data-stu-id="ee920-182">If hello method is not able toofind a corresponding `.xib`, hello notification will not be displayed and Engagement will output a message in hello console.</span></span>

<span data-ttu-id="ee920-183">Hello podane nib pliku powinna być zgodna hello następujące reguły:</span><span class="sxs-lookup"><span data-stu-id="ee920-183">hello provided nib file should respect hello following rules:</span></span>

* <span data-ttu-id="ee920-184">Powinna ona zawierać tylko jeden widok.</span><span class="sxs-lookup"><span data-stu-id="ee920-184">It should only contain one view.</span></span>
* <span data-ttu-id="ee920-185">Widoków podrzędnych powinny być hello typy takie same jak hello tych wewnątrz hello podane nib plik o nazwie`AENotificationView.xib`</span><span class="sxs-lookup"><span data-stu-id="ee920-185">Subviews should be of hello same types as hello ones inside hello provided nib file named `AENotificationView.xib`</span></span>
* <span data-ttu-id="ee920-186">Widoków podrzędnych powinny mieć hello znaczniki takie same jak hello tych wewnątrz hello podane nib plik o nazwie`AENotificationView.xib`</span><span class="sxs-lookup"><span data-stu-id="ee920-186">Subviews should have hello same tags as hello ones inside hello provided nib file named `AENotificationView.xib`</span></span>

> [!TIP]
> <span data-ttu-id="ee920-187">Po prostu skopiuj hello podane nib plik o nazwie `AENotificationView.xib`i rozpocząć pracę z tego miejsca.</span><span class="sxs-lookup"><span data-stu-id="ee920-187">Just copy hello provided nib file, named `AENotificationView.xib`, and start working from there.</span></span> <span data-ttu-id="ee920-188">Jednak należy zachować ostrożność, hello widoku wewnątrz ten plik nib jest skojarzona klasa toohello `AENotificationView`.</span><span class="sxs-lookup"><span data-stu-id="ee920-188">But be careful, hello view inside this nib file is associated toohello class `AENotificationView`.</span></span> <span data-ttu-id="ee920-189">Ta klasa ponownie definiować metody hello `layoutSubViews` toomove i zmień rozmiar jego widoków podrzędnych zgodnie z toocontext.</span><span class="sxs-lookup"><span data-stu-id="ee920-189">This class redefined hello method `layoutSubViews` toomove and resize its subviews according toocontext.</span></span> <span data-ttu-id="ee920-190">Może być tooreplace za pomocą `UIView` lub klasy widok niestandardowy.</span><span class="sxs-lookup"><span data-stu-id="ee920-190">You may want tooreplace it with an `UIView` or you custom view class.</span></span>
>
>

<span data-ttu-id="ee920-191">Jeśli potrzebujesz bardziej dostosowywania powiadomienia (Jeśli na przykład tooload widoku bezpośrednio z kodu hello), zalecane jest tootake przyjrzeć się hello podano źródła kodu i klasy w dokumentacji `Protocol ReferencesDefaultNotifier` i `AENotifier`.</span><span class="sxs-lookup"><span data-stu-id="ee920-191">If you need deeper customization of your notifications(if you want for instance tooload your view directly from hello code), it is recommended tootake a look at hello provided source code and class documentation of `Protocol ReferencesDefaultNotifier` and `AENotifier`.</span></span>

<span data-ttu-id="ee920-192">Należy pamiętać, że można użyć hello tego samego zgłaszający dla wielu kategorii.</span><span class="sxs-lookup"><span data-stu-id="ee920-192">Note that you can use hello same notifier for multiple categories.</span></span>

<span data-ttu-id="ee920-193">Można również ponownie zdefiniowany hello domyślne zgłaszający następująco:</span><span class="sxs-lookup"><span data-stu-id="ee920-193">You can also redefined hello default notifier like this:</span></span>

    AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
    [reach registerNotifier:myNotifier forCategory:kAEReachDefaultCategory];

##### <a name="notification-handling"></a><span data-ttu-id="ee920-194">Obsługa powiadomień</span><span class="sxs-lookup"><span data-stu-id="ee920-194">Notification handling</span></span>
<span data-ttu-id="ee920-195">Korzystając z kategorii domyślnej hello, w przypadku niektórych metod cyklu życia są nazywane na powitania `AEReachContent` obiekt tooreport statystyk i aktualizacji hello kampanii stanu:</span><span class="sxs-lookup"><span data-stu-id="ee920-195">When using hello default category, some life cycle methods are called on hello `AEReachContent` object tooreport statistics and update hello campaign state:</span></span>

* <span data-ttu-id="ee920-196">Po wyświetleniu powiadomienia hello w aplikacji hello `displayNotification` metoda jest wywoływana (która statystyki) przez `AEReachModule` Jeśli `handleNotification:` zwraca `YES`.</span><span class="sxs-lookup"><span data-stu-id="ee920-196">When hello notification is displayed in application, hello `displayNotification` method is called (which reports statistics) by `AEReachModule` if `handleNotification:` returns `YES`.</span></span>
* <span data-ttu-id="ee920-197">Jeśli powiadomienia hello jest odrzucane, hello `exitNotification` metoda jest wywoływana, statystyka jest zgłaszany i dalej kampanii teraz mogą być przetwarzane.</span><span class="sxs-lookup"><span data-stu-id="ee920-197">If hello notification is dismissed, hello `exitNotification` method is called, statistic is reported and next campaigns can now be processed.</span></span>
* <span data-ttu-id="ee920-198">Po kliknięciu hello powiadomień `actionNotification` jest wywoływana, statystyka jest zgłaszany i hello skojarzona akcja jest wykonywana.</span><span class="sxs-lookup"><span data-stu-id="ee920-198">If hello notification is clicked, `actionNotification` is called, statistic is reported and hello associated action is performed.</span></span>

<span data-ttu-id="ee920-199">Jeśli implementacji `AENotifier` pomija hello domyślne zachowanie, należy toocall tych metod cyklu życia samodzielnie.</span><span class="sxs-lookup"><span data-stu-id="ee920-199">If your implementation of `AENotifier` bypasses hello default behavior, you have toocall these life cycle methods by yourself.</span></span> <span data-ttu-id="ee920-200">Hello następujące przykłady przedstawiają niektórych przypadkach, gdy pomijana jest hello domyślne zachowanie:</span><span class="sxs-lookup"><span data-stu-id="ee920-200">hello following examples illustrate some cases where hello default behavior is bypassed:</span></span>

* <span data-ttu-id="ee920-201">Nie można rozszerzyć `AEDefaultNotifier`, np. zaimplementowano obsługi kategorii od początku.</span><span class="sxs-lookup"><span data-stu-id="ee920-201">You don't extend `AEDefaultNotifier`, e.g. you implemented category handling from scratch.</span></span>
* <span data-ttu-id="ee920-202">Możesz overrode `prepareNotificationView:forContent:`, toomap się, że co najmniej `onNotificationActioned` lub `onNotificationExited` tooone formantów U.I.</span><span class="sxs-lookup"><span data-stu-id="ee920-202">You overrode `prepareNotificationView:forContent:`, be sure toomap at least `onNotificationActioned` or `onNotificationExited` tooone of your U.I controls.</span></span>

> [!WARNING]
> <span data-ttu-id="ee920-203">Jeśli `handleNotification:` zwraca wyjątek, hello zawartości zostanie usunięty i `drop` jest wywoływana, jest to raportowane w statystykach i dalej kampanii teraz mogą być przetwarzane.</span><span class="sxs-lookup"><span data-stu-id="ee920-203">If `handleNotification:` throws an exception, hello content is deleted and `drop` is called, this is reported in statistics and next campaigns can now be processed.</span></span>
>
>

#### <a name="include-notification-as-part-of-an-existing-view"></a><span data-ttu-id="ee920-204">Powiadomienia jako część istniejącego widoku</span><span class="sxs-lookup"><span data-stu-id="ee920-204">Include notification as part of an existing view</span></span>
<span data-ttu-id="ee920-205">Nakładki są bardzo szybkiego integracji, ale może nie może być czasami wygodne lub może mieć niepożądane skutki uboczne.</span><span class="sxs-lookup"><span data-stu-id="ee920-205">Overlays are great for a fast integration but can be sometimes not convenient, or can have unwanted side effects.</span></span>

<span data-ttu-id="ee920-206">Jeśli użytkownik nie ma spełnia Twoje wymagania systemu nakładki hello w niektórych widoków, można dostosować go do tych widoków.</span><span class="sxs-lookup"><span data-stu-id="ee920-206">If you're not satisfied with hello overlay system in some of your views, you can customize it for these views.</span></span>

<span data-ttu-id="ee920-207">Można zdecydować, tooinclude naszych układu powiadomień w istniejących widoków.</span><span class="sxs-lookup"><span data-stu-id="ee920-207">You can decide tooinclude our notification layout in your existing views.</span></span> <span data-ttu-id="ee920-208">toodo tak, brak dwa style implementacji:</span><span class="sxs-lookup"><span data-stu-id="ee920-208">toodo so, there is two implementation styles:</span></span>

1. <span data-ttu-id="ee920-209">Dodaj widok powiadomienia hello przy użyciu narzędzia Konstruktor interfejsu</span><span class="sxs-lookup"><span data-stu-id="ee920-209">Add hello notification view using interface builder</span></span>

   * <span data-ttu-id="ee920-210">Otwórz *interfejsu konstruktora*</span><span class="sxs-lookup"><span data-stu-id="ee920-210">Open *Interface Builder*</span></span>
   * <span data-ttu-id="ee920-211">Umieść 320 x 60 (lub jeśli iPad 768 x 60) `UIView` miejscu hello tooappear powiadomień</span><span class="sxs-lookup"><span data-stu-id="ee920-211">Place a 320x60 (or 768x60 if you are on iPad) `UIView` where you want hello notification tooappear</span></span>
   * <span data-ttu-id="ee920-212">Ustaw wartość tagu powitania dla tego widoku zbyt: **36822491**</span><span class="sxs-lookup"><span data-stu-id="ee920-212">Set hello Tag value for this view too: **36822491**</span></span>
2. <span data-ttu-id="ee920-213">Dodaj widok powiadomienia hello programowo.</span><span class="sxs-lookup"><span data-stu-id="ee920-213">Add hello notification view programmatically.</span></span> <span data-ttu-id="ee920-214">Po prostu Dodaj hello następującego kodu po zainicjowaniu widoku:</span><span class="sxs-lookup"><span data-stu-id="ee920-214">Just add hello following code when your view has been initialized:</span></span>

       UIView* notificationView = [[UIView alloc] initWithFrame:CGRectMake(0, 0, 320, 60)]; //Replace x and y coordinate values tooyour needs.
       notificationView.tag = NOTIFICATION_AREA_VIEW_TAG;
       [self.view addSubview:notificationView];

<span data-ttu-id="ee920-215">`NOTIFICATION_AREA_VIEW_TAG`Makro można znaleźć w `AEDefaultNotifier.h`.</span><span class="sxs-lookup"><span data-stu-id="ee920-215">`NOTIFICATION_AREA_VIEW_TAG` macro can be found in `AEDefaultNotifier.h`.</span></span>

> [!NOTE]
> <span data-ttu-id="ee920-216">zgłaszający domyślne Hello automatycznie wykrywa taki układ powiadomień hello znajduje się w tym widoku i nie dodają nakładki dla niego.</span><span class="sxs-lookup"><span data-stu-id="ee920-216">hello default notifier automatically detects that hello notification layout is included in this view and will not add an overlay for it.</span></span>
>
>

### <a name="announcements-and-polls"></a><span data-ttu-id="ee920-217">Anonsów i sond</span><span class="sxs-lookup"><span data-stu-id="ee920-217">Announcements and polls</span></span>
#### <a name="layouts"></a><span data-ttu-id="ee920-218">Układy</span><span class="sxs-lookup"><span data-stu-id="ee920-218">Layouts</span></span>
<span data-ttu-id="ee920-219">Można zmodyfikować plików hello `AEDefaultAnnouncementView.xib` i `AEDefaultPollView.xib` tak długo, jak zabezpieczyć hello wartości tagów i typy widoków istniejących podrzędnych hello.</span><span class="sxs-lookup"><span data-stu-id="ee920-219">You can modify hello files `AEDefaultAnnouncementView.xib` and `AEDefaultPollView.xib` as long as you keep hello tag values and types of hello existing subviews.</span></span>

#### <a name="categories"></a><span data-ttu-id="ee920-220">Kategorie</span><span class="sxs-lookup"><span data-stu-id="ee920-220">Categories</span></span>
##### <a name="alternate-layouts"></a><span data-ttu-id="ee920-221">Układy alternatywnej</span><span class="sxs-lookup"><span data-stu-id="ee920-221">Alternate layouts</span></span>
<span data-ttu-id="ee920-222">Jak powiadomienia Kategoria kampanii hello mogą być używane toohave alternatywne układy anonsów i sond.</span><span class="sxs-lookup"><span data-stu-id="ee920-222">Like notifications, hello campaign's category can be used toohave alternate layouts for your announcements and polls.</span></span>

<span data-ttu-id="ee920-223">toocreate kategorii anonsu, należy rozszerzyć **AEAnnouncementViewController** i zarejestruj go po zainicjowaniu moduł reach hello:</span><span class="sxs-lookup"><span data-stu-id="ee920-223">toocreate a category for an announcement, you must extend **AEAnnouncementViewController** and register it once hello reach module has been initialized:</span></span>

    AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
    [reach registerAnnouncementController:[MyCustomAnnouncementViewController class] forCategory:@"my_category"];

> [!NOTE]
> <span data-ttu-id="ee920-224">Każdym razem, użytkownik będzie kliknij powiadomienie anonsu z kategorią hello "Mój\_kategorii", kontroler widoku zarejestrowane (w takim przypadku `MyCustomAnnouncementViewController`) zostanie zainicjowana przez wywołanie metody hello `initWithAnnouncement:` i widok hello będzie Dodano toohello bieżące okno aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ee920-224">Each time a user will click on a notification for an announcement with hello category "my\_category", your registered view controller (in that case `MyCustomAnnouncementViewController`) will be initialized by calling hello method `initWithAnnouncement:` and hello view will be added toohello current application window.</span></span>
>
>

<span data-ttu-id="ee920-225">W implementacji hello `AEAnnouncementViewController` klasy mają właściwość hello tooread `announcement` tooinitialize Twojego widoków podrzędnych.</span><span class="sxs-lookup"><span data-stu-id="ee920-225">In your implementation of hello `AEAnnouncementViewController` class you will have tooread hello property `announcement` tooinitialize your subviews.</span></span> <span data-ttu-id="ee920-226">Rozważ przykład Witaj poniżej, w przypadku, gdy dwie etykiety są inicjowane przy użyciu `title` i `body` właściwości hello `AEReachAnnouncement` klasy:</span><span class="sxs-lookup"><span data-stu-id="ee920-226">Consider hello example below, where two labels are initialized using `title` and `body` properties of hello `AEReachAnnouncement` class:</span></span>

    -(void)loadView
    {
        [super loadView];

        UILabel* titleLabel = [[UILabel alloc] initWithFrame:CGRectMake(10, 20, 300, 60)];
        titleLabel.font = [UIFont systemFontOfSize:32.0];
        titleLabel.text = self.announcement.title;

        UILabel* bodyLabel = [[UILabel alloc] initWithFrame:CGRectMake(10, 20, 300, 60)];
        bodyLabel.font = [UIFont systemFontOfSize:24.0];
        bodyLabel.text = self.announcement.body;

        [self.view addSubview:titleLabel];
        [self.view addSubview:bodyLabel];
    }

<span data-ttu-id="ee920-227">Jeśli nie chcesz tooload widoków samodzielnie, ale chcesz tooreuse hello domyślny anonsu widoku Układ, po prostu ułatwia kontroler niestandardowy widok rozszerza klasę hello podane `AEDefaultAnnouncementViewController`.</span><span class="sxs-lookup"><span data-stu-id="ee920-227">If you don't want tooload your views by yourself but you just want tooreuse hello default announcement view layout, you can simply make your custom view controller extends hello provided class `AEDefaultAnnouncementViewController`.</span></span> <span data-ttu-id="ee920-228">W takim przypadku zduplikowane hello nib pliku `AEDefaultAnnouncementView.xib` i zmień jego nazwę, dlatego może być załadowany przez kontroler niestandardowy widok (dla kontrolera o nazwie `CustomAnnouncementViewController`, należy wywołać pliku nib `CustomAnnouncementView.xib`).</span><span class="sxs-lookup"><span data-stu-id="ee920-228">In that case, duplicate hello nib file `AEDefaultAnnouncementView.xib` and rename it so it can be loaded by your custom view controller (for a controller named `CustomAnnouncementViewController`, you should call your nib file `CustomAnnouncementView.xib`).</span></span>

<span data-ttu-id="ee920-229">tooreplace hello domyślnej kategorii anonsów, po prostu zarejestrować Kontroler Widok niestandardowy kategorii hello zdefiniowane w `kAEReachDefaultCategory`:</span><span class="sxs-lookup"><span data-stu-id="ee920-229">tooreplace hello default category of announcements, simply register your custom view controller for hello category defined in `kAEReachDefaultCategory`:</span></span>

    [reach registerAnnouncementController:[MyCustomAnnouncementViewController class] forCategory:kAEReachDefaultCategory];

<span data-ttu-id="ee920-230">Ankiety może być dostosowane hello taki sam sposób:</span><span class="sxs-lookup"><span data-stu-id="ee920-230">Polls can be customized hello same way :</span></span>

    AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
    [reach registerPollController:[MyCustomPollViewController class] forCategory:@"my_category"];

<span data-ttu-id="ee920-231">Ten czas, podany hello `MyCustomPollViewController` muszą być rozszerzane `AEPollViewController`.</span><span class="sxs-lookup"><span data-stu-id="ee920-231">This time, hello provided `MyCustomPollViewController` must extend `AEPollViewController`.</span></span> <span data-ttu-id="ee920-232">Lub możesz wybrać tooextend hello domyślnego kontrolera: `AEDefaultPollViewController`.</span><span class="sxs-lookup"><span data-stu-id="ee920-232">Or you can choose tooextend from hello default controller: `AEDefaultPollViewController`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ee920-233">Nie zapomnij toocall albo `action` (`submitAnswers:` kontrolerów widok niestandardowy sondowania) lub `exit` metoda przed kontrolera widoku hello jest odrzucane.</span><span class="sxs-lookup"><span data-stu-id="ee920-233">Don't forget toocall either `action` (`submitAnswers:` for custom poll view controllers) or `exit` method before hello view controller is dismissed.</span></span> <span data-ttu-id="ee920-234">W przeciwnym razie statystyki nie zostaną wysłane (tzn. nie analizy kampanii hello) i więcej kampanii istotne dalej nie zostaną powiadomieni do ponownego uruchomienia procesu aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="ee920-234">Otherwise, statistics won't be sent (i.e. no analytics on hello campaign) and more importantly next campaigns will not be notified until hello application process is restarted.</span></span>
>
>

##### <a name="implementation-example"></a><span data-ttu-id="ee920-235">Przykład wdrożenia</span><span class="sxs-lookup"><span data-stu-id="ee920-235">Implementation example</span></span>
<span data-ttu-id="ee920-236">W tej implementacji widok niestandardowy anonsu hello są ładowane z pliku xib zewnętrznych.</span><span class="sxs-lookup"><span data-stu-id="ee920-236">In this implementation hello custom announcement view is loaded from an external xib file.</span></span>

<span data-ttu-id="ee920-237">Podobnie jak dostosowywania powiadomień zaawansowane, zalecane jest toolook na kod źródłowy hello hello standardowej implementacji.</span><span class="sxs-lookup"><span data-stu-id="ee920-237">Like for advanced notification customization, it is recommended toolook at hello source code of hello standard implementation.</span></span>

`CustomAnnouncementViewController.h`

    //Interface
    @interface CustomAnnouncementViewController : AEAnnouncementViewController {
      UILabel* titleLabel;
      UITextView* descTextView;
      UIWebView* htmlWebView;
      UIButton* okButton;
      UIButton* cancelButton;
    }

    @property (nonatomic, retain) IBOutlet UILabel* titleLabel;
    @property (nonatomic, retain) IBOutlet UITextView* descTextView;
    @property (nonatomic, retain) IBOutlet UIWebView* htmlWebView;
    @property (nonatomic, retain) IBOutlet UIButton* okButton;
    @property (nonatomic, retain) IBOutlet UIButton* cancelButton;

    -(IBAction)okButtonClicked:(id)sender;
    -(IBAction)cancelButtonClicked:(id)sender;

`CustomAnnouncementViewController.m`

    //Implementation
    @implementation CustomAnnouncementViewController
    @synthesize titleLabel;
    @synthesize descTextView;
    @synthesize htmlWebView;
    @synthesize okButton;
    @synthesize cancelButton;

    -(id)initWithAnnouncement:(AEReachAnnouncement*)anAnnouncement
    {
      self = [super initWithNibName:@"CustomAnnouncementViewController" bundle:nil];
      if (self != nil) {
        self.announcement = anAnnouncement;
      }
      return self;
    }

    - (void) dealloc
    {
      [titleLabel release];
      [descTextView release];
      [htmlWebView release];
      [okButton release];
      [cancelButton release];
      [super dealloc];
    }

    - (void)viewDidLoad {
      [super viewDidLoad];

      /* Init announcement title */
      titleLabel.text = self.announcement.title;

      /* Init announcement body */
      if(self.announcement.type == AEAnnouncementTypeHtml)
      {
        titleLabel.hidden = YES;
        htmlWebView.hidden = NO;
        [htmlWebView loadHTMLString:self.announcement.body baseURL:[NSURL URLWithString:@"http://localhost/"]];
      }
      else
      {
        titleLabel.hidden = NO;
        htmlWebView.hidden = YES;
        descTextView.text = self.announcement.body;
      }

      /* Set action button label */
      if([self.announcement.actionLabel length] > 0)
        [okButton setTitle:self.announcement.actionLabel forState:UIControlStateNormal];

      /* Set exit button label */
      if([self.announcement.exitLabel length] > 0)
        [cancelButton setTitle:self.announcement.exitLabel forState:UIControlStateNormal];
    }

    #pragma mark Actions

    -(IBAction)okButtonClicked:(id)sender
    {
        [self action];
    }

    -(IBAction)cancelButtonClicked:(id)sender
    {
        [self exit];
    }

    @end
