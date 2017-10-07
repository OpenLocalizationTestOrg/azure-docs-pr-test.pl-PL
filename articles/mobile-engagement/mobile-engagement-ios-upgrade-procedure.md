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
# <a name="upgrade-procedures"></a>Procedury uaktualniania
Jeśli już jest zintegrowany starszą wersję programu zaangażowania do aplikacji, należy hello tooconsider następujące punkty podczas uaktualniania hello zestawu SDK.

Dla każdej nowej wersji hello SDK najpierw należy zastąpić (Usuń i ponownie zaimportować w programie xcode) hello EngagementSDK i EngagementReach folderów.

## <a name="from-300-too400"></a>Z 3.0.0 too4.0.0
### <a name="xcode-8"></a>XCode 8
XCode 8 jest obowiązkowy, począwszy od wersji 4.0.0 hello zestawu SDK.

> [!NOTE]
> Jeśli naprawdę są zależne od XCode 7, możesz użyć hello [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh). Brak znaną usterką na powitania moduł reach tej poprzedniej wersji podczas uruchamiania na urządzeniach z systemem iOS 10: powiadomień systemowych nie są których wykonano akcje. toofix to będzie miał tooimplement hello przestarzałe interfejsu API `application:didReceiveRemoteNotification:` w aplikacji delegowanie w następujący sposób:
> 
> 

    - (void)application:(UIApplication*)application
    didReceiveRemoteNotification:(NSDictionary*)userInfo
    {
        [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:nil];
    }

> [!IMPORTANT]
> **Nie zaleca się rozwiązanie** jak to zachowanie można zmienić w jakiegokolwiek uaktualnienia wersji nadchodzących iOS (nawet pomocnicze), ponieważ ten iOS interfejsu API jest przestarzały. Należy jak najszybciej przełącznika tooXCode 8.
> 
> 

### <a name="usernotifications-framework"></a>UserNotifications framework
Należy tooadd hello `UserNotifications` framework w poszczególnych faz kompilacji.

w obszarze Eksplorator projektów hello Otwórz okienko z projektu i wybierz docelowy o poprawnej hello. Następnie otwórz hello **"Fazy kompilacji"** kartę w hello **"Binarny z bibliotekami"** menu Dodaj framework `UserNotifications.framework` — zestaw hello Połącz jako`Optional`

### <a name="application-push-capability"></a>Możliwości wypychania aplikacji
XCode 8 może zresetować aplikacji push możliwości, dokładnie Sprawdź ten w hello `capability` kartę wybranych docelowych.

### <a name="add-hello-new-ios-10-notification-registration-code"></a>Dodaj kod rejestracji powiadomień 10 nowych iOS hello
Hello starsze kodu fragment tooregister hello aplikacji toonotifications nadal działa, ale używa przestarzałe interfejsy API podczas uruchamiania w systemie iOS 10.

Importuj hello `User Notification` framework:

        #import <UserNotifications/UserNotifications.h> 

W delegata aplikacji `application:didFinishLaunchingWithOptions` Zastąp metodę:

    if ([application respondsToSelector:@selector(registerUserNotificationSettings:)]) {
        [application registerUserNotificationSettings:[UIUserNotificationSettings settingsForTypes:(UIUserNotificationTypeBadge | UIUserNotificationTypeSound | UIUserNotificationTypeAlert) categories:nil]];
        [application registerForRemoteNotifications];
    }
    else {

        [application registerForRemoteNotificationTypes:(UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound | UIRemoteNotificationTypeAlert)];
    }

przez:

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

### <a name="resolve-unusernotificationcenter-delegate-conflicts"></a>Rozwiązywanie konfliktów delegata UNUserNotificationCenter

*Jeśli implementuje jednej z bibliotek innych firm ani aplikacji `UNUserNotificationCenterDelegate` , a następnie można pominąć tej części.*

A `UNUserNotificationCenter` delegata jest używany przez hello SDK toomonitor hello cyklu życia zaangażowania powiadomienia na urządzeniach z systemem iOS, 10 lub nowszy. Witaj SDK ma własną implementację hello `UNUserNotificationCenterDelegate` protokołu, ale może istnieć tylko jedna `UNUserNotificationCenter` delegować na aplikację. Inne delegata dodane toohello `UNUserNotificationCenter` obiektu może powodować konflikt z hello zaangażowania jeden. Jeśli hello SDK wykryje użytkownika lub dowolnej innej strony trzeciej na delegata nie zastosuje toogive własną implementację możesz tooresolve szansy hello konfliktów. Konieczne będzie tooadd hello zaangażowania logiki tooyour właścicielem delegata w kolejności tooresolve hello konfliktów.

