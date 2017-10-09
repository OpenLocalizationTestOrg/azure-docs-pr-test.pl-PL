---
title: "aaaiOS powiadomień wypychanych przy użyciu usługi Notification Hubs dla aplikacji platformy Xamarin | Dokumentacja firmy Microsoft"
description: "Z tego samouczka dowiesz się, jak toosend usługi Azure Notification Hubs toouse wypychanie powiadomień tooa Xamarin iOS aplikacji."
services: notification-hubs
keywords: "powiadomienia wypychane w systemie ios, wiadomości wypychane, powiadomienia wypychane, wiadomość wypychana"
documentationcenter: xamarin
author: ysxu
manager: erikre
editor: 
ms.assetid: 4d4dfd42-c5a5-4360-9d70-7812f96924d2
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-ios
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 8db60338047dd53074b4d3d4bb127aa6d9f13a25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="ios-push-notifications-with-notification-hubs-for-xamarin-apps"></a>Wysyłanie powiadomień wypychanych do aplikacji platformy Xamarin dla systemu iOS przy użyciu usługi Notification Hubs
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a>Omówienie
> [!IMPORTANT]
> toocomplete tego samouczka, musi mieć aktywne konto platformy Azure. Jeśli go nie masz, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut. Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-ios-get-started).
> 
> 

Ten samouczek pokazuje, jak toosend usługi Azure Notification Hubs toouse wypychanych aplikacji dla systemu iOS tooan powiadomienia.
Utworzysz pustą aplikację platformy Xamarin.iOS służącą do odbierania powiadomień wypychanych przy użyciu hello [Apple Push Notification Service (APNs)](https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/APNSOverview.html). Po zakończeniu będziesz w stanie toouse Twojego toobroadcast Centrum powiadomień wypychanych powiadomienia tooall hello urządzeń z tą aplikacją. Witaj gotowy kod jest dostępny w hello [aplikacji NotificationHubs] [ GitHub] próbki.

W tym samouczku przedstawiono scenariusz wysyłania powiadomień wypychanych prostego powitania z usługą Notification Hubs.

## <a name="prerequisites"></a>Wymagania wstępne
Ten samouczek wymaga następujących hello:

* [Xcode 6.0][Install Xcode]
* Urządzenie zgodne z systemem iOS 7.0 (lub nowszą wersją)
* Członkostwo w programie dla deweloperów systemu iOS
* [Program Xamarin Studio]
  
  > [!NOTE]
  > Ze względu na wymagania dotyczące konfiguracji powiadomień wypychanych systemu iOS należy wdrożyć i przetestować aplikację przykładową hello na urządzenie fizyczne z systemem iOS (iPhone i iPad) zamiast w symulatorze hello.
  > 
  > 

Wykonanie czynności opisanych w tym samouczku jest wymaganiem wstępnym dla wszystkich innych samouczków usług Notification Hubs dotyczących aplikacji platformy Xamarin.iOS.

[!INCLUDE [Notification Hubs Enable Apple Push Notifications](../../includes/notification-hubs-enable-apple-push-notifications.md)]

## <a name="configure-your-notification-hub"></a>Konfigurowanie centrum powiadomień
Ta sekcja przeprowadzi Cię przez proces tworzenia nowego centrum powiadomień i konfigurowania uwierzytelniania w usłudze APNS przy użyciu hello **.p12** utworzony certyfikat wypychania. Jeśli chcesz toouse Centrum powiadomień, które zostały już utworzone, możesz pominąć toostep 5.

