---
title: "Azure Mobile Engagement iOS SDK Integration osiągnąć | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: ba74e0c442ac10f096d465f989e03d2ceae8cd88
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-integrate-engagement-reach-on-ios"></a><span data-ttu-id="675b1-103">Jak zintegrować Reach usługi Engagement w systemie iOS</span><span class="sxs-lookup"><span data-stu-id="675b1-103">How to Integrate Engagement Reach on iOS</span></span>
<span data-ttu-id="675b1-104">Należy wykonać procedury integracji opisane w sekcji [jak zintegrować zaangażowania w dokumencie iOS](mobile-engagement-ios-integrate-engagement.md) przed wykonaniem tego przewodnika.</span><span class="sxs-lookup"><span data-stu-id="675b1-104">You must follow the integration procedure described in the [How to Integrate Engagement on iOS document](mobile-engagement-ios-integrate-engagement.md) before following this guide.</span></span>

<span data-ttu-id="675b1-105">Ta dokumentacja wymaga XCode 8.</span><span class="sxs-lookup"><span data-stu-id="675b1-105">This documentation requires XCode 8.</span></span> <span data-ttu-id="675b1-106">Jeśli naprawdę są zależne od XCode 7, możesz użyć [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh).</span><span class="sxs-lookup"><span data-stu-id="675b1-106">If you really depend on XCode 7 then you may use the [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh).</span></span> <span data-ttu-id="675b1-107">Jest znaną usterką w poprzedniej podczas uruchamiania na urządzeniach z systemem iOS 10: powiadomień systemowych nie są których wykonano akcje.</span><span class="sxs-lookup"><span data-stu-id="675b1-107">There is a known bug on this previous version while running on iOS 10 devices:  system notifications are not actioned.</span></span> <span data-ttu-id="675b1-108">Rozwiązać problem, należy zaimplementować przestarzałe interfejsu API `application:didReceiveRemoteNotification:` w aplikacji delegowanie w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="675b1-108">To fix this you will have to implement the deprecated API `application:didReceiveRemoteNotification:` in your app delegate as follows:</span></span>

    - (void)application:(UIApplication*)application
    didReceiveRemoteNotification:(NSDictionary*)userInfo
    {
        [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:nil];
    }

> [!IMPORTANT]
> <span data-ttu-id="675b1-109">**Nie zaleca się rozwiązanie** jak to zachowanie można zmienić w jakiegokolwiek uaktualnienia wersji nadchodzących iOS (nawet pomocnicze), ponieważ ten iOS interfejsu API jest przestarzały.</span><span class="sxs-lookup"><span data-stu-id="675b1-109">**We do not recommend this workaround** as this behavior can change in any upcoming (even minor) iOS version upgrade because this iOS API is deprecated.</span></span> <span data-ttu-id="675b1-110">Powinna przebiegać XCode 8 tak szybko, jak to możliwe.</span><span class="sxs-lookup"><span data-stu-id="675b1-110">You should switch to XCode 8 as soon as possible.</span></span>
>
>

### <a name="enable-your-app-to-receive-silent-push-notifications"></a><span data-ttu-id="675b1-111">Umożliwianie aplikacji otrzymywania cichych powiadomień wypychanych</span><span class="sxs-lookup"><span data-stu-id="675b1-111">Enable your app to receive Silent Push Notifications</span></span>
[!INCLUDE [mobile-engagement-ios-silent-push](../../includes/mobile-engagement-ios-silent-push.md)]

## <a name="integration-steps"></a><span data-ttu-id="675b1-112">Kroki integracji</span><span class="sxs-lookup"><span data-stu-id="675b1-112">Integration steps</span></span>
### <a name="embed-the-engagement-reach-sdk-into-your-ios-project"></a><span data-ttu-id="675b1-113">Osadź SDK Reach usługi Engagement do projektu systemu iOS</span><span class="sxs-lookup"><span data-stu-id="675b1-113">Embed the Engagement Reach SDK into your iOS project</span></span>
* <span data-ttu-id="675b1-114">Dodawanie zestawu sdk modułu Reach do projektu Xcode.</span><span class="sxs-lookup"><span data-stu-id="675b1-114">Add the Reach sdk in your Xcode project.</span></span> <span data-ttu-id="675b1-115">W środowisku Xcode przejdź do **projektu \> Dodaj do projektu** i wybierz polecenie `EngagementReach` folderu.</span><span class="sxs-lookup"><span data-stu-id="675b1-115">In Xcode, go to **Project \> Add to project** and choose the `EngagementReach` folder.</span></span>

### <a name="modify-your-application-delegate"></a><span data-ttu-id="675b1-116">Modyfikowanie delegata aplikacji</span><span class="sxs-lookup"><span data-stu-id="675b1-116">Modify your Application Delegate</span></span>
* <span data-ttu-id="675b1-117">W górnej części pliku implementacji Zaimportuj moduł Reach usługi Engagement:</span><span class="sxs-lookup"><span data-stu-id="675b1-117">At the top of your implementation file, import the Engagement Reach module:</span></span>

      [...]
      #import "AEReachModule.h"
* <span data-ttu-id="675b1-118">Wewnątrz metody `applicationDidFinishLaunching:` lub `application:didFinishLaunchingWithOptions:`, Utwórz moduł reach i przekaż go do Twojego istniejącego wiersza inicjowania usługi Engagement:</span><span class="sxs-lookup"><span data-stu-id="675b1-118">Inside method `applicationDidFinishLaunching:` or `application:didFinishLaunchingWithOptions:`, create a reach module and pass it to your existing Engagement initialization line:</span></span>

      - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
        AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
        [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}" modules:reach, nil];
        [...]

        return YES;
      }
