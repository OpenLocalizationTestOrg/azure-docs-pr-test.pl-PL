---
title: aaaGet Started with Azure Mobile Engagement na potrzeby platformy Xamarin.iOS
description: "Dowiedz się, jak toouse usługi Azure Mobile Engagement z funkcją analizy i powiadomieniami Wypychanymi dla aplikacji platformy Xamarin.iOS."
services: mobile-engagement
documentationcenter: xamarin
author: piyushjo
manager: erikre
editor: 
ms.assetid: 0448209e-fff6-47bd-985c-2cf074bac12f
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-ios
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 02340a744753dcc5cd1b6888a5fa87628be47b68
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-xamarinios-apps"></a>Rozpoczynanie pracy z usługą Azure Mobile Engagement na potrzeby aplikacji platformy Xamarin.iOS
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

W tym temacie opisano sposób toounderstand usługi Azure Mobile Engagement toouse Twoje użycie aplikacji i wysyłania wypychanie powiadomień toosegmented użytkowników aplikacji platformy Xamarin.iOS.
W tym samouczku zostanie utworzona pusta aplikacja platformy Xamarin.iOS służąca do zbierania danych podstawowych i odbierania powiadomień wypychanych przy użyciu systemu Apple Push Notification System (APNS).

> [!NOTE]
> Usługa Azure Mobile Engagement Hello zostaną wycofane 2018 marca i jest obecnie tylko dostępne tooexisting klientów. Aby uzyskać więcej informacji, zobacz [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).

Ten samouczek wymaga następujących hello:

* Program [Xamarin Studio](http://xamarin.com/studio). Można również użyć programu Visual Studio z platformą Xamarin, ale w tym samouczku używany jest program Xamarin Studio. Aby uzyskać instrukcje dotyczące instalowania, zobacz [Instalator i instalacja programu Visual Studio i platformy Xamarin](https://msdn.microsoft.com/library/mt613162.aspx). 
* [Zestaw SDK platformy Xamarin usługi Mobile Engagement](https://www.nuget.org/packages/Microsoft.Azure.Engagement.Xamarin/)

> [!NOTE]
> toocomplete tego samouczka, musi mieć aktywne konto platformy Azure. Jeśli go nie masz, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut. Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-xamarin-ios-get-started).
> 
> 

## <a id="setup-azme"></a>Konfigurowanie usługi Mobile Engagement dla aplikacji systemu iOS
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a id="connecting-app"></a>Połączenie z zapleczem usługi Mobile Engagement toohello aplikacji
Ten samouczek przedstawia "podstawową integrację", który czy hello minimalny wymagany toocollect danych i wysyłania powiadomień wypychanych.

Utworzymy podstawową aplikację z integracją hello toodemonstrate Xamarin:

### <a name="create-a-new-xamarinios-project"></a>Tworzenie nowego projektu platformy Xamarin.iOS
1. Uruchom program Xamarin Studio. Przejdź za**pliku** -> **nowy** -> **rozwiązania** 
   
    ![][1]
2. Wybierz **jednej aplikacji widoku**, upewnij się, że hello wybrany język to **C#** , a następnie kliknij przycisk **dalej**.
   
    ![][2]
3. Wypełnij hello **Nazwa aplikacji** i hello **identyfikator organizacji** , a następnie kliknij przycisk **dalej**. 
   
    ![][3]
   
   > [!IMPORTANT]
   > Upewnij się, tym hello, możesz użyć aplikacji systemu iOS używa identyfikator aplikacji, która jest zgodna z hello identyfikator pakietu w tym miejscu masz toodeploy profilu publikowania. 
   > 
   > 
4. Aktualizacja hello **Nazwa projektu**, **Nazwa rozwiązania** i **lokalizacji** wymagane, a następnie kliknij przycisk **Utwórz**.
   
    ![][4]

Program Xamarin Studio zostanie utworzona aplikacja demonstracyjna hello, w której zostanie zintegrowana usługa Mobile Engagement. 

### <a name="connect-your-app-toomobile-engagement-backend"></a>Połącz zapleczu swojej aplikacji tooMobile zaangażowania
1. Kliknij prawym przyciskiem myszy hello **pakiety** folder w systemie windows rozwiązania hello i wybierz **Dodawanie pakietów...**
   
    ![][5]
2. Wyszukaj hello **Microsoft Azure Mobile Engagement Xamarin SDK** i dodaj go tooyour rozwiązania.  
   
    ![][6]
3. Otwórz **AppDelegate.cs** i dodaj następujące hello instrukcję using:
   
        using Microsoft.Azure.Engagement.Xamarin;
4. W hello **FinishedLaunching** metody, Dodaj powitania po tooinitialize hello połączenia z zapleczem usługi Mobile Engagement. Upewnij się, że tooadd Twojego **ConnectionString**. Ten kod zawiera również **NotificationIcon** dodawany przez hello zestaw Mobile Engagement SDK, który może być tooreplace. 
   
        EngagementConfiguration config = new EngagementConfiguration {
                        ConnectionString = "YourConnectionStringFromAzurePortal",
                        NotificationIcon = UIImage.FromBundle("close")
                    };
        EngagementAgent.Init (config);

## <a id="monitor"></a>Włączanie monitorowania w czasie rzeczywistym
W kolejności toostart wysyłanie danych i zapewnienie, że hello użytkownicy są aktywni konieczne jest wysłanie co najmniej jeden zapleczem usługi Mobile Engagement toohello ekranu.

1. Otwórz **ViewController.cs** i dodaj następujące hello instrukcję using:
   
        using Microsoft.Azure.Engagement.Xamarin;
2. Zastąp klasę hello, z której `ViewController` dziedziczy `UIViewController` zbyt`EngagementViewController`. 

## <a id="monitor"></a>Łączenie aplikacji z funkcją monitorowania w czasie rzeczywistym
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a id="integrate-push"></a>Włączanie powiadomień wypychanych i funkcji komunikatów w aplikacji
Usługa Mobile Engagement umożliwia toointeract z użytkownikami i ZASIĘGU z powiadomień wypychanych i komunikatów w kontekście kampanii hello w aplikacji. Ten moduł ma nazwę REACH w portalu Mobile Engagement hello.
Witaj sekcje skonfigurować tooreceive Twojej aplikacji je.

### <a name="modify-your-application-delegate"></a>Modyfikowanie delegata aplikacji
1. Otwórz hello **AppDelegate.cs** i dodaj następujące hello instrukcję using:
   
        using System; 
2. Teraz wewnątrz hello `FinishedLaunching` metody, Dodaj następujące tooregister wiadomości wypychanych hello`EngagementAgent.init(...)`
   
        if (UIDevice.CurrentDevice.CheckSystemVersion(8,0))
        {
            var pushSettings = UIUserNotificationSettings.GetSettingsForTypes (
                (UIUserNotificationType.Badge |
                    UIUserNotificationType.Sound |
                    UIUserNotificationType.Alert),
                null);
            UIApplication.SharedApplication.RegisterUserNotificationSettings (pushSettings);
            UIApplication.SharedApplication.RegisterForRemoteNotifications ();
        }
        else
        {
            UIApplication.SharedApplication.RegisterForRemoteNotificationTypes (
                UIRemoteNotificationType.Badge |
                UIRemoteNotificationType.Sound |
                UIRemoteNotificationType.Alert);
        }
3. Na koniec — aktualizacja lub Dodaj hello następujące metody:
   
        public override void DidReceiveRemoteNotification (UIApplication application, NSDictionary userInfo, 
            Action<UIBackgroundFetchResult> completionHandler)
        {
            EngagementAgent.ApplicationDidReceiveRemoteNotification(userInfo, completionHandler);
        }
   
        public override void RegisteredForRemoteNotifications (UIApplication application, NSData deviceToken)
        {
            // Register device token on Engagement
            EngagementAgent.RegisterDeviceToken(deviceToken);
        }
   
        public override void FailedToRegisterForRemoteNotifications(UIApplication application, NSError error)
        {
            Console.WriteLine("Failed tooregister for remote notifications: Error '{0}'", error);
        }
4. W Twojej **Info.plist** pliku w rozwiązaniu hello, upewnij się, że hello **identyfikator pakietu** jest zgodny z hello **identyfikator aplikacji** ma w Twoim profilu inicjowania obsługi administracyjnej w hello deweloperów firmy Apple Centrum. 
   
    ![][7]
5. W hello sam **Info.plist** plików, upewnij się, że zaznaczono hello **Włącz tryby tła** i **zdalnego powiadomienia**. 
   
     ![][8]
6. Uruchamianie aplikacji hello na urządzeniu hello, który został skojarzony z tym profilem publikowania. 

[!INCLUDE [mobile-engagement-ios-send-push-push](../../includes/mobile-engagement-ios-send-push.md)]

<!-- Images. -->
[1]: ./media/mobile-engagement-xamarin-ios-get-started/new-solution.png
[2]: ./media/mobile-engagement-xamarin-ios-get-started/app-type.png
[3]: ./media/mobile-engagement-xamarin-ios-get-started/configure-project-name.png
[4]: ./media/mobile-engagement-xamarin-ios-get-started/configure-project-confirm.png
[5]: ./media/mobile-engagement-xamarin-ios-get-started/add-nuget.png
[6]: ./media/mobile-engagement-xamarin-ios-get-started/add-nuget-azme.png
[7]: ./media/mobile-engagement-xamarin-ios-get-started/info-plist-confirm-bundle.png
[8]: ./media/mobile-engagement-xamarin-ios-get-started/info-plist-configure-push.png