[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="7">

<li>

<p>Ponieważ chcemy tooconfigure hello APNS połączenia w hello portalu Azure Otwórz ustawienia Centrum powiadomień, kliknij Hub na <b>usługi powiadomień</b>, a następnie kliknij przycisk hello <b>Apple (APNS)</b> element na liście hello. Po zakończeniu kliknij <b>Przekaż certyfikat</b> i wybierz hello <b>.p12</b> certyfikat wyeksportowany wcześniej, a także hello hasło dla certyfikatu hello.</p>

<p>Upewnij się, że tooselect <b>piaskownicy</b> trybu, ponieważ będą wysyłane wypychania wiadomości w środowisku projektowym. Należy używać tylko hello <b>produkcji</b> toosend toousers powiadomień wypychanych, którzy kupili już twoją aplikację w sklepie hello ustawienie.</p>
</li>
</ol>
&emsp;&emsp;![](./media/notification-hubs-ios-get-started/notification-hubs-apns.png)

&emsp;&emsp;![](./media/notification-hubs-ios-get-started/notification-hubs-sandbox.png)

Centrum powiadomień jest teraz skonfigurowany toowork przy użyciu usługi APNS i mieć tooregister ciągów połączenia hello aplikacji oraz wysyłać powiadomienia wypychane.

## <a name="connect-your-app-toohello-notification-hub"></a>Łączenie aplikacji toohello Centrum powiadomień
#### <a name="create-a-new-project"></a>Tworzenie nowego projektu
1. W programie Xamarin Studio Utwórz nowy projekt dla systemu iOS, a następnie wybierz hello **Unified API** > **pojedynczą aplikacją widoku** szablonu.
   
     ![Xamarin Studio — wybieranie typu aplikacji][31]
2. Dodaj odwołanie do składnika Azure Messaging toohello. W widoku Solution hello, kliknij prawym przyciskiem myszy hello **składniki** folderu projektu i wybierz polecenie **Uzyskaj więcej składników**. Wyszukaj hello **Azure Messaging** składników i Dodaj hello składnika tooyour projektu.
3. W **AppDelegate.cs**, Dodaj następujące hello instrukcję using:
   
        using WindowsAzure.Messaging;
4. Zadeklaruj wystąpienie **SBNotificationHub**:
   
        private SBNotificationHub Hub { get; set; }
5. Utwórz **Constants.cs** klasy z hello następujące zmienne:
   
        // Azure app-specific connection string and hub path
        public const string ConnectionString = "<Azure connection string>";
        public const string NotificationHubPath = "<Azure hub path>";
6. W **AppDelegate.cs**, zaktualizuj **FinishedLaunching()** toomatch hello poniżej:
   
        public override bool FinishedLaunching(UIApplication application, NSDictionary launchOptions)
        {
            if (UIDevice.CurrentDevice.CheckSystemVersion (8, 0)) {
                var pushSettings = UIUserNotificationSettings.GetSettingsForTypes (
                       UIUserNotificationType.Alert | UIUserNotificationType.Badge | UIUserNotificationType.Sound,
                       new NSSet ());
   
                UIApplication.SharedApplication.RegisterUserNotificationSettings (pushSettings);
                UIApplication.SharedApplication.RegisterForRemoteNotifications ();
            } else {
                UIRemoteNotificationType notificationTypes = UIRemoteNotificationType.Alert | UIRemoteNotificationType.Badge | UIRemoteNotificationType.Sound;
                UIApplication.SharedApplication.RegisterForRemoteNotificationTypes (notificationTypes);
            }
   
            return true;
        }
7. Zastąpienie hello **RegisteredForRemoteNotifications()** metody w **AppDelegate.cs**:
   
        public override void RegisteredForRemoteNotifications(UIApplication application, NSData deviceToken)
        {
            Hub = new SBNotificationHub(Constants.ConnectionString, Constants.NotificationHubPath);
   
            Hub.UnregisterAllAsync (deviceToken, (error) => {
                if (error != null)
                {
                    Console.WriteLine("Error calling Unregister: {0}", error.ToString());
                    return;
                }
   
                NSSet tags = null; // create tags if you want
                Hub.RegisterNativeAsync(deviceToken, tags, (errorCallback) => {
                    if (errorCallback != null)
                        Console.WriteLine("RegisterNativeAsync error: " + errorCallback.ToString());
                });
            });
        }
8. Zastąpienie hello **ReceivedRemoteNotification()** metody w **AppDelegate.cs**:
   
        public override void ReceivedRemoteNotification(UIApplication application, NSDictionary userInfo)
        {
            ProcessNotification(userInfo, false);
        }
9. Utwórz następujące hello **ProcessNotification()** metody w **AppDelegate.cs**:
   
        void ProcessNotification(NSDictionary options, bool fromFinishedLaunching)
        {
            // Check toosee if hello dictionary has hello aps key.  This is hello notification payload you would have sent
            if (null != options && options.ContainsKey(new NSString("aps")))
            {
                //Get hello aps dictionary
                NSDictionary aps = options.ObjectForKey(new NSString("aps")) as NSDictionary;
   
                string alert = string.Empty;
   
                //Extract hello alert text
                // NOTE: If you're using hello simple alert by just specifying
                // "  aps:{alert:"alert msg here"}  ", this will work fine.
                // But if you're using a complex alert with Localization keys, etc.,
                // your "alert" object from hello aps dictionary will be another NSDictionary.
                // Basically hello JSON gets dumped right into a NSDictionary,
                // so keep that in mind.
                if (aps.ContainsKey(new NSString("alert")))
                    alert = (aps [new NSString("alert")] as NSString).ToString();
   
                //If this came from hello ReceivedRemoteNotification while hello app was running,
                // we of course need toomanually process things like hello sound, badge, and alert.
                if (!fromFinishedLaunching)
                {
                    //Manually show an alert
                    if (!string.IsNullOrEmpty(alert))
                    {
                        UIAlertView avAlert = new UIAlertView("Notification", alert, null, "OK", null);
                        avAlert.Show();
                    }
                }
            }
        }
   
   > [!NOTE]
   > Możesz wybrać toooverride **FailedToRegisterForRemoteNotifications()** toohandle sytuacjach, takich jak brak połączenia z siecią. Jest to szczególnie istotne, gdzie hello użytkownik może uruchomić aplikację w trybie offline (np. w trybie Samolotowym) i ma wypychania toohandle wiadomości scenariusze tooyour określonych aplikacji.
   > 
   > 
10. Uruchamianie aplikacji hello na urządzeniu.

## <a name="sending-push-notifications"></a>Wysyłanie powiadomień wypychanych
Możesz przetestować odbieranie powiadomień wypychanych w aplikacji, wysyłając powiadomienia w hello [Azure Portal] za pośrednictwem hello **wysyłanie testowe** możliwości w hello **Rozwiązywanie problemów** zestaw narzędzi, bezpośrednio w hello stronie Centrum powiadomień, jak pokazano na powitania ekranu poniżej.

![](./media/notification-hubs-ios-get-started/notification-hubs-test-send.png)

Powiadomienia wypychane są zwykle wysyłane za pośrednictwem usługi zaplecza, takiej jak Mobile Services czy ASP.NET, z użyciem zgodnej biblioteki. Umożliwia także hello interfejsu API REST bezpośrednio wiadomości wypychanych toosend, jeśli biblioteka nie jest dostępna w danym scenariuszu. 

W tym samouczku będziemy Zachowaj prostotę i przedstawiono testowanie aplikacji klienckiej przez wysyłanie powiadomień dotyczących usługi notification hubs w aplikacji konsoli usługi zaplecza przy użyciu hello zestawu .NET SDK. Firma Microsoft zaleca hello [toousers powiadomienia toopush użyciu usługi Notification Hubs](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) samouczka jako hello następnego kroku do wysyłania powiadomień z zaplecza ASP.NET. Jednak po podejścia hello może służyć do wysyłania powiadomień:

* **Interfejs REST**: powiadomienia wypychane mogą być obsługiwane na dowolnej platformie zaplecza za pomocą hello [interfejsu REST](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx).
* **Microsoft Azure powiadomień koncentratory .NET SDK**: W hello Menedżera pakietów Nuget dla programu Visual Studio, uruchom [Install-Package Microsoft.Azure.NotificationHubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).
* **Node.js** : [jak toouse centra powiadomień w oprogramowaniu Node.js](notification-hubs-nodejs-push-notification-tutorial.md).

**Aplikacje mobilne**: na przykład jak toosend powiadomień z zaplecza Azure App Service Mobile Apps, który jest zintegrowany z usługą Notification Hubs, zobacz [aplikacji mobilnej tooyour powiadomień wypychanych Dodaj](../app-service-mobile/app-service-mobile-ios-get-started-push.md).

* **Java / PHP**: przykład sposobu toosend powiadomień wypychanych przy użyciu hello interfejsów API REST, zobacz "jak toouse usługi Notification Hubs za pomocą języka Java/PHP" ([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md)).

#### <a name="optional-send-push-notifications-from-a-net-console-app"></a>(Opcjonalnie) Wysyłanie powiadomień wypychanych z poziomu aplikacji konsoli .NET
W tej sekcji wyślemy powiadomienia wypychane za pomocą prostej aplikacji konsoli .NET. Celach hello tego przykładu przeniesiemy się tooa środowiska projektowego systemu Windows, który ma już zainstalowanego programu Visual Studio.

1. W programie Visual Studio utwórz nową aplikację konsoli języka Visual C#:
   
       ![Visual Studio - Create a new console application][213]
2. W programie Visual Studio kliknij kolejno pozycje **Narzędzia**, **Menedżer pakietów NuGet**, **Konsola menedżera pakietów**.
   
    konsoli Menedżera pakietów Hello powinna zostać wyświetlona zadokowanych toohello dolnej części obszaru roboczego programu Visual Studio.
3. W oknie konsoli Menedżera pakietów hello, ustaw hello **domyślny projekt** tooyour nowy projekt aplikacji konsoli, a następnie w oknie konsoli hello, wykonaj następujące polecenie hello:
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    Spowoduje to dodanie toohello odwołanie do zestawu SDK usługi Azure Notification Hubs za pomocą hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">pakietu Microsoft.Azure.Notification Hubs NuGet</a>.
   
    ![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-package-manager.png)
4. Otwórz hello `Program.cs` i dodaj następujące hello `using` instrukcji zapewnienie, że możemy użyć Azure klasy i funkcje w ramach klasy głównej:
   
        using Microsoft.Azure.NotificationHubs;
5. W Twojej `Program` klasy, Dodaj następujące metody hello (nie zapomnij tooreplace hello **ciąg połączenia** i **nazwy centrum**):
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            var alert = "{\"aps\":{\"alert\":\"Hello from .NET!\"}}";
            await hub.SendAppleNativeNotificationAsync(alert);
        }