* <span data-ttu-id="675b1-119">Modyfikowanie **"icon.png"** ciąg zawierający nazwę obrazu jako ikonę powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="675b1-119">Modify **'icon.png'** string with the image name you want as your notification icon.</span></span>
* <span data-ttu-id="675b1-120">Jeśli chcesz użyć opcji *wartość wskaźnika aktualizacji* kampanie Zasięgowe lub jeśli chcesz użyć natywnych powiadomień wypychanych \<SaaS/Reach interfejsu API/kampanii format/Native Push\> kampanie, należy umożliwić moduł Reach Zarządzanie wskaźnika Ikona sam (zostanie automatycznie usunięty wskaźnika aplikacji i również zresetować do wartości przechowywanej przez zaangażowania za każdym razem, gdy aplikacja jest uruchomiona lub foregrounded).</span><span class="sxs-lookup"><span data-stu-id="675b1-120">If you want to use the option *Update badge value* in Reach campaigns or if you want to use native push \</SaaS/Reach API/Campaign format/Native Push\> campaigns, you must let the Reach module manage the badge icon itself (it will automatically clear the application badge and also reset the value stored by Engagement every time the application is started or foregrounded).</span></span> <span data-ttu-id="675b1-121">Można to zrobić, dodając następujący wiersz po zainicjowaniu modułu Reach:</span><span class="sxs-lookup"><span data-stu-id="675b1-121">This is done by adding the following line after Reach module initialization:</span></span>

      [reach setAutoBadgeEnabled:YES];
* <span data-ttu-id="675b1-122">Jeśli chcesz obsługiwać Reach wypychanie danych, należy przeprowadzić delegata aplikacji jest zgodny ze `AEReachDataPushDelegate` protokołu.</span><span class="sxs-lookup"><span data-stu-id="675b1-122">If you want to handle Reach data push, you must let your Application delegate conform to the `AEReachDataPushDelegate` protocol.</span></span> <span data-ttu-id="675b1-123">Dodaj następujący wiersz po zainicjowaniu modułu Reach:</span><span class="sxs-lookup"><span data-stu-id="675b1-123">Add the following line after Reach module initialization:</span></span>

      [reach setDataPushDelegate:self];
* <span data-ttu-id="675b1-124">Następnie można zaimplementować metody `onDataPushStringReceived:` i `onDataPushBase64ReceivedWithDecodedBody:andEncodedBody:` w delegata aplikacji:</span><span class="sxs-lookup"><span data-stu-id="675b1-124">Then you can implement the methods `onDataPushStringReceived:` and `onDataPushBase64ReceivedWithDecodedBody:andEncodedBody:` in your application delegate:</span></span>

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

### <a name="category"></a><span data-ttu-id="675b1-125">Kategoria</span><span class="sxs-lookup"><span data-stu-id="675b1-125">Category</span></span>
<span data-ttu-id="675b1-126">Parametr kategorii jest opcjonalny, podczas tworzenia kampanii wypychania danych i umożliwia Wypychanie do filtrowania danych.</span><span class="sxs-lookup"><span data-stu-id="675b1-126">The category parameter is optional when you create a Data Push campaign and allows you to filter data pushes.</span></span> <span data-ttu-id="675b1-127">Jest to przydatne, jeśli chcesz dystrybuować różnych rodzajów z `Base64` danych, aby zidentyfikować ich typu przed ich analizowania.</span><span class="sxs-lookup"><span data-stu-id="675b1-127">This is useful if you want to push different kinds of `Base64` data and want to identify their type before parsing them.</span></span>

<span data-ttu-id="675b1-128">**Aplikacja jest teraz gotowa do odbierania i wyświetlić zawartość reach!**</span><span class="sxs-lookup"><span data-stu-id="675b1-128">**Your application is now ready to receive and display reach contents!**</span></span>

## <a name="how-to-receive-announcements-and-polls-at-any-time"></a><span data-ttu-id="675b1-129">Jak odbierać anonsów i sond w dowolnym momencie</span><span class="sxs-lookup"><span data-stu-id="675b1-129">How to receive announcements and polls at any time</span></span>
<span data-ttu-id="675b1-130">Zaangażowania można wysłać powiadomienia o zasięgu użytkownikom końcowym w dowolnej chwili za pomocą usługi Apple Push Notification Service.</span><span class="sxs-lookup"><span data-stu-id="675b1-130">Engagement can send Reach notifications to your end users at any time by using the Apple Push Notification Service.</span></span>

<span data-ttu-id="675b1-131">Aby włączyć tę funkcję, musisz przygotować aplikacji dla powiadomień wypychanych firmy Apple i modyfikowanie delegata aplikacji.</span><span class="sxs-lookup"><span data-stu-id="675b1-131">To enable this functionality, you'll have to prepare your application for Apple push notifications and modify your application delegate.</span></span>

