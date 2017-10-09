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
# <a name="ios-sdk-for-azure-mobile-engagement"></a>Zestaw iOS SDK dla usługi Azure Mobile Engagement
Zacznij tutaj tooget wszystkie hello szczegółowe informacje na temat toointegrate usługi Azure Mobile Engagement w aplikacji systemu iOS. Jeśli chcesz toogive on try najpierw upewnij się, można wykonywać naszych [samouczek 15 minut](mobile-engagement-ios-get-started.md).

Kliknij przycisk toosee hello [zawartość zestawu SDK](mobile-engagement-ios-sdk-content.md)

## <a name="integration-procedures"></a>Procedury integracji
1. Zacznij tutaj: [jak toointegrate Mobile Engagement w aplikacji systemu iOS](mobile-engagement-ios-integrate-engagement.md)
2. Dla powiadomień: [jak toointegrate Reach (powiadomienia) w aplikacji systemu iOS](mobile-engagement-ios-integrate-engagement-reach.md)
3. Tag plan implementacji: [jak toouse hello zaawansowane usługi Mobile Engagement znakowanie interfejsu API w aplikacji systemu iOS](mobile-engagement-ios-use-engagement-api.md)

## <a name="release-notes"></a>Informacje o wersji
### <a name="410-07172017"></a>4.1.0 (07/17/2017)
* Identyfikatory stałych wyczyszczone w tle.
* Stałe ostrzeżenia na 9 XCode o interfejsach API nie jest wywoływana w kolejki głównej.
* Stała sond Reach przeciek pamięci.
* Obsługę systemu iOS usunąć 6.X. Począwszy od ten cel wdrożenia hello wersji aplikacji musi mieć co najmniej system iOS 7.

Starsza wersja Zobacz hello [ukończyć informacje o wersji](mobile-engagement-ios-release-notes.md)

## <a name="upgrade-procedures"></a>Procedury uaktualniania
Jeśli już jest zintegrowany starszą wersję programu zaangażowania do aplikacji, należy hello tooconsider następujące punkty podczas uaktualniania hello zestawu SDK.

Masz toofollow kilka procedur Jeśli pominięte różne wersje hello zestawu SDK, zobacz pełną hello [procedur uaktualniania](mobile-engagement-ios-upgrade-procedure.md).

Dla każdej nowej wersji hello SDK najpierw należy zastąpić (Usuń i ponownie zaimportować w programie xcode) hello EngagementSDK i EngagementReach folderów.

### <a name="from-300-too400"></a>Z 3.0.0 too4.0.0
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

#### <a name="usernotifications-framework"></a>UserNotifications framework
Należy tooadd hello `UserNotifications` framework w poszczególnych faz kompilacji.

w obszarze Eksplorator projektów hello Otwórz okienko z projektu i wybierz docelowy o poprawnej hello. Następnie otwórz hello **"Fazy kompilacji"** kartę w hello **"Binarny z bibliotekami"** menu Dodaj framework `UserNotifications.framework` — zestaw hello Połącz jako`Optional`

#### <a name="application-push-capability"></a>Możliwości wypychania aplikacji
XCode 8 może zresetować aplikacji push możliwości, dokładnie Sprawdź ten w hello `capability` kartę wybranych docelowych.

#### <a name="add-hello-new-ios-10-notification-registration-code"></a>Dodaj kod rejestracji powiadomień 10 nowych iOS hello
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

#### <a name="resolve-unusernotificationcenter-delegate-conflicts"></a>Rozwiązywanie konfliktów delegata UNUserNotificationCenter

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