6. Dodaj hello następujące wiersze w Twojej `Main` metody:
   
         SendNotificationAsync();
         Console.ReadLine();
7. Naciśnij klawisz hello F5 klucza toorun hello aplikacji. W ciągu kilku sekund na urządzeniu powinno zostać wyświetlone powiadomienie wypychane. Czy korzystasz z sieci Wi-Fi i sieci danych komórkowych, upewnij się, że masz aktywne połączenie internetowe na urządzeniu hello.

Wszystkie możliwe ładunki hello można znaleźć w hello Apple [lokalnych i wypychanych Podręcznik programowania powiadomień].

#### <a name="optional-send-notifications-from-a-mobile-service"></a>(Opcjonalnie) Wysyłanie powiadomień wypychanych z poziomu usługi mobilnej
W tej sekcji wyślemy powiadomienia wypychane za pomocą usługi mobilnej, za pośrednictwem skryptu węzła.

toosend powiadomienia za pomocą usługi mobilnej, wykonaj [wprowadzenie do usług Mobile Services], a następnie:

1. Zaloguj się toohello [klasycznego portalu Azure]i wybierz usługę mobilną.
2. Wybierz hello **harmonogramu** kartę w górnej części hello.
   
       ![Azure Classic Portal - Scheduler][215]
3. Utwórz nowe zadanie zaplanowane, wstaw nazwę i wybierz opcję **Na żądanie**.
   
       ![Azure Classic Portal - Create new job][216]