### <a name="prepare-your-application-for-apple-push-notifications"></a><span data-ttu-id="675b1-132">Przygotowanie aplikacji dla powiadomień wypychanych firmy Apple</span><span class="sxs-lookup"><span data-stu-id="675b1-132">Prepare your application for Apple push notifications</span></span>
<span data-ttu-id="675b1-133">Wykonaj przewodnik: [sposobu przygotowania aplikacji do powiadomień wypychanych firmy Apple](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html#//apple_ref/doc/uid/TP40012582-CH26-SW6)</span><span class="sxs-lookup"><span data-stu-id="675b1-133">Please follow the guide : [How to Prepare your Application for Apple Push Notifications](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html#//apple_ref/doc/uid/TP40012582-CH26-SW6)</span></span>

### <a name="add-the-necessary-client-code"></a><span data-ttu-id="675b1-134">Dodaj kod niezbędne klienta</span><span class="sxs-lookup"><span data-stu-id="675b1-134">Add the necessary client code</span></span>
<span data-ttu-id="675b1-135">*W tym momencie aplikacji powinien mieć zarejestrowany certyfikat usługi Apple push frontonu zaangażowania.*</span><span class="sxs-lookup"><span data-stu-id="675b1-135">*At this point your application should have a registered Apple push certificate in the Engagement frontend.*</span></span>

<span data-ttu-id="675b1-136">Jeśli nie jest jeszcze zrobione, należy zarejestrować aplikację w taki sposób, aby odbierać powiadomienia wypychane.</span><span class="sxs-lookup"><span data-stu-id="675b1-136">If it's not done already, you need to register your application to receive push notifications.</span></span>

* <span data-ttu-id="675b1-137">Importuj `User Notification` framework:</span><span class="sxs-lookup"><span data-stu-id="675b1-137">Import the `User Notification` framework:</span></span>

        #import <UserNotifications/UserNotifications.h>
* <span data-ttu-id="675b1-138">Dodaj następujący wiersz po uruchomieniu aplikacji (zwykle w `application:didFinishLaunchingWithOptions:`):</span><span class="sxs-lookup"><span data-stu-id="675b1-138">Add the following line when your application starts (typically in `application:didFinishLaunchingWithOptions:`):</span></span>

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

<span data-ttu-id="675b1-139">Następnie musisz podać do zaangażowania token urządzenia zwrócony przez serwery firmy Apple.</span><span class="sxs-lookup"><span data-stu-id="675b1-139">Then, You need to provide to Engagement the device token returned by Apple servers.</span></span> <span data-ttu-id="675b1-140">Jest to wykonywane w metodę o nazwie `application:didRegisterForRemoteNotificationsWithDeviceToken:` w delegata aplikacji:</span><span class="sxs-lookup"><span data-stu-id="675b1-140">This is done in the method named `application:didRegisterForRemoteNotificationsWithDeviceToken:` in your application delegate:</span></span>

    - (void)application:(UIApplication*)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData*)deviceToken
    {
        [[EngagementAgent shared] registerDeviceToken:deviceToken];
    }

<span data-ttu-id="675b1-141">Na koniec należy poinformować Engagement SDK, gdy aplikacja otrzyma powiadomienie zdalnego.</span><span class="sxs-lookup"><span data-stu-id="675b1-141">Finally, you have to inform the Engagement SDK when your application receives a remote notification.</span></span> <span data-ttu-id="675b1-142">Aby to zrobić, należy wywołać metodę `applicationDidReceiveRemoteNotification:fetchCompletionHandler:` w delegata aplikacji:</span><span class="sxs-lookup"><span data-stu-id="675b1-142">To do that, call the method `applicationDidReceiveRemoteNotification:fetchCompletionHandler:` in your application delegate:</span></span>

    - (void)application:(UIApplication*)application didReceiveRemoteNotification:(NSDictionary*)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult result))handler
    {
        [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:handler];
    }

> [!IMPORTANT]
> <span data-ttu-id="675b1-143">Domyślnie Reach usługi Engagement steruje completionHandler.</span><span class="sxs-lookup"><span data-stu-id="675b1-143">By default, Engagement Reach controls the completionHandler.</span></span> <span data-ttu-id="675b1-144">Jeśli chcesz ręcznie odpowiadanie na `handler` bloków w kodzie, można przekazać nil `handler` argumentu i kontroli zakończenia zablokować samodzielnie.</span><span class="sxs-lookup"><span data-stu-id="675b1-144">If you want to manually respond to the `handler` block in your code, you can pass nil for the `handler` argument and control the completion block yourself.</span></span> <span data-ttu-id="675b1-145">Zobacz `UIBackgroundFetchResult` typu listę możliwych wartości.</span><span class="sxs-lookup"><span data-stu-id="675b1-145">See the `UIBackgroundFetchResult` type for a list of possible values.</span></span>
>
>

### <a name="full-example"></a><span data-ttu-id="675b1-146">Pełny przykład</span><span class="sxs-lookup"><span data-stu-id="675b1-146">Full example</span></span>
<span data-ttu-id="675b1-147">Oto pełny przykład integracji:</span><span class="sxs-lookup"><span data-stu-id="675b1-147">Here is a full example of integration:</span></span>

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

### <a name="resolve-unusernotificationcenter-delegate-conflicts"></a><span data-ttu-id="675b1-148">Rozwiązywanie konfliktów delegata UNUserNotificationCenter</span><span class="sxs-lookup"><span data-stu-id="675b1-148">Resolve UNUserNotificationCenter delegate conflicts</span></span>

<span data-ttu-id="675b1-149">*Jeśli implementuje jednej z bibliotek innych firm ani aplikacji `UNUserNotificationCenterDelegate` , a następnie można pominąć tej części.*</span><span class="sxs-lookup"><span data-stu-id="675b1-149">*If neither your application or one of your third party libraries implements a `UNUserNotificationCenterDelegate` then you can skip this part.*</span></span>

