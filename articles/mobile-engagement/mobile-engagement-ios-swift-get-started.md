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
# <a name="get-started-with-azure-mobile-engagement-for-ios-apps-in-swift"></a>Wprowadzenie do usługi Azure Mobile Engagement dla aplikacji systemu iOS w języku Swift
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

W tym temacie opisano sposób toounderstand usługi Azure Mobile Engagement toouse użycia aplikacji, a wysłać aplikacji dla systemu iOS tooan użytkowników toosegmented powiadomienia push.
W tym samouczku zostanie utworzona pusta aplikacja systemu iOS służąca do zbierania podstawowych danych i odbierania powiadomień wypychanych przy użyciu systemu Apple Push Notification System (APNS).

Ten samouczek wymaga następujących hello:

* Edytor XCode 8, który można zainstalować ze sklepu Mac App Store
* Witaj [Mobile Engagement iOS SDK]
* Certyfikat powiadomień wypychanych (p12), który można uzyskać z Centrum deweloperów firmy Apple

> [!NOTE]
> W tym samouczku jest używany język Swift w wersji 3.0. 
> 
> 

Wykonanie czynności opisanych w tym samouczku jest wymaganiem wstępnym dla wszystkich innych samouczków usługi Mobile Engagement dla aplikacji systemu iOS.

> [!NOTE]
> toocomplete tego samouczka, musi mieć aktywne konto platformy Azure. Jeśli go nie masz, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut. Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-ios-swift-get-started).
> 
> 

## <a id="setup-azme"></a>Konfigurowanie usługi Mobile Engagement dla aplikacji systemu iOS
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a id="connecting-app"></a>Połączenie z zapleczem usługi Mobile Engagement toohello aplikacji
Ten samouczek przedstawia "podstawową integrację", który czy hello minimalny wymagany toocollect danych i wysyłania powiadomień wypychanych. Witaj kompletna dokumentacja integracji znajduje się w hello [Mobile Engagement iOS SDK integration](mobile-engagement-ios-sdk-overview.md)

Utworzymy podstawową aplikację w środowisku XCode toodemonstrate hello integracji:

### <a name="create-a-new-ios-project"></a>Tworzenie nowego projektu systemu iOS
[!INCLUDE [Create a new iOS Project](../../includes/mobile-engagement-create-new-ios-app.md)]

### <a name="connect-your-app-toomobile-engagement-backend"></a>Połącz zapleczu swojej aplikacji tooMobile zaangażowania
1. Pobierz hello [Mobile Engagement iOS SDK]
2. Wyodrębnij hello. tar.gz pliku tooa folderu na swoim komputerze
3. Projektu powitania kliknij prawym przyciskiem myszy i wybierz opcję "Dodaj pliki zbyt..."
   
    ![][1]
4. Przejdź do folderu toohello, którym została rozpakowana hello zestawu SDK i wybierz hello `EngagementSDK` folder, a następnie naciśnij przycisk OK.
   
    ![][2]
5. Otwórz hello `Build Phases` kartę w hello `Link Binary With Libraries` menu Dodaj hello struktury, jak pokazano poniżej:
   
    ![][3]
6. Utworzyć mostkowanie nagłówka toobe toouse stanie hello w celu C interfejsów API zestawu SDK, wybierając plik > Nowy > Plik > iOS > źródło > pliku nagłówka.
   
    ![][4]
7. Edytuj hello mostkowanie nagłówka pliku tooexpose Mobile Engagement Objective-C kod tooyour kod Swift, Dodaj hello importuje następujące:
   
        /* Mobile Engagement Agent */
        #import "AEModule.h"
        #import "AEPushMessage.h"
        #import "AEStorage.h"
        #import "EngagementAgent.h"
        #import "EngagementTableViewController.h"
        #import "EngagementViewController.h"
        #import "AEUserNotificationHandler.h"
        #import "AEIdfaProvider.h"
