---
title: aaaAzure Mobile Engagement iOS SDK procedury uaktualniania | Dokumentacja firmy Microsoft
description: "Najnowsze aktualizacje i procedury dla systemu iOS SDK dla usługi Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 72a9e493-3f14-4e52-b6e2-0490fd04b184
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 12/13/2016
ms.author: piyushjo
ms.openlocfilehash: 5a81bcaaec72aec665b3334e6400d520454d56a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-procedures"></a><span data-ttu-id="24b54-103">Procedury uaktualniania</span><span class="sxs-lookup"><span data-stu-id="24b54-103">Upgrade procedures</span></span>
<span data-ttu-id="24b54-104">Jeśli już jest zintegrowany starszą wersję programu zaangażowania do aplikacji, należy hello tooconsider następujące punkty podczas uaktualniania hello zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="24b54-104">If you already have integrated an older version of Engagement into your application, you have tooconsider hello following points when upgrading hello SDK.</span></span>

<span data-ttu-id="24b54-105">Dla każdej nowej wersji hello SDK najpierw należy zastąpić (Usuń i ponownie zaimportować w programie xcode) hello EngagementSDK i EngagementReach folderów.</span><span class="sxs-lookup"><span data-stu-id="24b54-105">For each new version of hello SDK you must first replace (remove and re-import in xcode) hello EngagementSDK and EngagementReach folders.</span></span>

## <a name="from-300-too400"></a><span data-ttu-id="24b54-106">Z 3.0.0 too4.0.0</span><span class="sxs-lookup"><span data-stu-id="24b54-106">From 3.0.0 too4.0.0</span></span>
### <a name="xcode-8"></a><span data-ttu-id="24b54-107">XCode 8</span><span class="sxs-lookup"><span data-stu-id="24b54-107">XCode 8</span></span>
<span data-ttu-id="24b54-108">XCode 8 jest obowiązkowy, począwszy od wersji 4.0.0 hello zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="24b54-108">XCode 8 is mandatory starting from version 4.0.0 of hello SDK.</span></span>

> [!NOTE]
> <span data-ttu-id="24b54-109">Jeśli naprawdę są zależne od XCode 7, możesz użyć hello [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh).</span><span class="sxs-lookup"><span data-stu-id="24b54-109">If you really depend on XCode 7 then you may use hello [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh).</span></span> <span data-ttu-id="24b54-110">Brak znaną usterką na powitania moduł reach tej poprzedniej wersji podczas uruchamiania na urządzeniach z systemem iOS 10: powiadomień systemowych nie są których wykonano akcje.</span><span class="sxs-lookup"><span data-stu-id="24b54-110">There is a known bug on hello reach module of this previous version while running on iOS 10 devices:  system notifications are not actioned.</span></span> <span data-ttu-id="24b54-111">toofix to będzie miał tooimplement hello przestarzałe interfejsu API `application:didReceiveRemoteNotification:` w aplikacji delegowanie w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="24b54-111">toofix this you will have tooimplement hello deprecated API `application:didReceiveRemoteNotification:` in your app delegate as follows:</span></span>
> 
> 

    - (void)application:(UIApplication*)application
    didReceiveRemoteNotification:(NSDictionary*)userInfo
    {
        [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:nil];
    }

> [!IMPORTANT]
> <span data-ttu-id="24b54-112">**Nie zaleca się rozwiązanie** jak to zachowanie można zmienić w jakiegokolwiek uaktualnienia wersji nadchodzących iOS (nawet pomocnicze), ponieważ ten iOS interfejsu API jest przestarzały.</span><span class="sxs-lookup"><span data-stu-id="24b54-112">**We do not recommend this workaround** as this behavior can change in any upcoming (even minor) iOS version upgrade because this iOS API is deprecated.</span></span> <span data-ttu-id="24b54-113">Należy jak najszybciej przełącznika tooXCode 8.</span><span class="sxs-lookup"><span data-stu-id="24b54-113">You should switch tooXCode 8 as soon as possible.</span></span>
> 
> 