<span data-ttu-id="675b1-150">A `UNUserNotificationCenter` delegata jest używana przez zestaw SDK do monitorowania cyklu życia zaangażowania powiadomienia na urządzeniach z systemem iOS, 10 lub nowszy.</span><span class="sxs-lookup"><span data-stu-id="675b1-150">A `UNUserNotificationCenter` delegate is used by the SDK to monitor the life cycle of Engagement notifications on devices running on iOS 10 or greater.</span></span> <span data-ttu-id="675b1-151">Zestaw SDK ma własną implementację `UNUserNotificationCenterDelegate` protokołu, ale może istnieć tylko jedna `UNUserNotificationCenter` delegować na aplikację.</span><span class="sxs-lookup"><span data-stu-id="675b1-151">The SDK has its own implementation of the `UNUserNotificationCenterDelegate` protocol but there can be only one `UNUserNotificationCenter` delegate per application.</span></span> <span data-ttu-id="675b1-152">Inne delegata dodane do `UNUserNotificationCenter` obiektu może powodować konflikt z zaangażowania, jeden.</span><span class="sxs-lookup"><span data-stu-id="675b1-152">Any other delegate added to the `UNUserNotificationCenter` object will conflict with the Engagement one.</span></span> <span data-ttu-id="675b1-153">Jeśli zestaw SDK wykryje delegata użytkownika lub dowolnej innej strony trzeciej firmy nie będzie używać własną implementację daje możliwość Rozwiąż konflikty.</span><span class="sxs-lookup"><span data-stu-id="675b1-153">If the SDK detects your or any other third party's delegate then it will not use its own implementation to give you a chance to resolve the conflicts.</span></span> <span data-ttu-id="675b1-154">Należy dodać logikę zaangażowania do własnych delegata, aby rozwiązać konflikty.</span><span class="sxs-lookup"><span data-stu-id="675b1-154">You will have to add the Engagement logic to your own delegate in order to resolve the conflicts.</span></span>

<span data-ttu-id="675b1-155">Istnieją dwa sposoby można to osiągnąć.</span><span class="sxs-lookup"><span data-stu-id="675b1-155">There are two ways to achieve this.</span></span>

<span data-ttu-id="675b1-156">Wniosek 1, po prostu przekazywania pełnomocnika wywołania do zestawu SDK:</span><span class="sxs-lookup"><span data-stu-id="675b1-156">Proposal 1, simply by forwarding your delegate calls to the SDK:</span></span>

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

<span data-ttu-id="675b1-157">Lub propozycji 2, dziedziczenie z `AEUserNotificationHandler` — klasa</span><span class="sxs-lookup"><span data-stu-id="675b1-157">Or proposal 2, by inheriting from the `AEUserNotificationHandler` class</span></span>

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
> <span data-ttu-id="675b1-158">Można określić, czy powiadomienie jest dostarczany z zaangażowania lub nie przez przekazanie jej `userInfo` słownika do agenta `isEngagementPushPayload:` metoda klasy.</span><span class="sxs-lookup"><span data-stu-id="675b1-158">You can determine whether a notification comes from Engagement or not by passing its `userInfo` dictionary to the Agent `isEngagementPushPayload:` class method.</span></span>

<span data-ttu-id="675b1-159">Upewnij się, że `UNUserNotificationCenter` obiektu delegowanego ustawiono pełnomocnika albo `application:willFinishLaunchingWithOptions:` lub `application:didFinishLaunchingWithOptions:` metody delegata aplikacji.</span><span class="sxs-lookup"><span data-stu-id="675b1-159">Make sure that the `UNUserNotificationCenter` object's delegate is set to your delegate within either the `application:willFinishLaunchingWithOptions:` or the `application:didFinishLaunchingWithOptions:` method of your application delegate.</span></span>
<span data-ttu-id="675b1-160">Na przykład jeśli zaimplementowano wniosek powyżej 1:</span><span class="sxs-lookup"><span data-stu-id="675b1-160">For instance, if you implemented the above proposal 1:</span></span>

      - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
        // Any other code

        [UNUserNotificationCenter currentNotificationCenter].delegate = self;
        return YES;
      }

## <a name="how-to-customize-campaigns"></a><span data-ttu-id="675b1-161">Dostosowywanie kampanii</span><span class="sxs-lookup"><span data-stu-id="675b1-161">How to customize campaigns</span></span>
### <a name="notifications"></a><span data-ttu-id="675b1-162">Powiadomienia</span><span class="sxs-lookup"><span data-stu-id="675b1-162">Notifications</span></span>
<span data-ttu-id="675b1-163">Istnieją dwa typy powiadomień: powiadomień systemowych i w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="675b1-163">There are two types of notifications: system and in-app notifications.</span></span>

<span data-ttu-id="675b1-164">Powiadomienia systemowe są obsługiwane przez system iOS i nie można dostosować.</span><span class="sxs-lookup"><span data-stu-id="675b1-164">System notifications are handled by iOS, and cannot be customized.</span></span>

<span data-ttu-id="675b1-165">W aplikacji zawiadomienia widoku, który jest dynamicznie dodawane do bieżącego okna aplikacji.</span><span class="sxs-lookup"><span data-stu-id="675b1-165">In-app notifications are made of a view that is dynamically added to the current application window.</span></span> <span data-ttu-id="675b1-166">Jest to nakładce powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="675b1-166">This is called a notification overlay.</span></span> <span data-ttu-id="675b1-167">Nakładki powiadomienia są bardzo szybkiego integracji, ponieważ wymagają one, nie można zmodyfikować w dowolnym widoku w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="675b1-167">Notification overlays are great for a fast integration because they does not require you to modify any view in your application.</span></span>

#### <a name="layout"></a><span data-ttu-id="675b1-168">Układ</span><span class="sxs-lookup"><span data-stu-id="675b1-168">Layout</span></span>
<span data-ttu-id="675b1-169">Aby zmodyfikować wygląd powiadomienia w aplikacji, wystarczy zmodyfikować plik `AENotificationView.xib` do własnych potrzeb, tak długo, jak zabezpieczyć wartości tagów i typy widoków istniejących podrzędnych.</span><span class="sxs-lookup"><span data-stu-id="675b1-169">To modify the look of your in-app notifications, you can simply modify the file `AENotificationView.xib` to your needs, as long as you keep the tag values and types of the existing subviews.</span></span>

