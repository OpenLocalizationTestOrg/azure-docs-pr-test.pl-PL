---
title: "aaaAzure Mobile Engagement iOS SDK omówienie | Dokumentacja firmy Microsoft"
description: "Najnowsze aktualizacje i procedury dla systemu iOS SDK dla usługi Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 3a03bbd6-bcf8-436c-9775-5a8188629252
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 07/17/2017
ms.author: piyushjo
ms.openlocfilehash: 38f0da2f84df9c62f8fbca233bfda8b9936fdc0f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="ios-sdk-for-azure-mobile-engagement"></a><span data-ttu-id="d9ab2-103">Zestaw iOS SDK dla usługi Azure Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="d9ab2-103">iOS SDK for Azure Mobile Engagement</span></span>
<span data-ttu-id="d9ab2-104">Zacznij tutaj tooget wszystkie hello szczegółowe informacje na temat toointegrate usługi Azure Mobile Engagement w aplikacji systemu iOS.</span><span class="sxs-lookup"><span data-stu-id="d9ab2-104">Start here tooget all hello details on how toointegrate Azure Mobile Engagement in an iOS App.</span></span> <span data-ttu-id="d9ab2-105">Jeśli chcesz toogive on try najpierw upewnij się, można wykonywać naszych [samouczek 15 minut](mobile-engagement-ios-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="d9ab2-105">If you'd like toogive it a try first, make sure you do our [15 minutes tutorial](mobile-engagement-ios-get-started.md).</span></span>

<span data-ttu-id="d9ab2-106">Kliknij przycisk toosee hello [zawartość zestawu SDK](mobile-engagement-ios-sdk-content.md)</span><span class="sxs-lookup"><span data-stu-id="d9ab2-106">Click toosee hello [SDK Content](mobile-engagement-ios-sdk-content.md)</span></span>

## <a name="integration-procedures"></a><span data-ttu-id="d9ab2-107">Procedury integracji</span><span class="sxs-lookup"><span data-stu-id="d9ab2-107">Integration procedures</span></span>
1. <span data-ttu-id="d9ab2-108">Zacznij tutaj: [jak toointegrate Mobile Engagement w aplikacji systemu iOS](mobile-engagement-ios-integrate-engagement.md)</span><span class="sxs-lookup"><span data-stu-id="d9ab2-108">Start here: [How toointegrate Mobile Engagement in your iOS app](mobile-engagement-ios-integrate-engagement.md)</span></span>
2. <span data-ttu-id="d9ab2-109">Dla powiadomień: [jak toointegrate Reach (powiadomienia) w aplikacji systemu iOS](mobile-engagement-ios-integrate-engagement-reach.md)</span><span class="sxs-lookup"><span data-stu-id="d9ab2-109">For Notifications: [How toointegrate Reach (Notifications) in your iOS app](mobile-engagement-ios-integrate-engagement-reach.md)</span></span>
3. <span data-ttu-id="d9ab2-110">Tag plan implementacji: [jak toouse hello zaawansowane usługi Mobile Engagement znakowanie interfejsu API w aplikacji systemu iOS](mobile-engagement-ios-use-engagement-api.md)</span><span class="sxs-lookup"><span data-stu-id="d9ab2-110">Tag plan implementation: [How toouse hello advanced Mobile Engagement tagging API in your iOS app](mobile-engagement-ios-use-engagement-api.md)</span></span>

## <a name="release-notes"></a><span data-ttu-id="d9ab2-111">Informacje o wersji</span><span class="sxs-lookup"><span data-stu-id="d9ab2-111">Release notes</span></span>
### <a name="410-07172017"></a><span data-ttu-id="d9ab2-112">4.1.0 (07/17/2017)</span><span class="sxs-lookup"><span data-stu-id="d9ab2-112">4.1.0 (07/17/2017)</span></span>
* <span data-ttu-id="d9ab2-113">Identyfikatory stałych wyczyszczone w tle.</span><span class="sxs-lookup"><span data-stu-id="d9ab2-113">Fixed badges cleared in background.</span></span>
* <span data-ttu-id="d9ab2-114">Stałe ostrzeżenia na 9 XCode o interfejsach API nie jest wywoływana w kolejki głównej.</span><span class="sxs-lookup"><span data-stu-id="d9ab2-114">Fixed warnings on XCode 9 about APIs not called in main queue.</span></span>
* <span data-ttu-id="d9ab2-115">Stała sond Reach przeciek pamięci.</span><span class="sxs-lookup"><span data-stu-id="d9ab2-115">Fixed a memory leak in Reach polls.</span></span>
* <span data-ttu-id="d9ab2-116">Obsługę systemu iOS usunąć 6.X.</span><span class="sxs-lookup"><span data-stu-id="d9ab2-116">Dropped support for iOS 6.X.</span></span> <span data-ttu-id="d9ab2-117">Począwszy od ten cel wdrożenia hello wersji aplikacji musi mieć co najmniej system iOS 7.</span><span class="sxs-lookup"><span data-stu-id="d9ab2-117">Starting from this version hello deployment target of your application must be at least iOS 7.</span></span>

<span data-ttu-id="d9ab2-118">Starsza wersja Zobacz hello [ukończyć informacje o wersji](mobile-engagement-ios-release-notes.md)</span><span class="sxs-lookup"><span data-stu-id="d9ab2-118">For earlier version please see hello [complete release notes](mobile-engagement-ios-release-notes.md)</span></span>

## <a name="upgrade-procedures"></a><span data-ttu-id="d9ab2-119">Procedury uaktualniania</span><span class="sxs-lookup"><span data-stu-id="d9ab2-119">Upgrade procedures</span></span>
<span data-ttu-id="d9ab2-120">Jeśli już jest zintegrowany starszą wersję programu zaangażowania do aplikacji, należy hello tooconsider następujące punkty podczas uaktualniania hello zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="d9ab2-120">If you already have integrated an older version of Engagement into your application, you have tooconsider hello following points when upgrading hello SDK.</span></span>

<span data-ttu-id="d9ab2-121">Masz toofollow kilka procedur Jeśli pominięte różne wersje hello zestawu SDK, zobacz pełną hello [procedur uaktualniania](mobile-engagement-ios-upgrade-procedure.md).</span><span class="sxs-lookup"><span data-stu-id="d9ab2-121">You may have toofollow several procedures if you missed several versions of hello SDK see hello complete [Upgrade Procedures](mobile-engagement-ios-upgrade-procedure.md).</span></span>

<span data-ttu-id="d9ab2-122">Dla każdej nowej wersji hello SDK najpierw należy zastąpić (Usuń i ponownie zaimportować w programie xcode) hello EngagementSDK i EngagementReach folderów.</span><span class="sxs-lookup"><span data-stu-id="d9ab2-122">For each new version of hello SDK you must first replace (remove and re-import in xcode) hello EngagementSDK and EngagementReach folders.</span></span>

### <a name="from-300-too400"></a><span data-ttu-id="d9ab2-123">Z 3.0.0 too4.0.0</span><span class="sxs-lookup"><span data-stu-id="d9ab2-123">From 3.0.0 too4.0.0</span></span>
### <a name="xcode-8"></a><span data-ttu-id="d9ab2-124">XCode 8</span><span class="sxs-lookup"><span data-stu-id="d9ab2-124">XCode 8</span></span>
<span data-ttu-id="d9ab2-125">XCode 8 jest obowiązkowy, począwszy od wersji 4.0.0 hello zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="d9ab2-125">XCode 8 is mandatory starting from version 4.0.0 of hello SDK.</span></span>

> [!NOTE]
> <span data-ttu-id="d9ab2-126">Jeśli naprawdę są zależne od XCode 7, możesz użyć hello [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh).</span><span class="sxs-lookup"><span data-stu-id="d9ab2-126">If you really depend on XCode 7 then you may use hello [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh).</span></span> <span data-ttu-id="d9ab2-127">Brak znaną usterką na powitania moduł reach tej poprzedniej wersji podczas uruchamiania na urządzeniach z systemem iOS 10: powiadomień systemowych nie są których wykonano akcje.</span><span class="sxs-lookup"><span data-stu-id="d9ab2-127">There is a known bug on hello reach module of this previous version while running on iOS 10 devices:  system notifications are not actioned.</span></span> <span data-ttu-id="d9ab2-128">toofix to będzie miał tooimplement hello przestarzałe interfejsu API `application:didReceiveRemoteNotification:` w aplikacji delegowanie w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="d9ab2-128">toofix this you will have tooimplement hello deprecated API `application:didReceiveRemoteNotification:` in your app delegate as follows:</span></span>
>
>

    - (void)application:(UIApplication*)application
    didReceiveRemoteNotification:(NSDictionary*)userInfo
    {
        [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:nil];
    }

> [!IMPORTANT]
> <span data-ttu-id="d9ab2-129">**Nie zaleca się rozwiązanie** jak to zachowanie można zmienić w jakiegokolwiek uaktualnienia wersji nadchodzących iOS (nawet pomocnicze), ponieważ ten iOS interfejsu API jest przestarzały.</span><span class="sxs-lookup"><span data-stu-id="d9ab2-129">**We do not recommend this workaround** as this behavior can change in any upcoming (even minor) iOS version upgrade because this iOS API is deprecated.</span></span> <span data-ttu-id="d9ab2-130">Należy jak najszybciej przełącznika tooXCode 8.</span><span class="sxs-lookup"><span data-stu-id="d9ab2-130">You should switch tooXCode 8 as soon as possible.</span></span>
>
>

#### <a name="usernotifications-framework"></a><span data-ttu-id="d9ab2-131">UserNotifications framework</span><span class="sxs-lookup"><span data-stu-id="d9ab2-131">UserNotifications framework</span></span>
<span data-ttu-id="d9ab2-132">Należy tooadd hello `UserNotifications` framework w poszczególnych faz kompilacji.</span><span class="sxs-lookup"><span data-stu-id="d9ab2-132">You need tooadd hello `UserNotifications` framework in your Build Phases.</span></span>

<span data-ttu-id="d9ab2-133">w obszarze Eksplorator projektów hello Otwórz okienko z projektu i wybierz docelowy o poprawnej hello.</span><span class="sxs-lookup"><span data-stu-id="d9ab2-133">in hello project explorer, open your project pane and select hello correct target.</span></span> <span data-ttu-id="d9ab2-134">Następnie otwórz hello **"Fazy kompilacji"** kartę w hello **"Binarny z bibliotekami"** menu Dodaj framework `UserNotifications.framework` — zestaw hello Połącz jako`Optional`</span><span class="sxs-lookup"><span data-stu-id="d9ab2-134">Then, open hello **"Build phases"** tab and in hello **"Link Binary With Libraries"** menu, add framework `UserNotifications.framework` - set hello link as `Optional`</span></span>

#### <a name="application-push-capability"></a><span data-ttu-id="d9ab2-135">Możliwości wypychania aplikacji</span><span class="sxs-lookup"><span data-stu-id="d9ab2-135">Application push capability</span></span>
<span data-ttu-id="d9ab2-136">XCode 8 może zresetować aplikacji push możliwości, dokładnie Sprawdź ten w hello `capability` kartę wybranych docelowych.</span><span class="sxs-lookup"><span data-stu-id="d9ab2-136">XCode 8 may reset your app push capability, please double check it in hello `capability` tab of your selected target.</span></span>

#### <a name="add-hello-new-ios-10-notification-registration-code"></a><span data-ttu-id="d9ab2-137">Dodaj kod rejestracji powiadomień 10 nowych iOS hello</span><span class="sxs-lookup"><span data-stu-id="d9ab2-137">Add hello new iOS 10 notification registration code</span></span>
<span data-ttu-id="d9ab2-138">Hello starsze kodu fragment tooregister hello aplikacji toonotifications nadal działa, ale używa przestarzałe interfejsy API podczas uruchamiania w systemie iOS 10.</span><span class="sxs-lookup"><span data-stu-id="d9ab2-138">hello older code snippet tooregister hello app toonotifications still works but is using deprecated APIs while running on iOS 10.</span></span>

<span data-ttu-id="d9ab2-139">Importuj hello `User Notification` framework:</span><span class="sxs-lookup"><span data-stu-id="d9ab2-139">Import hello `User Notification` framework:</span></span>

        #import <UserNotifications/UserNotifications.h>

<span data-ttu-id="d9ab2-140">W delegata aplikacji `application:didFinishLaunchingWithOptions` Zastąp metodę:</span><span class="sxs-lookup"><span data-stu-id="d9ab2-140">In your application delegate `application:didFinishLaunchingWithOptions` method replace:</span></span>

        if ([application respondsToSelector:@selector(registerUserNotificationSettings:)]) {
            [application registerUserNotificationSettings:[UIUserNotificationSettings settingsForTypes:(UIUserNotificationTypeBadge | UIUserNotificationTypeSound | UIUserNotificationTypeAlert) categories:nil]];
            [application registerForRemoteNotifications];
        }
        else {

            [application registerForRemoteNotificationTypes:(UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound | UIRemoteNotificationTypeAlert)];
        }

<span data-ttu-id="d9ab2-141">przez:</span><span class="sxs-lookup"><span data-stu-id="d9ab2-141">by :</span></span>

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

#### <a name="resolve-unusernotificationcenter-delegate-conflicts"></a><span data-ttu-id="d9ab2-142">Rozwiązywanie konfliktów delegata UNUserNotificationCenter</span><span class="sxs-lookup"><span data-stu-id="d9ab2-142">Resolve UNUserNotificationCenter delegate conflicts</span></span>

<span data-ttu-id="d9ab2-143">*Jeśli implementuje jednej z bibliotek innych firm ani aplikacji `UNUserNotificationCenterDelegate` , a następnie można pominąć tej części.*</span><span class="sxs-lookup"><span data-stu-id="d9ab2-143">*If neither your application or one of your third party libraries implements a `UNUserNotificationCenterDelegate` then you can skip this part.*</span></span>

<span data-ttu-id="d9ab2-144">A `UNUserNotificationCenter` delegata jest używany przez hello SDK toomonitor hello cyklu życia zaangażowania powiadomienia na urządzeniach z systemem iOS, 10 lub nowszy.</span><span class="sxs-lookup"><span data-stu-id="d9ab2-144">A `UNUserNotificationCenter` delegate is used by hello SDK toomonitor hello life cycle of Engagement notifications on devices running on iOS 10 or greater.</span></span> <span data-ttu-id="d9ab2-145">Witaj SDK ma własną implementację hello `UNUserNotificationCenterDelegate` protokołu, ale może istnieć tylko jedna `UNUserNotificationCenter` delegować na aplikację.</span><span class="sxs-lookup"><span data-stu-id="d9ab2-145">hello SDK has its own implementation of hello `UNUserNotificationCenterDelegate` protocol but there can be only one `UNUserNotificationCenter` delegate per application.</span></span> <span data-ttu-id="d9ab2-146">Inne delegata dodane toohello `UNUserNotificationCenter` obiektu może powodować konflikt z hello zaangażowania jeden.</span><span class="sxs-lookup"><span data-stu-id="d9ab2-146">Any other delegate added toohello `UNUserNotificationCenter` object will conflict with hello Engagement one.</span></span> <span data-ttu-id="d9ab2-147">Jeśli hello SDK wykryje użytkownika lub dowolnej innej strony trzeciej na delegata nie zastosuje toogive własną implementację możesz tooresolve szansy hello konfliktów.</span><span class="sxs-lookup"><span data-stu-id="d9ab2-147">If hello SDK detects your or any other third party's delegate then it will not use its own implementation toogive you a chance tooresolve hello conflicts.</span></span> <span data-ttu-id="d9ab2-148">Konieczne będzie tooadd hello zaangażowania logiki tooyour właścicielem delegata w kolejności tooresolve hello konfliktów.</span><span class="sxs-lookup"><span data-stu-id="d9ab2-148">You will have tooadd hello Engagement logic tooyour own delegate in order tooresolve hello conflicts.</span></span>

<span data-ttu-id="d9ab2-149">Istnieją dwa sposoby tooachieve to.</span><span class="sxs-lookup"><span data-stu-id="d9ab2-149">There are two ways tooachieve this.</span></span>

<span data-ttu-id="d9ab2-150">Wniosek 1, po prostu przesyłając pełnomocnika wywołuje toohello zestawu SDK:</span><span class="sxs-lookup"><span data-stu-id="d9ab2-150">Proposal 1, simply by forwarding your delegate calls toohello SDK:</span></span>

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

<span data-ttu-id="d9ab2-151">Lub propozycji 2, dziedziczenie z hello `AEUserNotificationHandler` — klasa</span><span class="sxs-lookup"><span data-stu-id="d9ab2-151">Or proposal 2, by inheriting from hello `AEUserNotificationHandler` class</span></span>

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
> <span data-ttu-id="d9ab2-152">Można określić, czy powiadomienie jest dostarczany z zaangażowania lub nie przez przekazanie jej `userInfo` toohello słownika agenta `isEngagementPushPayload:` metoda klasy.</span><span class="sxs-lookup"><span data-stu-id="d9ab2-152">You can determine whether a notification comes from Engagement or not by passing its `userInfo` dictionary toohello Agent `isEngagementPushPayload:` class method.</span></span>

<span data-ttu-id="d9ab2-153">Upewnij się, że hello `UNUserNotificationCenter` obiektu delegowanego ustawiono tooyour delegata w obu hello `application:willFinishLaunchingWithOptions:` lub hello `application:didFinishLaunchingWithOptions:` metody delegata aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d9ab2-153">Make sure that hello `UNUserNotificationCenter` object's delegate is set tooyour delegate within either hello `application:willFinishLaunchingWithOptions:` or hello `application:didFinishLaunchingWithOptions:` method of your application delegate.</span></span>
<span data-ttu-id="d9ab2-154">Na przykład jeśli zaimplementowano hello powyżej wniosek 1:</span><span class="sxs-lookup"><span data-stu-id="d9ab2-154">For instance, if you implemented hello above proposal 1:</span></span>

      - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
        // Any other code

        [UNUserNotificationCenter currentNotificationCenter].delegate = self;
        return YES;
      }