### <a name="usernotifications-framework"></a><span data-ttu-id="24b54-114">UserNotifications framework</span><span class="sxs-lookup"><span data-stu-id="24b54-114">UserNotifications framework</span></span>
<span data-ttu-id="24b54-115">Należy tooadd hello `UserNotifications` framework w poszczególnych faz kompilacji.</span><span class="sxs-lookup"><span data-stu-id="24b54-115">You need tooadd hello `UserNotifications` framework in your Build Phases.</span></span>

<span data-ttu-id="24b54-116">w obszarze Eksplorator projektów hello Otwórz okienko z projektu i wybierz docelowy o poprawnej hello.</span><span class="sxs-lookup"><span data-stu-id="24b54-116">in hello project explorer, open your project pane and select hello correct target.</span></span> <span data-ttu-id="24b54-117">Następnie otwórz hello **"Fazy kompilacji"** kartę w hello **"Binarny z bibliotekami"** menu Dodaj framework `UserNotifications.framework` — zestaw hello Połącz jako`Optional`</span><span class="sxs-lookup"><span data-stu-id="24b54-117">Then, open hello **"Build phases"** tab and in hello **"Link Binary With Libraries"** menu, add framework `UserNotifications.framework` - set hello link as `Optional`</span></span>

### <a name="application-push-capability"></a><span data-ttu-id="24b54-118">Możliwości wypychania aplikacji</span><span class="sxs-lookup"><span data-stu-id="24b54-118">Application push capability</span></span>
<span data-ttu-id="24b54-119">XCode 8 może zresetować aplikacji push możliwości, dokładnie Sprawdź ten w hello `capability` kartę wybranych docelowych.</span><span class="sxs-lookup"><span data-stu-id="24b54-119">XCode 8 may reset your app push capability, please double check it in hello `capability` tab of your selected target.</span></span>

### <a name="add-hello-new-ios-10-notification-registration-code"></a><span data-ttu-id="24b54-120">Dodaj kod rejestracji powiadomień 10 nowych iOS hello</span><span class="sxs-lookup"><span data-stu-id="24b54-120">Add hello new iOS 10 notification registration code</span></span>
<span data-ttu-id="24b54-121">Hello starsze kodu fragment tooregister hello aplikacji toonotifications nadal działa, ale używa przestarzałe interfejsy API podczas uruchamiania w systemie iOS 10.</span><span class="sxs-lookup"><span data-stu-id="24b54-121">hello older code snippet tooregister hello app toonotifications still works but is using deprecated APIs while running on iOS 10.</span></span>

<span data-ttu-id="24b54-122">Importuj hello `User Notification` framework:</span><span class="sxs-lookup"><span data-stu-id="24b54-122">Import hello `User Notification` framework:</span></span>

        #import <UserNotifications/UserNotifications.h> 

<span data-ttu-id="24b54-123">W delegata aplikacji `application:didFinishLaunchingWithOptions` Zastąp metodę:</span><span class="sxs-lookup"><span data-stu-id="24b54-123">In your application delegate `application:didFinishLaunchingWithOptions` method replace:</span></span>

    if ([application respondsToSelector:@selector(registerUserNotificationSettings:)]) {
        [application registerUserNotificationSettings:[UIUserNotificationSettings settingsForTypes:(UIUserNotificationTypeBadge | UIUserNotificationTypeSound | UIUserNotificationTypeAlert) categories:nil]];
        [application registerForRemoteNotifications];
    }
    else {

        [application registerForRemoteNotificationTypes:(UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound | UIRemoteNotificationTypeAlert)];
    }

<span data-ttu-id="24b54-124">przez:</span><span class="sxs-lookup"><span data-stu-id="24b54-124">by :</span></span>

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

### <a name="resolve-unusernotificationcenter-delegate-conflicts"></a><span data-ttu-id="24b54-125">Rozwiązywanie konfliktów delegata UNUserNotificationCenter</span><span class="sxs-lookup"><span data-stu-id="24b54-125">Resolve UNUserNotificationCenter delegate conflicts</span></span>

<span data-ttu-id="24b54-126">*Jeśli implementuje jednej z bibliotek innych firm ani aplikacji `UNUserNotificationCenterDelegate` , a następnie można pominąć tej części.*</span><span class="sxs-lookup"><span data-stu-id="24b54-126">*If neither your application or one of your third party libraries implements a `UNUserNotificationCenterDelegate` then you can skip this part.*</span></span>