<span data-ttu-id="675b1-170">Domyślnie powiadomienia w aplikacji są prezentowane w dolnej części ekranu.</span><span class="sxs-lookup"><span data-stu-id="675b1-170">By default, in-app notifications are presented at the bottom of the screen.</span></span> <span data-ttu-id="675b1-171">Jeśli chcesz je wyświetlić w górnej części ekranu, Edytuj dostarczonych `AENotificationView.xib` i zmienić `AutoSizing` właściwości widoku głównego, mogą być przechowywane w górnej części jej superview.</span><span class="sxs-lookup"><span data-stu-id="675b1-171">If you prefer to display them at the top of screen, edit the provided `AENotificationView.xib` and change the `AutoSizing` property of the main view so it can be kept at the top of its superview.</span></span>

#### <a name="categories"></a><span data-ttu-id="675b1-172">Kategorie</span><span class="sxs-lookup"><span data-stu-id="675b1-172">Categories</span></span>
<span data-ttu-id="675b1-173">Po zmodyfikowaniu układu, możesz zmodyfikować wygląd wszystkich powiadomień.</span><span class="sxs-lookup"><span data-stu-id="675b1-173">When you modify the provided layout, you modify the look of all your notifications.</span></span> <span data-ttu-id="675b1-174">Kategorie umożliwiają definiowanie różnych wygląda docelowej (prawdopodobnie zachowania) dla powiadomień.</span><span class="sxs-lookup"><span data-stu-id="675b1-174">Categories allow you to define various targeted looks (possibly behaviors) for notifications.</span></span> <span data-ttu-id="675b1-175">Po utworzeniu kampanii Reach można określić kategorię.</span><span class="sxs-lookup"><span data-stu-id="675b1-175">A category can be specified when you create a Reach campaign.</span></span> <span data-ttu-id="675b1-176">Należy pamiętać, że kategorie pozwalają również dostosować anonsów i sond, opisane w dalszej części tego dokumentu.</span><span class="sxs-lookup"><span data-stu-id="675b1-176">Keep in mind that categories also let you customize announcements and polls, that is described later in this document.</span></span>

<span data-ttu-id="675b1-177">Aby zarejestrować kategorii Obsługa powiadomienia, należy dodać wywołanie po zainicjowaniu moduł reach.</span><span class="sxs-lookup"><span data-stu-id="675b1-177">To register a category handler for your notifications, you need to add a call once the reach module is initialized.</span></span>

    AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
    [reach registerNotifier:myNotifier forCategory:@"my_category"];
    ...

<span data-ttu-id="675b1-178">`myNotifier`musi być wystąpieniem obiektu, który jest zgodny z protokołem `AENotifier`.</span><span class="sxs-lookup"><span data-stu-id="675b1-178">`myNotifier` must be an instance of an object that conforms to the protocol `AENotifier`.</span></span>

<span data-ttu-id="675b1-179">Można zaimplementować metody protokołu przez siebie lub mogą być reimplement istniejącej klasy `AEDefaultNotifier` który już wykonuje większość pracy.</span><span class="sxs-lookup"><span data-stu-id="675b1-179">You can implement the protocol methods by yourself or you can choose to reimplement the existing class `AEDefaultNotifier` which already performs most of the work.</span></span>

<span data-ttu-id="675b1-180">Na przykład jeśli chcesz zmienić definicję widoku powiadomień dla określonej kategorii, należy wykonać w tym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="675b1-180">For example, if you want to redefine the notification view for a specific category, you can follow this example:</span></span>

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

<span data-ttu-id="675b1-181">Ten prosty przykład kategorii założono, że istnieje plik o nazwie `MyNotificationView.xib` w Twojego pakietu aplikacji głównej.</span><span class="sxs-lookup"><span data-stu-id="675b1-181">This simple example of category assume that you have a file named `MyNotificationView.xib` in your main application bundle.</span></span> <span data-ttu-id="675b1-182">Jeśli metoda nie jest w stanie znaleźć odpowiadającego `.xib`, nie będą wyświetlane powiadomienia i zaangażowania dane wyjściowe obejmują komunikat w konsoli.</span><span class="sxs-lookup"><span data-stu-id="675b1-182">If the method is not able to find a corresponding `.xib`, the notification will not be displayed and Engagement will output a message in the console.</span></span>

<span data-ttu-id="675b1-183">Nib podanego pliku powinna przestrzegać następujących reguł:</span><span class="sxs-lookup"><span data-stu-id="675b1-183">The provided nib file should respect the following rules:</span></span>

* <span data-ttu-id="675b1-184">Powinna ona zawierać tylko jeden widok.</span><span class="sxs-lookup"><span data-stu-id="675b1-184">It should only contain one view.</span></span>
* <span data-ttu-id="675b1-185">Widoków podrzędnych powinny być tego samego typu, jak te w nib podany plik o nazwie`AENotificationView.xib`</span><span class="sxs-lookup"><span data-stu-id="675b1-185">Subviews should be of the same types as the ones inside the provided nib file named `AENotificationView.xib`</span></span>
* <span data-ttu-id="675b1-186">Widoków podrzędnych powinny mieć te same znaczniki, jak te w dostarczonych nib plik o nazwie`AENotificationView.xib`</span><span class="sxs-lookup"><span data-stu-id="675b1-186">Subviews should have the same tags as the ones inside the provided nib file named `AENotificationView.xib`</span></span>

> [!TIP]
> <span data-ttu-id="675b1-187">Po prostu skopiuj plik nib udostępnionego o nazwie `AENotificationView.xib`i rozpocząć pracę z tego miejsca.</span><span class="sxs-lookup"><span data-stu-id="675b1-187">Just copy the provided nib file, named `AENotificationView.xib`, and start working from there.</span></span> <span data-ttu-id="675b1-188">Jednak należy zachować ostrożność, widok wewnątrz tego pliku nib jest skojarzony z klasy `AENotificationView`.</span><span class="sxs-lookup"><span data-stu-id="675b1-188">But be careful, the view inside this nib file is associated to the class `AENotificationView`.</span></span> <span data-ttu-id="675b1-189">Ta klasa ponownie definiować metodę `layoutSubViews` na przenoszenie i zmienianie rozmiaru jego widoków podrzędnych zgodnie z kontekstu.</span><span class="sxs-lookup"><span data-stu-id="675b1-189">This class redefined the method `layoutSubViews` to move and resize its subviews according to context.</span></span> <span data-ttu-id="675b1-190">Chcesz go zastąpić `UIView` lub klasy widok niestandardowy.</span><span class="sxs-lookup"><span data-stu-id="675b1-190">You may want to replace it with an `UIView` or you custom view class.</span></span>
>
>

