---
title: "aplikacji platformy Xamarin.Forms tooyour powiadomień wypychanych aaaAdd | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse Azure usług toosend obejmującego wiele platform wypychania powiadomień tooyour platformy Xamarin.Forms aplikacji."
services: app-service\mobile
documentationcenter: xamarin
author: ysxu
manager: syntaxc4
editor: 
ms.assetid: d9b1ba9a-b3f2-4d12-affc-2ee34311538b
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin
ms.devlang: dotnet
ms.topic: article
ms.date: 10/12/2016
ms.author: yuaxu
ms.openlocfilehash: 9133a0b6dd99c01def525607c20ce5a9c19b9502
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="add-push-notifications-tooyour-xamarinforms-app"></a>Dodawanie aplikacji platformy Xamarin.Forms tooyour powiadomień wypychanych
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a>Omówienie
W tym samouczku, Dodaj wypychania powiadomień tooall hello projektów, które jest wynikiem hello [szybki start platformy Xamarin.Forms](app-service-mobile-xamarin-forms-get-started.md). Oznacza to, że powiadomienie wypychane zostanie wysłane tooall klientów i platform, za każdym razem, gdy wstawieniu rekordu.

Jeśli nie używasz hello pobrany Projekt serwera szybki start, muszą hello pakiet rozszerzenia powiadomień wypychanych. Aby uzyskać więcej informacji, zobacz [pracować z serwera wewnętrznej bazy danych hello .NET SDK usługi Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).