4. Po utworzeniu zadania powitania kliknij nazwę zadania hello. Następnie kliknij przycisk hello **skryptu** kartę na górnym pasku hello.
5. Wstaw hello następującego skryptu w funkcji harmonogramu. Wprowadź symbole zastępcze hello tooreplace się z powiadomienia Centrum nazwy i hello parametrów połączenia dla *DefaultFullSharedAccessSignature* uzyskany wcześniej. Kliknij pozycję **Zapisz**.
   
        var azure = require('azure');
        var notificationHubService = azure.createNotificationHubService('<Hubname>', '<SAS Full access >');
        notificationHubService.apns.send(
            null,
            {"aps":
                {
                  "alert": "Hello from Mobile Services!"
                }
            },
            function (error)
            {
                if (!error) {
                    console.warn("Notification successful");
                }
            }
        );
6. Kliknij przycisk **uruchom raz** na powitania dolnym pasku. Na urządzeniu powinien zostać wyświetlony alert.

## <a name="next-steps"></a>Następne kroki
W tym prostym przykładzie wysłano tooall powiadomień wypychanych urządzeń z systemem iOS. W kolejności tootarget określonych użytkowników, zobacz samouczek toohello [toousers powiadomienia toopush użyciu usługi Notification Hubs]. Jeśli chcesz toosegment użytkowników na grupy zainteresowań, możesz przeczytać [toosend użyciu usługi Notification Hubs fundamentalne wiadomości]. Dowiedz się więcej na temat toouse centra powiadomień w [wskazówki dotyczące usługi Notification Hubs] w hello [iOS centra powiadomień w sposób toofor].

