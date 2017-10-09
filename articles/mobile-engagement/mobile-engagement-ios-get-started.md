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
# <a name="get-started-with-azure-mobile-engagement-for-ios-apps-in-objective-c"></a>Wprowadzenie do usługi Azure Mobile Engagement dla aplikacji systemu iOS w języku Objective C
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

W tym temacie opisano sposób toounderstand usługi Azure Mobile Engagement toouse użycia aplikacji, a wysłać aplikacji dla systemu iOS tooan użytkowników toosegmented powiadomienia push.
W tym samouczku zostanie utworzona pusta aplikacja systemu iOS służąca do zbierania podstawowych danych i odbierania powiadomień wypychanych przy użyciu systemu Apple Push Notification System (APNS).

Ten samouczek wymaga następujących hello:

* Edytor XCode 8, który można zainstalować ze sklepu Mac App Store
* Witaj [Mobile Engagement iOS SDK]

Wykonanie czynności opisanych w tym samouczku jest wymaganiem wstępnym dla wszystkich innych samouczków usługi Mobile Engagement dla aplikacji systemu iOS.

> [!NOTE]
> toocomplete tego samouczka, musi mieć aktywne konto platformy Azure. Jeśli go nie masz, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut. Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-ios-get-started).
>
>

## <a id="setup-azme"></a>Konfigurowanie usługi Mobile Engagement dla aplikacji systemu iOS
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a id="connecting-app"></a>Połączenie z zapleczem usługi Mobile Engagement toohello aplikacji
Ten samouczek przedstawia "podstawową integrację", który czy hello minimalny wymagany toocollect danych i wysyłania powiadomień wypychanych. Witaj kompletna dokumentacja integracji znajduje się w hello [Mobile Engagement iOS SDK integration](mobile-engagement-ios-sdk-overview.md)

Utworzymy podstawową aplikację w środowisku XCode toodemonstrate hello integracji.

### <a name="create-a-new-ios-project"></a>Tworzenie nowego projektu systemu iOS
[!INCLUDE [Create a new iOS Project](../../includes/mobile-engagement-create-new-ios-app.md)]

### <a name="connect-your-app-toohello-mobile-engagement-backend"></a>Połączenie z zapleczem usługi Mobile Engagement toohello aplikacji
1. Pobierz hello [Mobile Engagement iOS SDK].
2. Wyodrębnij hello. tar.gz pliku tooa folderu na swoim komputerze.
3. Kliknij prawym przyciskiem myszy projekt hello, a następnie wybierz **Dodaj pliki do**.

    ![][1]
4. Przejdź do folderu toohello, w którym wyodrębniono hello zestawu SDK, wybierz hello `EngagementSDK` folderu, kliknij przycisk **opcje** hello lewym dolnym rogu i upewnij się, że pole wyboru hello **skopiować elementy w razie potrzeby** i hello pole wyboru docelowego są sprawdzane, a następnie naciśnij klawisz **OK**.

    ![][2]
5. Otwórz hello **fazy kompilacji** karcie w hello **binarny z bibliotekami** menu Dodaj hello struktury, jak pokazano poniżej:

    ![][3]
6. Przejdź wstecz toohello portalu Azure w Twojej aplikacji **informacje o połączeniu** strony i skopiuj parametry połączenia hello.

    ![][4]
7. Dodaj powitania po wierszu kodu w Twojej **AppDelegate.m** pliku.

        #import "EngagementAgent.h"
8. Teraz Wklej parametry połączenia hello hello `didFinishLaunchingWithOptions` delegowanie.

        - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
        {
              [...]   
              [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}"];
              [...]
        }
9. `setTestLogEnabled`jest instrukcją opcjonalną, która umożliwia dzienników zestawu SDK dla Ciebie tooidentify problemów.

## <a id="monitor"></a>Włączanie monitorowania w czasie rzeczywistym
W kolejności toostart wysyłanie danych i zapewnienie, że hello użytkownicy są aktywni konieczne jest wysłanie co najmniej jeden zapleczem usługi Mobile Engagement toohello ekranu (działanie).

1. Otwórz hello **ViewController.h** pliku i zaimportować **EngagementViewController.h**:

    `#import "EngagementViewController.h"`
2. Teraz Zastąp hello superklasę hello **ViewController** interfejsu `EngagementViewController`:

    `@interface ViewController : EngagementViewController`

## <a id="monitor"></a>Łączenie aplikacji z funkcją monitorowania w czasie rzeczywistym
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a id="integrate-push"></a>Włączanie powiadomień wypychanych i funkcji komunikatów w aplikacji
Usługa Mobile Engagement umożliwia toointeract z użytkownikami i ZASIĘGU z powiadomień wypychanych i komunikatów w kontekście kampanii hello w aplikacji. Ten moduł ma nazwę REACH w portalu Mobile Engagement hello.
Witaj sekcje skonfigurować tooreceive Twojej aplikacji je.

### <a name="enable-your-app-tooreceive-silent-push-notifications"></a>Włącz tooreceive Twojej aplikacji cichych powiadomień wypychanych
[!INCLUDE [mobile-engagement-ios-silent-push](../../includes/mobile-engagement-ios-silent-push.md)]

### <a name="add-hello-reach-library-tooyour-project"></a>Dodaj projekt tooyour biblioteki Reach hello
1. Kliknij prawym przyciskiem myszy projekt.
2. Wybierz pozycję **Add file to** (Dodaj plik do).
3. Przejdź toohello folder, w którym wyodrębniono hello zestawu SDK.
4. Wybierz hello `EngagementReach` folderu.
5. Kliknij pozycję **Dodaj**.

### <a name="modify-your-application-delegate"></a>Modyfikowanie delegata aplikacji
1. W **Appdelegate.m** plików, zaimportuj moduł Reach usługi Engagement hello.

        #import "AEReachModule.h"
        #import <UserNotifications/UserNotifications.h>
2. Witaj wewnątrz `application:didFinishLaunchingWithOptions` metody, Utwórz moduł Reach i przekaż go tooyour istniejącego wiersza inicjowania usługi Engagement:

        - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
            AEReachModule * reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
            [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}" modules:reach, nil];
            [...]
            return YES;
        }

### <a name="enable-your-app-tooreceive-apns-push-notifications"></a>Włącz tooreceive Twojej aplikacji powiadomień wypychanych usługi APNS
1. Dodaj powitania po wierszu toohello `application:didFinishLaunchingWithOptions` metody:

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
2. Dodaj hello `application:didRegisterForRemoteNotificationsWithDeviceToken` metody w następujący sposób:

        - (void)application:(UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken
        {
             [[EngagementAgent shared] registerDeviceToken:deviceToken];
            NSLog(@"Registered Token: %@", deviceToken);
        }
3. Dodaj hello `didFailToRegisterForRemoteNotificationsWithError` metody w następujący sposób:

        - (void)application:(UIApplication*)application didFailToRegisterForRemoteNotificationsWithError:(NSError*)error
        {
           NSLog(@"Failed tooget token, error: %@", error);
        }
4. Dodaj hello `didReceiveRemoteNotification:fetchCompletionHandler` metody w następujący sposób:

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