## <a name="prerequisites"></a>Wymagania wstępne
Dla systemu iOS, konieczne będzie [członkostwo w programie dla deweloperów firmy Apple](https://developer.apple.com/programs/ios/) i urządzenie fizyczne z systemem iOS. Witaj [symulatora systemu iOS nie obsługuje powiadomień wypychanych](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/iOS_Simulator_Guide/TestingontheiOSSimulator.html).

## <a name="configure-hub"></a>Konfigurowanie Centrum powiadomień
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <a name="update-hello-server-project-toosend-push-notifications"></a>Zaktualizuj powiadomień wypychanych toosend powitania serwera projektu
[!INCLUDE [app-service-mobile-update-server-project-for-push-template](../../includes/app-service-mobile-update-server-project-for-push-template.md)]

## <a name="configure-and-run-hello-android-project-optional"></a>Konfigurowanie i uruchamianie projektu systemu Android hello (opcjonalnie)
Ukończenie tej sekcji tooenable powiadomień wypychanych dla hello Droid platformy Xamarin.Forms projektu dla systemu Android.

### <a name="enable-firebase-cloud-messaging-fcm"></a>Włącz Firebase Cloud Messaging (FCM)
[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

### <a name="configure-hello-mobile-apps-back-end-toosend-push-requests-by-using-fcm"></a>Skonfiguruj hello Mobile Apps zaplecza toosend wypychania żądania przy użyciu FCM
[!INCLUDE [app-service-mobile-android-configure-push](../../includes/app-service-mobile-android-configure-push.md)]

### <a name="add-push-notifications-toohello-android-project"></a>Dodaj projekt systemu Android toohello powiadomień wypychanych
Witaj zaplecza skonfigurowane z FCM można dodawać składników i kody tooregister klienta toohello z FCM. Można również zarejestrować dla powiadomień wypychanych przy użyciu usługi Azure Notification Hubs za pomocą hello Mobile Apps ponownie zakończyć i otrzymywać powiadomienia.

1. W hello **Droid** projektu, kliknij prawym przyciskiem myszy hello **składniki** folder, a następnie kliknij przycisk **Uzyskaj więcej składników... **. Następnie wyszukaj hello **Google Cloud Messaging Client** składników i dodaj go toohello projektu. Ten składnik obsługuje powiadomień wypychanych dla projektu dla systemu Xamarin Android.
2. Otwórz plik projektu MainActivity.cs hello, a następnie dodaj powitania po instrukcji u góry pliku hello hello:

        using Gcm.Client;
3. Dodaj hello następującego kodu toohello **OnCreate** za wywołanie metody po hello**LoadApplication**:

        try
        {
            // Check tooensure everything's set up right
            GcmClient.CheckDevice(this);
            GcmClient.CheckManifest(this);

            // Register for push notifications
            System.Diagnostics.Debug.WriteLine("Registering...");
            GcmClient.Register(this, PushHandlerBroadcastReceiver.SENDER_IDS);
        }
        catch (Java.Net.MalformedURLException)
        {
            CreateAndShowDialog("There was an error creating hello client. Verify hello URL.", "Error");
        }
        catch (Exception e)
        {
            CreateAndShowDialog(e.Message, "Error");
        }
4. Dodaj nową **CreateAndShowDialog** metody pomocnika, w następujący sposób:

        private void CreateAndShowDialog(String message, String title)
        {
            AlertDialog.Builder builder = new AlertDialog.Builder(this);

            builder.SetMessage (message);
            builder.SetTitle (title);
            builder.Create().Show ();
        }
5. Dodaj hello następującego kodu toohello **MainActivity** klasy:

        // Create a new instance field for this activity.
        static MainActivity instance = null;

        // Return hello current activity instance.
        public static MainActivity CurrentActivity
        {
            get
            {
                return instance;
            }
        }

    To przedstawia bieżący hello **MainActivity** wystąpienie, dlatego można wykonać na powitania głównego wątku interfejsu użytkownika.
6. Inicjowanie hello `instance` zmiennej na początku hello hello **OnCreate** metody, w następujący sposób.

        // Set hello current instance of MainActivity.
        instance = this;
7. Dodaj nowy toohello pliku klasy **Droid** projektu o nazwie `GcmService.cs`i upewnij się, że następujące hello **przy użyciu** instrukcje znajdują się u góry pliku hello hello:

        using Android.App;
        using Android.Content;
        using Android.Media;
        using Android.Support.V4.App;
        using Android.Util;
        using Gcm.Client;
        using Microsoft.WindowsAzure.MobileServices;
        using Newtonsoft.Json.Linq;
        using System;
        using System.Collections.Generic;
        using System.Diagnostics;
        using System.Text;
8. Dodaj następujące żądania uprawnień u góry pliku hello powitania po hello hello **przy użyciu** instrukcje i przed hello **przestrzeni nazw** deklaracji.

        [assembly: Permission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "com.google.android.c2dm.permission.RECEIVE")]
        [assembly: UsesPermission(Name = "android.permission.INTERNET")]
        [assembly: UsesPermission(Name = "android.permission.WAKE_LOCK")]
        //GET_ACCOUNTS is only needed for android versions 4.0.3 and below
        [assembly: UsesPermission(Name = "android.permission.GET_ACCOUNTS")]
9. Dodaj hello następujące przestrzeni nazw toohello definicji klasy.

       [BroadcastReceiver(Permission = Gcm.Client.Constants.PERMISSION_GCM_INTENTS)]
       [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_MESSAGE }, Categories = new string[] { "@PACKAGE_NAME@" })]
       [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_REGISTRATION_CALLBACK }, Categories = new string[] { "@PACKAGE_NAME@" })]
       [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_LIBRARY_RETRY }, Categories = new string[] { "@PACKAGE_NAME@" })]
       public class PushHandlerBroadcastReceiver : GcmBroadcastReceiverBase<GcmService>
       {
           public static string[] SENDER_IDS = new string[] { "<PROJECT_NUMBER>" };
       }

   > [!NOTE]
   > Zastąp **< PROJECT_NUMBER >** wcześniej zapisany numer projektu.    
   >
   >
10. Zastąp hello pusty **GcmService** klas z następującego kodu, który używa nowego odbiornika emisji hello hello:

         [Service]
         public class GcmService : GcmServiceBase
         {
             public static string RegistrationID { get; private set; }

             public GcmService()
                 : base(PushHandlerBroadcastReceiver.SENDER_IDS){}
         }