<span data-ttu-id="24b54-127">A `UNUserNotificationCenter` delegata jest używany przez hello SDK toomonitor hello cyklu życia zaangażowania powiadomienia na urządzeniach z systemem iOS, 10 lub nowszy.</span><span class="sxs-lookup"><span data-stu-id="24b54-127">A `UNUserNotificationCenter` delegate is used by hello SDK toomonitor hello life cycle of Engagement notifications on devices running on iOS 10 or greater.</span></span> <span data-ttu-id="24b54-128">Witaj SDK ma własną implementację hello `UNUserNotificationCenterDelegate` protokołu, ale może istnieć tylko jedna `UNUserNotificationCenter` delegować na aplikację.</span><span class="sxs-lookup"><span data-stu-id="24b54-128">hello SDK has its own implementation of hello `UNUserNotificationCenterDelegate` protocol but there can be only one `UNUserNotificationCenter` delegate per application.</span></span> <span data-ttu-id="24b54-129">Inne delegata dodane toohello `UNUserNotificationCenter` obiektu może powodować konflikt z hello zaangażowania jeden.</span><span class="sxs-lookup"><span data-stu-id="24b54-129">Any other delegate added toohello `UNUserNotificationCenter` object will conflict with hello Engagement one.</span></span> <span data-ttu-id="24b54-130">Jeśli hello SDK wykryje użytkownika lub dowolnej innej strony trzeciej na delegata nie zastosuje toogive własną implementację możesz tooresolve szansy hello konfliktów.</span><span class="sxs-lookup"><span data-stu-id="24b54-130">If hello SDK detects your or any other third party's delegate then it will not use its own implementation toogive you a chance tooresolve hello conflicts.</span></span> <span data-ttu-id="24b54-131">Konieczne będzie tooadd hello zaangażowania logiki tooyour właścicielem delegata w kolejności tooresolve hello konfliktów.</span><span class="sxs-lookup"><span data-stu-id="24b54-131">You will have tooadd hello Engagement logic tooyour own delegate in order tooresolve hello conflicts.</span></span>

<span data-ttu-id="24b54-132">Istnieją dwa sposoby tooachieve to.</span><span class="sxs-lookup"><span data-stu-id="24b54-132">There are two ways tooachieve this.</span></span>

<span data-ttu-id="24b54-133">Wniosek 1, po prostu przesyłając pełnomocnika wywołuje toohello zestawu SDK:</span><span class="sxs-lookup"><span data-stu-id="24b54-133">Proposal 1, simply by forwarding your delegate calls toohello SDK:</span></span>

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

<span data-ttu-id="24b54-134">Lub propozycji 2, dziedziczenie z hello `AEUserNotificationHandler` — klasa</span><span class="sxs-lookup"><span data-stu-id="24b54-134">Or proposal 2, by inheriting from hello `AEUserNotificationHandler` class</span></span>

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
> <span data-ttu-id="24b54-135">Można określić, czy powiadomienie jest dostarczany z zaangażowania lub nie przez przekazanie jej `userInfo` toohello słownika agenta `isEngagementPushPayload:` metoda klasy.</span><span class="sxs-lookup"><span data-stu-id="24b54-135">You can determine whether a notification comes from Engagement or not by passing its `userInfo` dictionary toohello Agent `isEngagementPushPayload:` class method.</span></span>

<span data-ttu-id="24b54-136">Upewnij się, że hello `UNUserNotificationCenter` obiektu delegowanego ustawiono tooyour delegata w obu hello `application:willFinishLaunchingWithOptions:` lub hello `application:didFinishLaunchingWithOptions:` metody delegata aplikacji.</span><span class="sxs-lookup"><span data-stu-id="24b54-136">Make sure that hello `UNUserNotificationCenter` object's delegate is set tooyour delegate within either hello `application:willFinishLaunchingWithOptions:` or hello `application:didFinishLaunchingWithOptions:` method of your application delegate.</span></span>
<span data-ttu-id="24b54-137">Na przykład jeśli zaimplementowano hello powyżej wniosek 1:</span><span class="sxs-lookup"><span data-stu-id="24b54-137">For instance, if you implemented hello above proposal 1:</span></span>

      - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
        // Any other code
  
        [UNUserNotificationCenter currentNotificationCenter].delegate = self;
        return YES;
      }