<!-- Images. -->

[213]: ./media/partner-xamarin-notification-hubs-ios-get-started/notification-hub-create-console-app.png

[215]: ./media/partner-xamarin-notification-hubs-ios-get-started/notification-hub-scheduler1.png
[216]: ./media/partner-xamarin-notification-hubs-ios-get-started/notification-hub-scheduler2.png


[31]: ./media/partner-xamarin-notification-hubs-ios-get-started/notification-hub-create-ios-app.png




<!-- URLs. -->
[Mobile Services iOS SDK]: http://go.microsoft.com/fwLink/?LinkID=266533
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253

[wprowadzenie do usług Mobile Services]: /develop/mobile/tutorials/get-started-xamarin-ios
[klasycznego portalu Azure]: https://manage.windowsazure.com/
[wskazówki dotyczące usługi Notification Hubs]: http://msdn.microsoft.com/library/jj927170.aspx
[iOS centra powiadomień w sposób toofor]: http://msdn.microsoft.com/library/jj927168.aspx
[Install Xcode]: https://go.microsoft.com/fwLink/p/?LinkID=266532
[iOS Provisioning Portal]: http://go.microsoft.com/fwlink/p/?LinkId=272456

[toousers powiadomienia toopush użyciu usługi Notification Hubs]: /manage/services/notification-hubs/notify-users-aspnet
[toosend użyciu usługi Notification Hubs fundamentalne wiadomości]: /manage/services/notification-hubs/breaking-news-dotnet

[lokalnych i wypychanych Podręcznik programowania powiadomień]:https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/HandlingRemoteNotifications.html#//apple_ref/doc/uid/TP40008194-CH6-SW1
[Apple Push Notification Service]: http://go.microsoft.com/fwlink/p/?LinkId=272584

[Azure Mobile Services Component]: http://components.xamarin.com/view/azure-mobile-services/
[GitHub]: http://go.microsoft.com/fwlink/p/?LinkId=331329
[Program Xamarin Studio]: http://xamarin.com/download
[WindowsAzure.Messaging]: https://github.com/infosupport/WindowsAzure.Messaging.iOS
[Azure Portal]: https://portal.azure.com