11. Dodaj hello następującego kodu toohello **GcmService** klasy. Przesłania hello **OnRegistered** obsługi zdarzeń i implementuje **zarejestrować** metody.

        protected override void OnRegistered(Context context, string registrationId)
        {
            Log.Verbose("PushHandlerBroadcastReceiver", "GCM Registered: " + registrationId);
            RegistrationID = registrationId;

            var push = TodoItemManager.DefaultManager.CurrentClient.GetPush();

            MainActivity.CurrentActivity.RunOnUiThread(() => Register(push, null));
        }

        public async void Register(Microsoft.WindowsAzure.MobileServices.Push push, IEnumerable<string> tags)
        {
            try
            {
                const string templateBodyGCM = "{\"data\":{\"message\":\"$(messageParam)\"}}";

                JObject templates = new JObject();
                templates["genericMessage"] = new JObject
                {
                    {"body", templateBodyGCM}
                };

                await push.RegisterAsync(RegistrationID, templates);
                Log.Info("Push Installation Id", push.InstallationId.ToString());
            }
            catch (Exception ex)
            {
                System.Diagnostics.Debug.WriteLine(ex.Message);
                Debugger.Break();
            }
        }

    Zwróć uwagę, że ten kod używa hello `messageParam` parametru w hello szablon rejestracji.
12. Dodaj hello następującego kodu, który implementuje **OnMessage**:

        protected override void OnMessage(Context context, Intent intent)
        {
            Log.Info("PushHandlerBroadcastReceiver", "GCM Message Received!");

            var msg = new StringBuilder();

            if (intent != null && intent.Extras != null)
            {
                foreach (var key in intent.Extras.KeySet())
                    msg.AppendLine(key + "=" + intent.Extras.Get(key).ToString());
            }

            //Store hello message
            var prefs = GetSharedPreferences(context.PackageName, FileCreationMode.Private);
            var edit = prefs.Edit();
            edit.PutString("last_msg", msg.ToString());
            edit.Commit();

            string message = intent.Extras.GetString("message");
            if (!string.IsNullOrEmpty(message))
            {
                createNotification("New todo item!", "Todo item: " + message);
                return;
            }

            string msg2 = intent.Extras.GetString("msg");
            if (!string.IsNullOrEmpty(msg2))
            {
                createNotification("New hub message!", msg2);
                return;
            }

            createNotification("Unknown message details", msg.ToString());
        }

        void createNotification(string title, string desc)
        {
            //Create notification
            var notificationManager = GetSystemService(Context.NotificationService) as NotificationManager;

            //Create an intent tooshow ui
            var uiIntent = new Intent(this, typeof(MainActivity));

            //Use Notification Builder
            NotificationCompat.Builder builder = new NotificationCompat.Builder(this);

            //Create hello notification
            //we use hello pending intent, passing our ui intent over which will get called
            //when hello notification is tapped.
            var notification = builder.SetContentIntent(PendingIntent.GetActivity(this, 0, uiIntent, 0))
                    .SetSmallIcon(Android.Resource.Drawable.SymActionEmail)
                    .SetTicker(title)
                    .SetContentTitle(title)
                    .SetContentText(desc)

                    //Set hello notification sound
                    .SetSound(RingtoneManager.GetDefaultUri(RingtoneType.Notification))

                    //Auto cancel will remove hello notification once hello user touches it
                    .SetAutoCancel(true).Build();

            //Show hello notification
            notificationManager.Notify(1, notification);
        }

    Obsługuje przychodzące powiadomienia i wysyła je toobe Menedżera powiadomień toohello wyświetlane.
13. **GcmServiceBase** wymaga również tooimplement hello **OnUnRegistered** i **OnError** metody obsługi, które można wykonać w następujący sposób:

        protected override void OnUnRegistered(Context context, string registrationId)
        {
            Log.Error("PushHandlerBroadcastReceiver", "Unregistered RegisterationId : " + registrationId);
        }

        protected override void OnError(Context context, string errorId)
        {
            Log.Error("PushHandlerBroadcastReceiver", "GCM Error: " + errorId);
        }

Teraz są gotowe testu powiadomień wypychanych w aplikacji hello uruchomionej na urządzeniu z systemem Android lub hello emulatora.