## <a name="from-200-too300"></a><span data-ttu-id="24b54-138">Z 2.0.0 too3.0.0</span><span class="sxs-lookup"><span data-stu-id="24b54-138">From 2.0.0 too3.0.0</span></span>
<span data-ttu-id="24b54-139">Obsługę systemu iOS usunąć 4.X.</span><span class="sxs-lookup"><span data-stu-id="24b54-139">Dropped support for iOS 4.X.</span></span> <span data-ttu-id="24b54-140">Począwszy od ten cel wdrożenia hello wersji aplikacji musi mieć co najmniej iOS 6.</span><span class="sxs-lookup"><span data-stu-id="24b54-140">Starting from this version hello deployment target of your application must be at least iOS 6.</span></span>

<span data-ttu-id="24b54-141">Jeśli używasz Reach w aplikacji, należy dodać `remote-notification` toohello wartość `UIBackgroundModes` tablicy w pliku Info.plist w kolejności tooreceive zdalnego powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="24b54-141">If you are using Reach in your application, you must add `remote-notification` value toohello `UIBackgroundModes` array in your Info.plist file in order tooreceive remote notifications.</span></span>

<span data-ttu-id="24b54-142">Witaj metody `application:didReceiveRemoteNotification:` musi toobe zastępuje `application:didReceiveRemoteNotification:fetchCompletionHandler:` w delegata aplikacji.</span><span class="sxs-lookup"><span data-stu-id="24b54-142">hello method `application:didReceiveRemoteNotification:` needs toobe replaced by `application:didReceiveRemoteNotification:fetchCompletionHandler:` in your application delegate.</span></span>

<span data-ttu-id="24b54-143">"AEPushDelegate.h" jest przestarzały interfejsu i potrzebujesz tooremove wszystkie odwołania.</span><span class="sxs-lookup"><span data-stu-id="24b54-143">"AEPushDelegate.h" is deprecated interface and you need tooremove all references.</span></span> <span data-ttu-id="24b54-144">Dotyczy to również usunięcie `[[EngagementAgent shared] setPushDelegate:self]` i hello delegatem metody delegata aplikacji:</span><span class="sxs-lookup"><span data-stu-id="24b54-144">This includes removing `[[EngagementAgent shared] setPushDelegate:self]` and hello delegate methods from your application delegate:</span></span>

    -(void)willRetrieveLaunchMessage;
    -(void)didFailToRetrieveLaunchMessage;
    -(void)didReceiveLaunchMessage:(AEPushMessage*)launchMessage;

## <a name="from-1160-too200"></a><span data-ttu-id="24b54-145">Z 1.16.0 too2.0.0</span><span class="sxs-lookup"><span data-stu-id="24b54-145">From 1.16.0 too2.0.0</span></span>
<span data-ttu-id="24b54-146">Witaj poniżej opisano sposób toomigrate integracji zestawu SDK z hello Capptain usługi oferowane przez Capptain SAS w aplikacji obsługiwane przez usługę Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="24b54-146">hello following describes how toomigrate an SDK integration from hello Capptain service offered by Capptain SAS into an app powered by Azure Mobile Engagement.</span></span>
<span data-ttu-id="24b54-147">W przypadku migracji z wcześniejszej wersji, najpierw zapoznaj się hello Capptain witryny sieci web toomigrate too1.16 następnie Zastosuj hello procedury.</span><span class="sxs-lookup"><span data-stu-id="24b54-147">If you are migrating from an earlier version, please consult hello Capptain web site toomigrate too1.16 first then apply hello following procedure.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="24b54-148">Capptain i usługi Mobile Engagement nie hello tej samej usługi i procedury hello tylko podane poniżej prezentuje sposób toomigrate hello aplikacji klienckiej.</span><span class="sxs-lookup"><span data-stu-id="24b54-148">Capptain and Mobile Engagement are not hello same services and hello procedure given below only highlights how toomigrate hello client app.</span></span> <span data-ttu-id="24b54-149">Migrowanie hello zestawu SDK w aplikacji hello nie będą migrowane dane z hello Capptain serwerów toohello Mobile Engagement serwerów</span><span class="sxs-lookup"><span data-stu-id="24b54-149">Migrating hello SDK in hello app will NOT migrate your data from hello Capptain servers toohello Mobile Engagement servers</span></span>
> 
> 

