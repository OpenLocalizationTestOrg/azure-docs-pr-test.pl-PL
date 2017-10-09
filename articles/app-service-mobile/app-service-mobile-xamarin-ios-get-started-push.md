---
title: "aaaAdd aplikacji platformy Xamarin.iOS tooyour powiadomienia wypychane z usługi aplikacji Azure"
description: "Dowiedz się, jak toosend usłudze Azure App Service toouse push aplikacji platformy Xamarin.iOS tooyour powiadomienia"
services: app-service\mobile
documentationcenter: xamarin
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 2921214a-49f8-45e1-a306-a85ce21defca
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-ios
ms.devlang: dotnet
ms.topic: article
ms.date: 10/12/2016
ms.author: glenga
ms.openlocfilehash: 3e6439aee4f3fe0f60b9786d0bbfd74c4f5e52d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="add-push-notifications-tooyour-xamarinios-app"></a>Dodaj tooyour powiadomienia wypychane aplikacji platformy Xamarin.iOS
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a>Omówienie
W tym samouczku, możesz dodać toohello powiadomień wypychanych [Xamarin.iOS szybki start](app-service-mobile-xamarin-ios-get-started.md) projektu, aby powiadomienie wypychane zostanie wysłane toohello urządzenia, za każdym razem, gdy wstawieniu rekordu.

Jeśli nie używasz hello pobrany Projekt serwera szybki start, muszą hello pakiet rozszerzenia powiadomień wypychanych. Zobacz [pracować z serwera wewnętrznej bazy danych hello .NET SDK usługi Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) Aby uzyskać więcej informacji.

## <a name="prerequisites"></a>Wymagania wstępne
* Zakończenie hello [szybkiego startu Xamarin.iOS](app-service-mobile-xamarin-ios-get-started.md) samouczka.
* Urządzenie fizyczne z systemem iOS. Powiadomienia wypychane nie są obsługiwane przez hello symulatora systemu iOS.

## <a name="register-hello-app-for-push-notifications-on-apples-developer-portal"></a>Rejestrowanie aplikacji hello powiadomień wypychanych na portalu dla deweloperów firmy Apple
[!INCLUDE [Enable Apple Push Notifications](../../includes/enable-apple-push-notifications.md)]

## <a name="configure-your-mobile-app-toosend-push-notifications"></a>Konfigurowanie powiadomień wypychanych toosend aplikacji mobilnej
[!INCLUDE [app-service-mobile-apns-configure-push](../../includes/app-service-mobile-apns-configure-push.md)]

## <a name="update-hello-server-project-toosend-push-notifications"></a>Zaktualizuj powiadomień wypychanych toosend powitania serwera projektu
[!INCLUDE [app-service-mobile-update-server-project-for-push-template](../../includes/app-service-mobile-update-server-project-for-push-template.md)]

## <a name="configure-your-xamarinios-project"></a>Konfigurowanie projektu platformy Xamarin.iOS
[!INCLUDE [app-service-mobile-xamarin-ios-configure-project](../../includes/app-service-mobile-xamarin-ios-configure-project.md)]

## <a name="add-push-notifications-tooyour-app"></a>Dodaj aplikację tooyour powiadomień wypychanych
1. W **QSTodoService**, Dodaj następujące właściwości hello, aby **AppDelegate** można uzyskać hello klientów urządzeń przenośnych:
   
            public MobileServiceClient GetClient {
            get
            {
                return client;
            }
            private set
            {
                client = value;
            }
        }
2. Dodaj następujące hello `using` instrukcji toohello początku hello **AppDelegate.cs** pliku.
   
        using Microsoft.WindowsAzure.MobileServices;
        using Newtonsoft.Json.Linq;
3. W **AppDelegate**, Zastąp hello **FinishedLaunching** zdarzeń:
   
        public override bool FinishedLaunching(UIApplication application, NSDictionary launchOptions)
        {
            // registers for push for iOS8
            var settings = UIUserNotificationSettings.GetSettingsForTypes(
                UIUserNotificationType.Alert
                | UIUserNotificationType.Badge
                | UIUserNotificationType.Sound,
                new NSSet());
   
            UIApplication.SharedApplication.RegisterUserNotificationSettings(settings);
            UIApplication.SharedApplication.RegisterForRemoteNotifications();
   
            return true;
        }
4. W hello tego samego pliku, Zastąp hello **RegisteredForRemoteNotifications** zdarzeń. W tym kodzie rejestrowania dla powiadomień prostego szablonu, który zostanie wysłany na wszystkich platformach obsługiwanych przez serwer hello.
   
    Aby uzyskać więcej informacji dotyczących szablonów z usługą Notification Hubs, zobacz [szablony](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md).

        public override void RegisteredForRemoteNotifications(UIApplication application, NSData deviceToken)
        {
            MobileServiceClient client = QSTodoService.DefaultService.GetClient;

            const string templateBodyAPNS = "{\"aps\":{\"alert\":\"$(messageParam)\"}}";

            JObject templates = new JObject();
            templates["genericMessage"] = new JObject
            {
                {"body", templateBodyAPNS}
            };

            // Register for push with your mobile app
            var push = client.GetPush();
            push.RegisterAsync(deviceToken, templates);
        }


1. Następnie zastąp hello **DidReceivedRemoteNotification** zdarzeń:
   
        public override void DidReceiveRemoteNotification (UIApplication application, NSDictionary userInfo, Action<UIBackgroundFetchResult> completionHandler)
        {
            NSDictionary aps = userInfo.ObjectForKey(new NSString("aps")) as NSDictionary;
   
            string alert = string.Empty;
            if (aps.ContainsKey(new NSString("alert")))
                alert = (aps [new NSString("alert")] as NSString).ToString();
   
            //show alert
            if (!string.IsNullOrEmpty(alert))
            {
                UIAlertView avAlert = new UIAlertView("Notification", alert, null, "OK", null);
                avAlert.Show();
            }
        }

Aplikacja jest teraz zaktualizowane toosupport powiadomień wypychanych.

## <a name="test"></a>Testowych powiadomień wypychanych w aplikacji
1. Naciśnij klawisz hello **Uruchom** przycisk toobuild hello projekt i uruchomić aplikacji hello w stanie urządzenia z systemem iOS, a następnie kliknij **OK** tooaccept powiadomień wypychanych.
   
   > [!NOTE]
   > Należy jawnie zaakceptować powiadomień wypychanych z aplikacji. To żądanie występuje tylko hello hello aplikacja działa po raz pierwszy.
   > 
   > 
2. W aplikacji hello typu zadania, a następnie kliknij przycisk hello plus (**+**) ikona.
3. Sprawdź, czy powiadomienie o odebraniu, a następnie kliknij przycisk **OK** toodismiss hello powiadomień.
4. Powtórz krok 2 i natychmiast zamknij hello aplikacji, a następnie sprawdź, czy powiadomienie jest widoczne.

W tym samouczku została pomyślnie ukończona.

<!-- Images. -->

<!-- URLs. -->