### <a name="test-push-notifications-in-your-android-app"></a>Testowych powiadomień wypychanych w aplikacji systemu Android
Witaj pierwsze dwa kroki są wymagane tylko wtedy, gdy w przypadku testowania emulatora.

1. Upewnij się, że jest wdrażany tooor debugowania na urządzeniu wirtualnym, który ma ustawić jako cel hello interfejsy API Google, jak pokazano poniżej, w Menedżerze urządzeń wirtualnych systemu Android hello.
2. Dodanie urządzenia Android toohello konto Google, klikając **aplikacje** > **ustawienia** > **Dodaj konto**. Następnie wykonaj hello monity tooadd istniejące urządzenie toohello konto Google lub toocreate nowy.
3. W programie Visual Studio lub Xamarin Studio kliknij prawym przyciskiem myszy hello **Droid** projekt i kliknij przycisk **Ustaw jako projekt startowy**.
4. Kliknij przycisk **Uruchom** toobuild hello projekt i uruchomić aplikacji hello na urządzeniu z systemem Android lub w emulatorze.
5. W aplikacji hello typu zadania, a następnie kliknij przycisk hello plus (**+**) ikona.
6. Sprawdź, czy otrzyma powiadomienie po dodaniu elementu.

## <a name="configure-and-run-hello-ios-project-optional"></a>Konfigurowanie i uruchamianie projektu iOS hello (opcjonalnie)
Ta sekcja dotyczy uruchamiania projektu Xamarin iOS powitania dla urządzeń z systemem iOS. Jeśli nie pracujesz z urządzeniami z systemem iOS, możesz pominąć tę sekcję.

[!INCLUDE [Enable Apple Push Notifications](../../includes/enable-apple-push-notifications.md)]

#### <a name="configure-hello-notification-hub-for-apns"></a>Konfigurowanie Centrum powiadomień hello w przypadku usługi APNS
[!INCLUDE [app-service-mobile-apns-configure-push](../../includes/app-service-mobile-apns-configure-push.md)]

Następnie skonfiguruj ustawienia projektu iOS hello w programie Xamarin Studio lub Visual Studio.

[!INCLUDE [app-service-mobile-xamarin-ios-configure-project](../../includes/app-service-mobile-xamarin-ios-configure-project.md)]

#### <a name="add-push-notifications-tooyour-ios-app"></a>Dodawanie aplikacji dla systemu iOS tooyour powiadomień wypychanych
1. W hello **iOS** projektu, otwórz AppDelegate.cs i Dodaj powitania po instrukcji toohello początku hello pliku kodu.

        using Newtonsoft.Json.Linq;
2. W hello **AppDelegate** klasy, Dodaj zastąpienie hello **RegisteredForRemoteNotifications** tooregister zdarzenia dla powiadomień:

        public override void RegisteredForRemoteNotifications(UIApplication application,
            NSData deviceToken)
        {
            const string templateBodyAPNS = "{\"aps\":{\"alert\":\"$(messageParam)\"}}";

            JObject templates = new JObject();
            templates["genericMessage"] = new JObject
                {
                  {"body", templateBodyAPNS}
                };

            // Register for push with your mobile app
            Push push = TodoItemManager.DefaultManager.CurrentClient.GetPush();
            push.RegisterAsync(deviceToken, templates);
        }
3. W **AppDelegate**, także dodać następujące zastąpienie hello hello **DidReceiveRemoteNotification** obsługi zdarzeń:

        public override void DidReceiveRemoteNotification(UIApplication application,
            NSDictionary userInfo, Action<UIBackgroundFetchResult> completionHandler)
        {
            NSDictionary aps = userInfo.ObjectForKey(new NSString("aps")) as NSDictionary;

            string alert = string.Empty;
            if (aps.ContainsKey(new NSString("alert")))
                alert = (aps[new NSString("alert")] as NSString).ToString();

            //show alert
            if (!string.IsNullOrEmpty(alert))
            {
                UIAlertView avAlert = new UIAlertView("Notification", alert, null, "OK", null);
                avAlert.Show();
            }
        }

    Ta metoda obsługuje przychodzące powiadomienia aplikacji hello jest uruchomiona.