8. W ustawieniach kompilacji upewnij się, że ustawienie w obszarze Swift kompilatora - generowania kodu kompilacji nagłówków mostkowania języka Objective-C hello ma nagłówek toothis ścieżki. Oto przykład ścieżki: **$(SRCROOT)/MySuperApp/MySuperApp-Bridging-Header.h (w zależności od ścieżki hello)**
   
   ![][6]
9. Przejdź wstecz toohello portalu Azure w Twojej aplikacji *informacje o połączeniu* strony i skopiuj parametry połączenia hello
   
   ![][5]
10. Teraz Wklej parametry połączenia hello hello `didFinishLaunchingWithOptions` delegowanie
    
        func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplicationLaunchOptionsKey: Any]?) -> Bool
        {
              [...]
                EngagementAgent.init("Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}")
              [...]
        }

## <a id="monitor"></a>Włączanie monitorowania w czasie rzeczywistym
W kolejności toostart wysyłanie danych i zapewnienie, że hello użytkownicy są aktywni konieczne jest wysłanie co najmniej jeden zapleczem usługi Mobile Engagement toohello ekranu (działanie).

1. Otwórz hello **ViewController.swift** plików i Zastąp klasę podstawową hello **ViewController** toobe **EngagementViewController**:
   
    `class ViewController : EngagementViewController {`

## <a id="monitor"></a>Łączenie aplikacji z funkcją monitorowania w czasie rzeczywistym
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a id="integrate-push"></a>Włączanie powiadomień wypychanych i funkcji komunikatów w aplikacji
Usługa Mobile Engagement umożliwia toointeract i ZASIĘGU z użytkownikami przy użyciu powiadomień wypychanych i komunikatów w aplikacji w kontekście hello kampanii. Ten moduł ma nazwę REACH w portalu Mobile Engagement hello.
Witaj poniższe sekcje umożliwią skonfigurowanie tooreceive Twojej aplikacji je.

### <a name="enable-your-app-tooreceive-silent-push-notifications"></a>Włącz tooreceive Twojej aplikacji cichych powiadomień wypychanych
[!INCLUDE [mobile-engagement-ios-silent-push](../../includes/mobile-engagement-ios-silent-push.md)]

### <a name="add-hello-reach-library-tooyour-project"></a>Dodaj projekt tooyour biblioteki Reach hello
1. Kliknij prawym przyciskiem projekt.
2. Wybierz pozycję `Add file too...`
3. Przejdź do folderu toohello, w którym wyodrębniono hello zestawu SDK
4. Wybierz hello `EngagementReach` folderu
5. Kliknij pozycję Dodaj.
6. Edytuj hello mostkowanie nagłówków Reach usługi Mobile Engagement Objective-C nagłówka pliku tooexpose i Dodaj hello importuje następujące:
   
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

### <a name="modify-your-application-delegate"></a>Modyfikowanie delegata aplikacji
1. Witaj wewnątrz `didFinishLaunchingWithOptions` — Utwórz moduł reach i przekaż go tooyour istniejącego wiersza inicjowania usługi Engagement:
   
        func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplicationLaunchOptionsKey: Any]?) -> Bool 
        {
            let reach = AEReachModule.module(withNotificationIcon: UIImage(named:"icon.png")) as! AEReachModule
            EngagementAgent.init("Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}", modulesArray:[reach])
            [...]
            return true
        }

### <a name="enable-your-app-tooreceive-apns-push-notifications"></a>Włącz tooreceive Twojej aplikacji powiadomień wypychanych usługi APNS
1. Dodaj powitania po wierszu toohello `didFinishLaunchingWithOptions` metody:
   
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
2. Dodaj hello `didRegisterForRemoteNotificationsWithDeviceToken` metody w następujący sposób:
   
        func application(_ application: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: Data) {
            EngagementAgent.shared().registerDeviceToken(deviceToken)
        }
3. Dodaj hello `didReceiveRemoteNotification:fetchCompletionHandler:` metody w następujący sposób:
   
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