<span data-ttu-id="675b1-191">Jeśli potrzebujesz bardziej dostosowywania powiadomienia (Jeśli na przykład chcesz załadować widoku bezpośrednio z kodu), zaleca się Spójrz na źródła podany kod i klasy w dokumentacji `Protocol ReferencesDefaultNotifier` i `AENotifier`.</span><span class="sxs-lookup"><span data-stu-id="675b1-191">If you need deeper customization of your notifications(if you want for instance to load your view directly from the code), it is recommended to take a look at the provided source code and class documentation of `Protocol ReferencesDefaultNotifier` and `AENotifier`.</span></span>

<span data-ttu-id="675b1-192">Pamiętaj, że można używać tego samego zgłaszający dla wielu kategorii.</span><span class="sxs-lookup"><span data-stu-id="675b1-192">Note that you can use the same notifier for multiple categories.</span></span>

<span data-ttu-id="675b1-193">Można również ponownie zdefiniować zgłaszający domyślne następująco:</span><span class="sxs-lookup"><span data-stu-id="675b1-193">You can also redefined the default notifier like this:</span></span>

    AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
    [reach registerNotifier:myNotifier forCategory:kAEReachDefaultCategory];

##### <a name="notification-handling"></a><span data-ttu-id="675b1-194">Obsługa powiadomień</span><span class="sxs-lookup"><span data-stu-id="675b1-194">Notification handling</span></span>
<span data-ttu-id="675b1-195">Podczas korzystania z domyślnej kategorii, w przypadku niektórych metod cyklu życia są nazywane na `AEReachContent` obiektu do raportu statystyk i zaktualizować stan kampanii:</span><span class="sxs-lookup"><span data-stu-id="675b1-195">When using the default category, some life cycle methods are called on the `AEReachContent` object to report statistics and update the campaign state:</span></span>

* <span data-ttu-id="675b1-196">Gdy zostanie wyświetlone powiadomienie w aplikacji, `displayNotification` metoda jest wywoływana (która statystyki) przez `AEReachModule` Jeśli `handleNotification:` zwraca `YES`.</span><span class="sxs-lookup"><span data-stu-id="675b1-196">When the notification is displayed in application, the `displayNotification` method is called (which reports statistics) by `AEReachModule` if `handleNotification:` returns `YES`.</span></span>
* <span data-ttu-id="675b1-197">Jeśli powiadomienie jest odrzucane, `exitNotification` metoda jest wywoływana, statystyka jest zgłaszany i dalej kampanii teraz mogą być przetwarzane.</span><span class="sxs-lookup"><span data-stu-id="675b1-197">If the notification is dismissed, the `exitNotification` method is called, statistic is reported and next campaigns can now be processed.</span></span>
* <span data-ttu-id="675b1-198">Po kliknięciu powiadomienia `actionNotification` jest wywoływana, statystyka zostaje zgłoszone i skojarzona akcja jest wykonywana.</span><span class="sxs-lookup"><span data-stu-id="675b1-198">If the notification is clicked, `actionNotification` is called, statistic is reported and the associated action is performed.</span></span>

<span data-ttu-id="675b1-199">Jeśli implementacji `AENotifier` pomija domyślne zachowanie, należy wywołać metody te cyklu życia samodzielnie.</span><span class="sxs-lookup"><span data-stu-id="675b1-199">If your implementation of `AENotifier` bypasses the default behavior, you have to call these life cycle methods by yourself.</span></span> <span data-ttu-id="675b1-200">Poniższe przykłady przedstawiają w niektórych przypadkach, gdy pomijane jest domyślne zachowanie:</span><span class="sxs-lookup"><span data-stu-id="675b1-200">The following examples illustrate some cases where the default behavior is bypassed:</span></span>

* <span data-ttu-id="675b1-201">Nie można rozszerzyć `AEDefaultNotifier`, np. zaimplementowano obsługi kategorii od początku.</span><span class="sxs-lookup"><span data-stu-id="675b1-201">You don't extend `AEDefaultNotifier`, e.g. you implemented category handling from scratch.</span></span>
* <span data-ttu-id="675b1-202">Możesz overrode `prepareNotificationView:forContent:`, pamiętaj zamapować co najmniej `onNotificationActioned` lub `onNotificationExited` do jednego z U.I kontrolki.</span><span class="sxs-lookup"><span data-stu-id="675b1-202">You overrode `prepareNotificationView:forContent:`, be sure to map at least `onNotificationActioned` or `onNotificationExited` to one of your U.I controls.</span></span>

> [!WARNING]
> <span data-ttu-id="675b1-203">Jeśli `handleNotification:` zgłasza wyjątek, zawartość zostanie usunięta i `drop` jest wywoływana, jest to raportowane w statystykach i dalej kampanii teraz mogą być przetwarzane.</span><span class="sxs-lookup"><span data-stu-id="675b1-203">If `handleNotification:` throws an exception, the content is deleted and `drop` is called, this is reported in statistics and next campaigns can now be processed.</span></span>
>
>