4. W hello **AppDelegate** klasy, Dodaj hello następującego kodu toohello **FinishedLaunching** metody:

        // Register for push notifications.
        var settings = UIUserNotificationSettings.GetSettingsForTypes(
            UIUserNotificationType.Alert
            | UIUserNotificationType.Badge
            | UIUserNotificationType.Sound,
            new NSSet());

        UIApplication.SharedApplication.RegisterUserNotificationSettings(settings);
        UIApplication.SharedApplication.RegisterForRemoteNotifications();

    Umożliwia to obsługę zdalnego powiadomienia i żądania push rejestracji.

Aplikacja jest teraz zaktualizowane toosupport powiadomień wypychanych.

#### <a name="test-push-notifications-in-your-ios-app"></a>Testowych powiadomień wypychanych w aplikacji systemu iOS
1. Kliknij prawym przyciskiem myszy projekt iOS hello, a następnie kliknij przycisk **Ustaw jako projekt startowy**.
2. Naciśnij klawisz hello **Uruchom** przycisk lub **F5** w programie Visual Studio toobuild hello projekt i uruchomić aplikacji hello w urządzeniu z systemem iOS. Następnie kliknij przycisk **OK** tooaccept powiadomień wypychanych.

   > [!NOTE]
   > Należy jawnie zaakceptować powiadomień wypychanych z aplikacji. To żądanie występuje tylko hello hello aplikacja działa po raz pierwszy.
   >
   >
3. W aplikacji hello typu zadania, a następnie kliknij przycisk hello plus (**+**) ikona.
4. Sprawdź, czy otrzyma powiadomienie, a następnie kliknij **OK** toodismiss hello powiadomień.

## <a name="configure-and-run-windows-projects-optional"></a>Konfigurowanie i uruchamianie projekty systemu Windows (opcjonalnie)
Ta sekcja dotyczy uruchamiania aplikacji platformy Xamarin.Forms i WinPhone81 projektów dla urządzeń z systemem Windows hello. Te kroki również obsługiwać projekty systemu Windows platformy Uniwersalnej. Jeśli nie pracujesz z urządzeniami z systemem Windows, możesz pominąć tę sekcję.

#### <a name="register-your-windows-app-for-push-notifications-with-windows-notification-service-wns"></a>Rejestrowanie aplikacji systemu Windows dla powiadomień wypychanych z powiadomienia usługi WNS (Windows)
[!INCLUDE [app-service-mobile-register-wns](../../includes/app-service-mobile-register-wns.md)]

#### <a name="configure-hello-notification-hub-for-wns"></a>Konfigurowanie Centrum powiadomień hello przypadku usługi WNS
[!INCLUDE [app-service-mobile-configure-wns](../../includes/app-service-mobile-configure-wns.md)]

#### <a name="add-push-notifications-tooyour-windows-app"></a>Dodawanie aplikacji dla systemu Windows tooyour powiadomień wypychanych
1. W programie Visual Studio Otwórz **App.xaml.cs** w systemie Windows projektu i dodaj następujące instrukcje hello.

        using Newtonsoft.Json.Linq;
        using Microsoft.WindowsAzure.MobileServices;
        using System.Threading.Tasks;
        using Windows.Networking.PushNotifications;
        using <your_TodoItemManager_portable_class_namespace>;

    Zastąp `<your_TodoItemManager_portable_class_namespace>` z przestrzenią nazw hello przenośne projektu zawierającego hello `TodoItemManager` klasy.