### <a name="agent"></a><span data-ttu-id="24b54-150">Agent</span><span class="sxs-lookup"><span data-stu-id="24b54-150">Agent</span></span>
<span data-ttu-id="24b54-151">Witaj metody `registerApp:` został zastąpiony nową metodę hello `init:`.</span><span class="sxs-lookup"><span data-stu-id="24b54-151">hello method `registerApp:` has been replaced by hello new method `init:`.</span></span> <span data-ttu-id="24b54-152">Delegata aplikacji należy zaktualizować odpowiednio i użyj parametrów połączenia:</span><span class="sxs-lookup"><span data-stu-id="24b54-152">Your application delegate must be updated accordingly and use connection string:</span></span>

            - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
            {
              [...]
              [EngagementAgent init:@"YOUR_CONNECTION_STRING"];
              [...]
            }

<span data-ttu-id="24b54-153">Śledzenie SmartAd został usunięty z zestawu SDK, wystarczy tooremove wszystkie wystąpienia `AETrackModule` — klasa</span><span class="sxs-lookup"><span data-stu-id="24b54-153">SmartAd tracking has been removed from SDK you just have tooremove all instances of `AETrackModule` class</span></span>

### <a name="class-name-changes"></a><span data-ttu-id="24b54-154">Zmiany nazwy klasy</span><span class="sxs-lookup"><span data-stu-id="24b54-154">Class Name Changes</span></span>
<span data-ttu-id="24b54-155">W ramach hello rebranding istnieje kilka nazw klasy/plików, które należy zmienić toobe.</span><span class="sxs-lookup"><span data-stu-id="24b54-155">As part of hello rebranding, there are couple of class/file names that need toobe changed.</span></span>

<span data-ttu-id="24b54-156">Wszystkie klasy i jest poprzedzony prefiksem "CP" zostały zmienione z prefiksem "AE".</span><span class="sxs-lookup"><span data-stu-id="24b54-156">All classes prefixed with "CP" are renamed with "AE" prefix.</span></span>

<span data-ttu-id="24b54-157">Przykład:</span><span class="sxs-lookup"><span data-stu-id="24b54-157">Example:</span></span>

* <span data-ttu-id="24b54-158">`CPModule.h`Nazwa zostanie zmieniona zbyt`AEModule.h`.</span><span class="sxs-lookup"><span data-stu-id="24b54-158">`CPModule.h` is renamed too`AEModule.h`.</span></span>

<span data-ttu-id="24b54-159">Wszystkie klasy i jest poprzedzony prefiksem "Capptain" zostały zmienione z prefiksem "Zaangażowania".</span><span class="sxs-lookup"><span data-stu-id="24b54-159">All classes prefixed with "Capptain" are renamed with "Engagement" prefix.</span></span>

<span data-ttu-id="24b54-160">Przykłady:</span><span class="sxs-lookup"><span data-stu-id="24b54-160">Examples:</span></span>

* <span data-ttu-id="24b54-161">Witaj klasy `CapptainAgent` jest zmieniana zbyt`EngagementAgent`.</span><span class="sxs-lookup"><span data-stu-id="24b54-161">hello class `CapptainAgent` is renamed too`EngagementAgent`.</span></span>
* <span data-ttu-id="24b54-162">Witaj klasy `CapptainTableViewController` jest zmieniana zbyt`EngagementTableViewController`.</span><span class="sxs-lookup"><span data-stu-id="24b54-162">hello class `CapptainTableViewController` is renamed too`EngagementTableViewController`.</span></span>
* <span data-ttu-id="24b54-163">Witaj klasy `CapptainUtils` jest zmieniana zbyt`EngagementUtils`.</span><span class="sxs-lookup"><span data-stu-id="24b54-163">hello class `CapptainUtils` is renamed too`EngagementUtils`.</span></span>
* <span data-ttu-id="24b54-164">Witaj klasy `CapptainViewController` jest zmieniana zbyt`EngagementViewController`.</span><span class="sxs-lookup"><span data-stu-id="24b54-164">hello class `CapptainViewController` is renamed too`EngagementViewController`.</span></span>