#### <a name="include-notification-as-part-of-an-existing-view"></a><span data-ttu-id="675b1-204">Powiadomienia jako część istniejącego widoku</span><span class="sxs-lookup"><span data-stu-id="675b1-204">Include notification as part of an existing view</span></span>
<span data-ttu-id="675b1-205">Nakładki są bardzo szybkiego integracji, ale może nie może być czasami wygodne lub może mieć niepożądane skutki uboczne.</span><span class="sxs-lookup"><span data-stu-id="675b1-205">Overlays are great for a fast integration but can be sometimes not convenient, or can have unwanted side effects.</span></span>

<span data-ttu-id="675b1-206">Jeśli użytkownik nie ma spełnia Twoje wymagania systemu nakładki w niektórych widoków, można dostosować go do tych widoków.</span><span class="sxs-lookup"><span data-stu-id="675b1-206">If you're not satisfied with the overlay system in some of your views, you can customize it for these views.</span></span>

<span data-ttu-id="675b1-207">Można zdecydować objąć naszych układu powiadomień istniejących widoków.</span><span class="sxs-lookup"><span data-stu-id="675b1-207">You can decide to include our notification layout in your existing views.</span></span> <span data-ttu-id="675b1-208">Aby to zrobić, brak dwa style implementacji:</span><span class="sxs-lookup"><span data-stu-id="675b1-208">To do so, there is two implementation styles:</span></span>

1. <span data-ttu-id="675b1-209">Dodaj widok powiadomienia za pomocą konstruktora interfejsu</span><span class="sxs-lookup"><span data-stu-id="675b1-209">Add the notification view using interface builder</span></span>

   * <span data-ttu-id="675b1-210">Otwórz *interfejsu konstruktora*</span><span class="sxs-lookup"><span data-stu-id="675b1-210">Open *Interface Builder*</span></span>
   * <span data-ttu-id="675b1-211">Umieść 320 x 60 (lub jeśli iPad 768 x 60) `UIView` miejscu powiadomienia</span><span class="sxs-lookup"><span data-stu-id="675b1-211">Place a 320x60 (or 768x60 if you are on iPad) `UIView` where you want the notification to appear</span></span>
   * <span data-ttu-id="675b1-212">Ustaw wartość tagu dla tego widoku do: **36822491**</span><span class="sxs-lookup"><span data-stu-id="675b1-212">Set the Tag value for this view to : **36822491**</span></span>
2. <span data-ttu-id="675b1-213">Dodaj widok powiadomienia programowo.</span><span class="sxs-lookup"><span data-stu-id="675b1-213">Add the notification view programmatically.</span></span> <span data-ttu-id="675b1-214">Po zainicjowaniu widoku, po prostu dodaj następujący kod:</span><span class="sxs-lookup"><span data-stu-id="675b1-214">Just add the following code when your view has been initialized:</span></span>

       UIView* notificationView = [[UIView alloc] initWithFrame:CGRectMake(0, 0, 320, 60)]; //Replace x and y coordinate values to your needs.
       notificationView.tag = NOTIFICATION_AREA_VIEW_TAG;
       [self.view addSubview:notificationView];

<span data-ttu-id="675b1-215">`NOTIFICATION_AREA_VIEW_TAG`Makro można znaleźć w `AEDefaultNotifier.h`.</span><span class="sxs-lookup"><span data-stu-id="675b1-215">`NOTIFICATION_AREA_VIEW_TAG` macro can be found in `AEDefaultNotifier.h`.</span></span>

> [!NOTE]
> <span data-ttu-id="675b1-216">Zgłaszający domyślne automatycznie wykrywa, czy układ powiadomień znajduje się w tym widoku i nie dodają nakładki dla niego.</span><span class="sxs-lookup"><span data-stu-id="675b1-216">The default notifier automatically detects that the notification layout is included in this view and will not add an overlay for it.</span></span>
>
>

### <a name="announcements-and-polls"></a><span data-ttu-id="675b1-217">Anonsów i sond</span><span class="sxs-lookup"><span data-stu-id="675b1-217">Announcements and polls</span></span>
#### <a name="layouts"></a><span data-ttu-id="675b1-218">Układy</span><span class="sxs-lookup"><span data-stu-id="675b1-218">Layouts</span></span>
<span data-ttu-id="675b1-219">Można modyfikować pliki `AEDefaultAnnouncementView.xib` i `AEDefaultPollView.xib` tak długo, jak zabezpieczyć wartości tagów i typy widoków istniejących podrzędnych.</span><span class="sxs-lookup"><span data-stu-id="675b1-219">You can modify the files `AEDefaultAnnouncementView.xib` and `AEDefaultPollView.xib` as long as you keep the tag values and types of the existing subviews.</span></span>

#### <a name="categories"></a><span data-ttu-id="675b1-220">Kategorie</span><span class="sxs-lookup"><span data-stu-id="675b1-220">Categories</span></span>
##### <a name="alternate-layouts"></a><span data-ttu-id="675b1-221">Układy alternatywnej</span><span class="sxs-lookup"><span data-stu-id="675b1-221">Alternate layouts</span></span>
<span data-ttu-id="675b1-222">Takich jak powiadomienia Kategoria kampanii można mieć alternatywne układy anonsów i sond.</span><span class="sxs-lookup"><span data-stu-id="675b1-222">Like notifications, the campaign's category can be used to have alternate layouts for your announcements and polls.</span></span>

<span data-ttu-id="675b1-223">Aby utworzyć kategorii anonsu, należy rozszerzyć **AEAnnouncementViewController** i zarejestruj go po zainicjowaniu moduł reach:</span><span class="sxs-lookup"><span data-stu-id="675b1-223">To create a category for an announcement, you must extend **AEAnnouncementViewController** and register it once the reach module has been initialized:</span></span>

    AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
    [reach registerAnnouncementController:[MyCustomAnnouncementViewController class] forCategory:@"my_category"];