2. W pliku App.xaml.cs Dodaj następujące hello **InitNotificationsAsync** metody:

        private async Task InitNotificationsAsync()
        {
            var channel = await PushNotificationChannelManager
                .CreatePushNotificationChannelForApplicationAsync();

            const string templateBodyWNS =
                "<toast><visual><binding template=\"ToastText01\"><text id=\"1\">$(messageParam)</text></binding></visual></toast>";

            JObject headers = new JObject();
            headers["X-WNS-Type"] = "wns/toast";

            JObject templates = new JObject();
            templates["genericMessage"] = new JObject
            {
                {"body", templateBodyWNS},
                {"headers", headers} // Needed for WNS.
            };

            await TodoItemManager.DefaultManager.CurrentClient.GetPush()
                .RegisterAsync(channel.Uri, templates);
        }

    Ta metoda pobiera kanału powiadomień wypychanych hello i rejestruje powiadomienia szablonu tooreceive szablonu z Centrum powiadomień. Powiadomienie szablonu, który obsługuje *messageParam* będą dostarczane toothis klienta.
3. W pliku App.xaml.cs aktualizacji hello **OnLaunched** definicję metody obsługi zdarzeń, dodając hello `async` modyfikator. Następnie dodaj powitania po wiersz kodu na końcu hello metody hello:

        await InitNotificationsAsync();

    Dzięki temu, że rejestracji powiadomień wypychanych hello jest tworzony lub odświeżyć za każdym razem, gdy aplikacja hello jest uruchamiana. Ważne jest, toodo to tooguarantee, który hello kanału wypychanych usługi WNS jest zawsze aktywna.  
4. W Eksploratorze rozwiązań programu Visual Studio Otwórz hello **Package.appxmanifest** pliku, a następnie ustaw **wyskakujące funkcją** za**tak** w obszarze **powiadomienia**.
5. Tworzenie aplikacji hello i sprawdź, czy użytkownik nie ma błędów. Twoja aplikacja kliencka powinna teraz zarejestrować hello szablonu odbieranie powiadomień z hello pewno zakończyć Mobile Apps ponownie. W tej sekcji należy powtórzyć dla każdego projektu systemu Windows w rozwiązaniu.

#### <a name="test-push-notifications-in-your-windows-app"></a>Testowych powiadomień wypychanych w aplikacji systemu Windows
1. W programie Visual Studio, kliknij prawym przyciskiem myszy projekt dla systemu Windows, a następnie kliknij przycisk **Ustaw jako projekt startowy**.
2. Naciśnij klawisz hello **Uruchom** przycisk toobuild hello projekt i uruchomić aplikacji hello.
3. W aplikacji hello, wpisz nazwę nowego zadania do wykonania, a następnie kliknij przycisk hello plus (**+**) tooadd ikonę go.
4. Sprawdź, czy otrzyma powiadomienie po dodaniu elementu hello.

## <a name="next-steps"></a>Następne kroki
Dodatkowe informacje na temat powiadomień wypychanych:

* [Diagnozowanie problemów powiadomień wypychanych](../notification-hubs/notification-hubs-push-notification-fixer.md)  
  Istnieją różne przyczyny, dlaczego powiadomienia mogą pobrać usunięte lub nie kończą na urządzeniach. W tym temacie pokazano, jak tooanalyze i ustalenie potrzebnej głównego hello. Przyczyna niepowodzenia powiadomień wypychanych.

Można też nadal tooone hello następujące samouczki:

* [Dodaj aplikację tooyour uwierzytelniania](app-service-mobile-xamarin-forms-get-started-users.md)  
  Dowiedz się, jak tooauthenticate użytkowników aplikacji przy użyciu dostawcy tożsamości.
* [Włączanie synchronizacji w trybie offline dla aplikacji](app-service-mobile-xamarin-forms-get-started-offline-data.md)  
  Dowiedz się, jak zaplecza tooadd obsługi w trybie offline dla aplikacji przy użyciu aplikacji mobilnej. Z synchronizacji w trybie offline, użytkownicy mogą korzystać z aplikacji mobilnej&mdash;przeglądanie, dodawanie lub modyfikowanie danych&mdash;nawet wtedy, gdy istnieje połączenie sieciowe.

<!-- Images. -->

<!-- URLs. -->
[Install Xcode]: https://go.microsoft.com/fwLink/p/?LinkID=266532
[Xcode]: https://go.microsoft.com/fwLink/?LinkID=266532
[apns object]: http://go.microsoft.com/fwlink/p/?LinkId=272333