Istnieją dwa sposoby tooachieve to.

Wniosek 1, po prostu przesyłając pełnomocnika wywołuje toohello zestawu SDK:

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

Lub propozycji 2, dziedziczenie z hello `AEUserNotificationHandler` — klasa

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
> Można określić, czy powiadomienie jest dostarczany z zaangażowania lub nie przez przekazanie jej `userInfo` toohello słownika agenta `isEngagementPushPayload:` metoda klasy.

Upewnij się, że hello `UNUserNotificationCenter` obiektu delegowanego ustawiono tooyour delegata w obu hello `application:willFinishLaunchingWithOptions:` lub hello `application:didFinishLaunchingWithOptions:` metody delegata aplikacji.
Na przykład jeśli zaimplementowano hello powyżej wniosek 1:

      - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
        // Any other code
  
        [UNUserNotificationCenter currentNotificationCenter].delegate = self;
        return YES;
      }

## <a name="from-200-too300"></a>Z 2.0.0 too3.0.0
Obsługę systemu iOS usunąć 4.X. Począwszy od ten cel wdrożenia hello wersji aplikacji musi mieć co najmniej iOS 6.

Jeśli używasz Reach w aplikacji, należy dodać `remote-notification` toohello wartość `UIBackgroundModes` tablicy w pliku Info.plist w kolejności tooreceive zdalnego powiadomienia.

Witaj metody `application:didReceiveRemoteNotification:` musi toobe zastępuje `application:didReceiveRemoteNotification:fetchCompletionHandler:` w delegata aplikacji.

"AEPushDelegate.h" jest przestarzały interfejsu i potrzebujesz tooremove wszystkie odwołania. Dotyczy to również usunięcie `[[EngagementAgent shared] setPushDelegate:self]` i hello delegatem metody delegata aplikacji:

    -(void)willRetrieveLaunchMessage;
    -(void)didFailToRetrieveLaunchMessage;
    -(void)didReceiveLaunchMessage:(AEPushMessage*)launchMessage;

## <a name="from-1160-too200"></a>Z 1.16.0 too2.0.0
Witaj poniżej opisano sposób toomigrate integracji zestawu SDK z hello Capptain usługi oferowane przez Capptain SAS w aplikacji obsługiwane przez usługę Azure Mobile Engagement.
W przypadku migracji z wcześniejszej wersji, najpierw zapoznaj się hello Capptain witryny sieci web toomigrate too1.16 następnie Zastosuj hello procedury.

> [!IMPORTANT]
> Capptain i usługi Mobile Engagement nie hello tej samej usługi i procedury hello tylko podane poniżej prezentuje sposób toomigrate hello aplikacji klienckiej. Migrowanie hello zestawu SDK w aplikacji hello nie będą migrowane dane z hello Capptain serwerów toohello Mobile Engagement serwerów
> 
> 

### <a name="agent"></a>Agent
Witaj metody `registerApp:` został zastąpiony nową metodę hello `init:`. Delegata aplikacji należy zaktualizować odpowiednio i użyj parametrów połączenia:

            - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
            {
              [...]
              [EngagementAgent init:@"YOUR_CONNECTION_STRING"];
              [...]
            }

Śledzenie SmartAd został usunięty z zestawu SDK, wystarczy tooremove wszystkie wystąpienia `AETrackModule` — klasa

### <a name="class-name-changes"></a>Zmiany nazwy klasy
W ramach hello rebranding istnieje kilka nazw klasy/plików, które należy zmienić toobe.

Wszystkie klasy i jest poprzedzony prefiksem "CP" zostały zmienione z prefiksem "AE".

Przykład:

* `CPModule.h`Nazwa zostanie zmieniona zbyt`AEModule.h`.

Wszystkie klasy i jest poprzedzony prefiksem "Capptain" zostały zmienione z prefiksem "Zaangażowania".

Przykłady:

* Witaj klasy `CapptainAgent` jest zmieniana zbyt`EngagementAgent`.
* Witaj klasy `CapptainTableViewController` jest zmieniana zbyt`EngagementTableViewController`.
* Witaj klasy `CapptainUtils` jest zmieniana zbyt`EngagementUtils`.
* Witaj klasy `CapptainViewController` jest zmieniana zbyt`EngagementViewController`.