> [!NOTE]
> <span data-ttu-id="675b1-224">Każdym razem, użytkownik będzie kliknij powiadomienie anonsu z kategorią "Mój\_kategorii", kontroler widoku zarejestrowane (w takim przypadku `MyCustomAnnouncementViewController`) zostanie zainicjowana przez wywołanie metody `initWithAnnouncement:` i widoku zostaną dodane do bieżące okno aplikacji.</span><span class="sxs-lookup"><span data-stu-id="675b1-224">Each time a user will click on a notification for an announcement with the category "my\_category", your registered view controller (in that case `MyCustomAnnouncementViewController`) will be initialized by calling the method `initWithAnnouncement:` and the view will be added to the current application window.</span></span>
>
>

<span data-ttu-id="675b1-225">W implementacji `AEAnnouncementViewController` klasy trzeba będzie można odczytać właściwości `announcement` zainicjować z widoków podrzędnych.</span><span class="sxs-lookup"><span data-stu-id="675b1-225">In your implementation of the `AEAnnouncementViewController` class you will have to read the property `announcement` to initialize your subviews.</span></span> <span data-ttu-id="675b1-226">Należy wziąć pod uwagę w poniższym przykładzie, gdy dwie etykiety są inicjowane przy użyciu `title` i `body` właściwości `AEReachAnnouncement` klasy:</span><span class="sxs-lookup"><span data-stu-id="675b1-226">Consider the example below, where two labels are initialized using `title` and `body` properties of the `AEReachAnnouncement` class:</span></span>

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

<span data-ttu-id="675b1-227">Jeśli nie chcesz załadować widoków samodzielnie, ale po prostu chcesz ponownie użyć domyślnego układu widoku anonsu, po prostu ułatwia kontroler niestandardowy widok rozszerza klasę podana `AEDefaultAnnouncementViewController`.</span><span class="sxs-lookup"><span data-stu-id="675b1-227">If you don't want to load your views by yourself but you just want to reuse the default announcement view layout, you can simply make your custom view controller extends the provided class `AEDefaultAnnouncementViewController`.</span></span> <span data-ttu-id="675b1-228">W takim przypadku zduplikowany plik nib `AEDefaultAnnouncementView.xib` i zmień jego nazwę, dlatego może być załadowany przez kontroler niestandardowy widok (dla kontrolera o nazwie `CustomAnnouncementViewController`, należy wywołać pliku nib `CustomAnnouncementView.xib`).</span><span class="sxs-lookup"><span data-stu-id="675b1-228">In that case, duplicate the nib file `AEDefaultAnnouncementView.xib` and rename it so it can be loaded by your custom view controller (for a controller named `CustomAnnouncementViewController`, you should call your nib file `CustomAnnouncementView.xib`).</span></span>

<span data-ttu-id="675b1-229">Aby zastąpić domyślne kategorię anonsów, po prostu zarejestrować Kontroler Widok niestandardowy kategorii zdefiniowanej w `kAEReachDefaultCategory`:</span><span class="sxs-lookup"><span data-stu-id="675b1-229">To replace the default category of announcements, simply register your custom view controller for the category defined in `kAEReachDefaultCategory`:</span></span>

    [reach registerAnnouncementController:[MyCustomAnnouncementViewController class] forCategory:kAEReachDefaultCategory];

<span data-ttu-id="675b1-230">Ankiety można dostosować ten sam sposób:</span><span class="sxs-lookup"><span data-stu-id="675b1-230">Polls can be customized the same way :</span></span>

    AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
    [reach registerPollController:[MyCustomPollViewController class] forCategory:@"my_category"];

<span data-ttu-id="675b1-231">Teraz, dostępnego `MyCustomPollViewController` muszą być rozszerzane `AEPollViewController`.</span><span class="sxs-lookup"><span data-stu-id="675b1-231">This time, the provided `MyCustomPollViewController` must extend `AEPollViewController`.</span></span> <span data-ttu-id="675b1-232">Można rozszerzyć z domyślnego kontrolera: `AEDefaultPollViewController`.</span><span class="sxs-lookup"><span data-stu-id="675b1-232">Or you can choose to extend from the default controller: `AEDefaultPollViewController`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="675b1-233">Nie zapomnij wywołań albo `action` (`submitAnswers:` kontrolerów widok niestandardowy sondowania) lub `exit` metoda przed kontroler widoku jest odrzucane.</span><span class="sxs-lookup"><span data-stu-id="675b1-233">Don't forget to call either `action` (`submitAnswers:` for custom poll view controllers) or `exit` method before the view controller is dismissed.</span></span> <span data-ttu-id="675b1-234">W przeciwnym razie statystyki nie zostaną wysłane (tzn. nie analytics kampanii) i więcej kampanii istotne dalej nie zostaną powiadomieni do ponownego uruchomienia procesu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="675b1-234">Otherwise, statistics won't be sent (i.e. no analytics on the campaign) and more importantly next campaigns will not be notified until the application process is restarted.</span></span>
>
>

##### <a name="implementation-example"></a><span data-ttu-id="675b1-235">Przykład wdrożenia</span><span class="sxs-lookup"><span data-stu-id="675b1-235">Implementation example</span></span>
<span data-ttu-id="675b1-236">W tej implementacji widok niestandardowy anonsu została załadowana z pliku zewnętrznego xib.</span><span class="sxs-lookup"><span data-stu-id="675b1-236">In this implementation the custom announcement view is loaded from an external xib file.</span></span>

<span data-ttu-id="675b1-237">Podobnie jak dostosowywania powiadomień zaawansowane zalecane jest aby przyjrzeć się kodu źródłowego standardowej implementacji.</span><span class="sxs-lookup"><span data-stu-id="675b1-237">Like for advanced notification customization, it is recommended to look at the source code of the standard implementation.</span></span>

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
