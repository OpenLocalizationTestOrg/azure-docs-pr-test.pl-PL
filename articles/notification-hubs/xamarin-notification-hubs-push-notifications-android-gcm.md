---
title: "aaaGet pracę z usługą Notification Hubs dla aplikacji platformy Xamarin.Android | Dokumentacja firmy Microsoft"
description: "Z tego samouczka dowiesz się, jak toosend usługi Azure Notification Hubs toouse push tooa powiadomień aplikacji dla systemu Xamarin Android."
author: ysxu
manager: erikre
editor: 
services: notification-hubs
documentationcenter: xamarin
ms.assetid: 0be600fe-d5f3-43a5-9e5e-3135c9743e54
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-android
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: c5c7ead9a9381ab9fb6bbe86e930a8a9254813d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-notification-hubs-with-xamarin-for-android"></a>Wprowadzenie do usługi Notification Hubs dla systemu Android na platformie Xamarin
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a>Omówienie
Ten samouczek pokazuje, jak toosend usługi Azure Notification Hubs toouse push aplikacji platformy Xamarin.Android tooa powiadomienia.
Utworzysz pustą aplikację platformy Xamarin.Android służącą do odbierania powiadomień wypychanych przy użyciu usługi Google Cloud Messaging (GCM). Po zakończeniu będziesz w stanie toouse Twojego toobroadcast Centrum powiadomień wypychanych powiadomienia tooall hello urządzeń z tą aplikacją. Witaj gotowy kod jest dostępny w hello [aplikacji NotificationHubs] [ GitHub] próbki.

W tym samouczku przedstawiono hello Prosty scenariusz wysyłania przy użyciu usługi Notification Hubs.

## <a name="before-you-begin"></a>Przed rozpoczęciem
[!INCLUDE [notification-hubs-hero-slug](../../includes/notification-hubs-hero-slug.md)]

Kod ukończyć powitalnych dla tego samouczka można znaleźć w witrynie GitHub [tutaj](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/Xamarin/GetStartedXamarinAndroid).

## <a name="prerequisites"></a>Wymagania wstępne
Ten samouczek wymaga następujących hello:

* Program Visual Studio z platformą Xamarin w systemie Windows lub program Xamarin Studio w systemie Mac OS X. Kompletne instrukcje instalacji można znaleźć w temacie [Konfigurowanie i instalowanie oprogramowania Visual Studio i Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).
* Aktywne konto Google
* [Składnik Azure Messaging]
* [Składnik Google Cloud Messaging Client]

Wykonanie czynności opisanych w tym samouczku jest wymaganiem wstępnym dla wszystkich innych samouczków usługi Notification Hubs dotyczących aplikacji platformy Xamarin.Android.

> [!IMPORTANT]
> toocomplete tego samouczka, musi mieć aktywne konto platformy Azure. Jeśli go nie masz, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut. Aby uzyskać szczegółowe informacje, zobacz [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A9C9624B5&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-android-get-started%2F).
> 
> 

## <a name="enable-google-cloud-messaging"></a>Włączanie usługi Google Cloud Messaging
[!INCLUDE [mobile-services-enable-Google-cloud-messaging](../../includes/mobile-services-enable-google-cloud-messaging.md)]

## <a name="configure-your-notification-hub"></a>Konfigurowanie centrum powiadomień
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="7">

<li><p>Kliknij przycisk hello <b>Konfiguruj</b> u góry hello, wprowadź hello <b>klucz interfejsu API</b> wartość uzyskaną w poprzedniej sekcji hello, a następnie kliknij przycisk <b>zapisać</b>.</p>
</li>
</ol>
&emsp;&emsp;![](./media/notification-hubs-android-get-started/notification-hub-configure-android.png)

Centrum powiadomień jest teraz skonfigurowany toowork z usługą GCM i masz tooboth ciągów połączenia hello zarejestrować swoje powiadomienia tooreceive aplikacji i toosend powiadomień wypychanych.

## <a name="connect-your-app-toohello-notification-hub"></a>Łączenie aplikacji toohello Centrum powiadomień
### <a name="create-a-new-project"></a>Tworzenie nowego projektu
1. W programie Xamarin Studio kliknij kolejno pozycje **New Solution** (Nowe rozwiązanie), **Android App** (Aplikacja dla systemu Android) i **Next** (Dalej).
   
      ![](./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-xamarin-android-project1.png)

2. Wprowadź nazwę aplikacji w polu **App Name** i identyfikator w polu **Identifier**. Kliknij przycisk hello **Platforms docelowej** toosupport a następnie kliknij przycisk **dalej** i **Utwórz**.
   
      ![](./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-xamarin-android-project2.png)

    Spowoduje to utworzenie nowego projektu dla systemu Android.

1. Otwórz właściwości projektu hello prawym przyciskiem myszy nowy projekt w widoku Solution hello i wybierając pozycję **opcje**. Wybierz hello **aplikacji systemu Android** elementu hello **kompilacji** sekcji.
   
    Upewnij się, że hello pierwszą literę z **nazwy pakietu** jest pisana małymi literami.
   
   > [!IMPORTANT]
   > pierwszą literę Hello hello nazwa pakietu musi być mała. W przeciwnym razie podczas rejestrowania elementów **BroadcastReceiver** i **IntentFilter** dla powiadomień wypychanych w kolejnym etapie zostaną zwrócone błędy manifestu aplikacji.
   > 
   > 
   
      ![](./media/partner-xamarin-notification-hubs-android-get-started/notification-hub--xamarin-android-app-options.png)
2. Opcjonalnie, zestaw hello **Minimum Android wersji** tooanother poziom interfejsu API.
3. Opcjonalnie, zestaw hello **wersji docelowej Android** toohello inna wersja interfejsu API, które mają tootarget (musi być poziom interfejsu API 8 lub nowszy).

Kliknij przycisk **OK** i zamknij hello opcje projektu w oknie dialogowym.

### <a name="add-hello-required-components-tooyour-project"></a>Dodaj projekt tooyour wymaganych składników hello
Witaj Google Cloud Messaging Client dostępny w magazynie składników Xamarin hello upraszcza proces hello obsługi powiadomień wypychanych na platformie Xamarin.Android.

1. Kliknij prawym przyciskiem myszy folder Components hello w aplikacji platformy Xamarin.Android i wybierz polecenie **Uzyskaj więcej składników**.
2. Wyszukaj hello **Azure Messaging** składników i dodaj go toohello projektu.
3. Wyszukaj hello **Google Cloud Messaging Client** składników i dodaj go toohello projektu.

### <a name="set-up-notification-hubs-in-your-project"></a>Konfigurowanie centrów powiadomień w projekcie
1. Zbierz następujące informacje dotyczące Twojego systemu Android aplikacji i Centrum powiadomień hello:
   
   * **GoogleProjectNumber**: Pobierz wartość numeru projektu z przeglądu hello aplikacji na powitania Google Developer Portal. Zanotowano wcześniej tej wartości podczas tworzenia aplikacji hello na powitania portalu.
   * **Nasłuchiwanie parametry połączenia**: na pulpicie nawigacyjnym hello w hello [klasycznego portalu Azure], kliknij przycisk **Wyświetl parametry połączenia**. Kopiuj hello *DefaultListenSharedAccessSignature* parametry połączenia dla tej wartości.
   * **Nazwa koncentratora**: jest to nazwa hello koncentrator z hello [klasycznego portalu Azure]. Na przykład *moje_centrum_powiadomien_2*.
     
     Utwórz **Constants.cs** klasy w projekcie Xamarin i zdefiniuj hello następujące wartości stałych hello klasy. Zastąp symbole zastępcze hello własnymi wartościami.
     
       public static class Constants   {
     
           public const string SenderID = "<GoogleProjectNumber>"; // Google API Project Number
           public const string ListenConnectionString = "<Listen connection string>";
           public const string NotificationHubName = "<hub name>";
       }
2. Dodaj następujące hello za pomocą instrukcji**MainActivity.cs**:
   
        using Android.Util;
        using Gcm.Client;
3. Dodawanie zmiennej toohello wystąpienia `MainActivity` klasy, która będzie używana tooshow okna dialogowego alertu uruchomionej aplikacji hello:
   
        public static MainActivity instance;
4. Utwórz następujące metody w hello hello **MainActivity** klasy:
   
        private void RegisterWithGCM()
        {
            // Check tooensure everything's set up right
            GcmClient.CheckDevice(this);
            GcmClient.CheckManifest(this);
   
            // Register for push notifications
            Log.Info("MainActivity", "Registering...");
            GcmClient.Register(this, Constants.SenderID);
        }
5. W hello `OnCreate` metody **MainActivity.cs**, zainicjować hello `instance` zmienną i dodaj wywołanie za`RegisterWithGCM`:
   
        protected override void OnCreate (Bundle bundle)
        {
            instance = this;
   
            base.OnCreate (bundle);
   
            // Set your view from hello "main" layout resource
            SetContentView (Resource.Layout.Main);
   
            // Get your button from hello layout resource,
            // and attach an event tooit
            Button button = FindViewById<Button> (Resource.Id.myButton);
   
            RegisterWithGCM();
        }
6. Utwórz nową klasę: **MyBroadcastReceiver**.
   
   > [!NOTE]
   > Poniżej znajdziesz instrukcje tworzenia klasy **BroadcastReceiver** krok po kroku. Jednak toomanually alternatywnych szybkie tworzenie **MyBroadcastReceiver.cs** jest toorefer toohello **GcmService.cs** plik znajdujący się w hello przykładowym projekcie platformy Xamarin.Android dołączonym hello [Przykłady NotificationHubs][GitHub]. Duplikowanie **GcmService.cs** i zmiana nazwy klas może być również doskonałym miejscem toostart.
   > 
   > 
7. Dodaj następujące hello za pomocą instrukcji**MyBroadcastReceiver.cs** (odwołujące się toohello składnika i zestawu dodanego wcześniej):
   
        using System.Collections.Generic;
        using System.Text;
        using Android.App;
        using Android.Content;
        using Android.Util;
        using Gcm.Client;
        using WindowsAzure.Messaging;
8. W **MyBroadcastReceiver.cs**, Dodaj następujące żądania uprawnień pomiędzy hello hello **przy użyciu** instrukcje i hello **przestrzeni nazw** deklaracji:
   
        [assembly: Permission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "com.google.android.c2dm.permission.RECEIVE")]
   
        //GET_ACCOUNTS is needed only for Android versions 4.0.3 and below
        [assembly: UsesPermission(Name = "android.permission.GET_ACCOUNTS")]
        [assembly: UsesPermission(Name = "android.permission.INTERNET")]
        [assembly: UsesPermission(Name = "android.permission.WAKE_LOCK")]
9. W **MyBroadcastReceiver.cs**, zmień hello **MyBroadcastReceiver** toomatch hello następujące klasy:
   
        [BroadcastReceiver(Permission=Gcm.Client.Constants.PERMISSION_GCM_INTENTS)]
        [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_MESSAGE },
            Categories = new string[] { "@PACKAGE_NAME@" })]
        [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_REGISTRATION_CALLBACK },
            Categories = new string[] { "@PACKAGE_NAME@" })]
        [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_LIBRARY_RETRY },
            Categories = new string[] { "@PACKAGE_NAME@" })]
        public class MyBroadcastReceiver : GcmBroadcastReceiverBase<PushHandlerService>
        {
            public static string[] SENDER_IDS = new string[] { Constants.SenderID };
   
            public const string TAG = "MyBroadcastReceiver-GCM";
        }
10. Dodaj w pliku **MyBroadcastReceiver.cs** kolejną klasę o nazwie **PushHandlerService** pochodzącą od klasy **GcmServiceBase**. Upewnij się, że hello tooapply **usługi** toohello klasy atrybutu:
    
         [Service] // Must use hello service tag
         public class PushHandlerService : GcmServiceBase
         {
             public static string RegistrationID { get; private set; }
             private NotificationHub Hub { get; set; }
    
             public PushHandlerService() : base(Constants.SenderID)
                {
                 Log.Info(MyBroadcastReceiver.TAG, "PushHandlerService() constructor");
             }
         }
11. Klasa **GcmServiceBase** implementuje metody **OnRegistered()**, **OnUnRegistered()**, **OnMessage()**, **OnRecoverableError()** oraz **OnError()**. Nasze **PushHandlerService** klasa implementacji musi zastępować te metody i będą uruchamiane w odpowiedzi toointeracting hello Centrum powiadomień.
12. Zastąpienie hello **OnRegistered()** metody w **PushHandlerService** przy użyciu hello następującego kodu:
    
         protected override void OnRegistered(Context context, string registrationId)
         {
             Log.Verbose(MyBroadcastReceiver.TAG, "GCM Registered: " + registrationId);
             RegistrationID = registrationId;
    
             createNotification("PushHandlerService-GCM Registered...",
                                 "hello device has been Registered!");
    
             Hub = new NotificationHub(Constants.NotificationHubName, Constants.ListenConnectionString,
                                         context);
             try
             {
                 Hub.UnregisterAll(registrationId);
             }
             catch (Exception ex)
             {
                 Log.Error(MyBroadcastReceiver.TAG, ex.Message);
             }
    
             //var tags = new List<string>() { "falcons" }; // create tags if you want
             var tags = new List<string>() {};
    
             try
             {
                 var hubRegistration = Hub.Register(registrationId, tags.ToArray());
             }
             catch (Exception ex)
             {
                 Log.Error(MyBroadcastReceiver.TAG, ex.Message);
             }
         }
    
    > [!NOTE]
    > W hello **OnRegistered()** kodu powyżej, należy zwrócić uwagę hello możliwości toospecify tagi tooregister dla określonych kanałów komunikacji.
    > 
    > 
13. Zastąpienie hello **OnMessage** metody w **PushHandlerService** przy użyciu hello następującego kodu:
    
        protected override void OnMessage(Context context, Intent intent)
        {
            Log.Info(MyBroadcastReceiver.TAG, "GCM Message Received!");
    
            var msg = new StringBuilder();
    
            if (intent != null && intent.Extras != null)
            {
                foreach (var key in intent.Extras.KeySet())
                    msg.AppendLine(key + "=" + intent.Extras.Get(key).ToString());
            }
    
            string messageText = intent.Extras.GetString("message");
            if (!string.IsNullOrEmpty (messageText))
            {
                createNotification ("New hub message!", messageText);
            }
            else
            {
                createNotification ("Unknown message details", msg.ToString ());
            }
        }
14. Dodaj następujące hello **createNotification** i **dialogNotify** metody zbyt**PushHandlerService** powiadamiania użytkowników w przypadku otrzymania powiadomienia.
    
    > [!NOTE]
    > Projekt powiadomień w systemie Android w wersji 5.0 i nowszych znacząco różni się od tego używanego we wcześniejszych wersjach. Jeśli w przypadku testowania tej funkcji w systemie Android 5.0 lub nowszej, aplikacji hello należy toobe systemem tooreceive hello powiadomień. Aby uzyskać więcej informacji, zobacz [Android Notifications](http://go.microsoft.com/fwlink/?LinkId=615880) (Powiadomienia w systemie Android).
    > 
    > 
    
        void createNotification(string title, string desc)
        {
            //Create notification
            var notificationManager = GetSystemService(Context.NotificationService) as NotificationManager;
    
            //Create an intent tooshow UI
            var uiIntent = new Intent(this, typeof(MainActivity));
    
            //Create hello notification
            var notification = new Notification(Android.Resource.Drawable.SymActionEmail, title);
    
            //Auto-cancel will remove hello notification once hello user touches it
            notification.Flags = NotificationFlags.AutoCancel;
    
            //Set hello notification info
            //we use hello pending intent, passing our ui intent over, which will get called
            //when hello notification is tapped.
            notification.SetLatestEventInfo(this, title, desc, PendingIntent.GetActivity(this, 0, uiIntent, 0));
    
            //Show hello notification
            notificationManager.Notify(1, notification);
            dialogNotify (title, desc);
        }
    
        protected void dialogNotify(String title, String message)
        {
    
            MainActivity.instance.RunOnUiThread(() => {
                AlertDialog.Builder dlg = new AlertDialog.Builder(MainActivity.instance);
                AlertDialog alert = dlg.Create();
                alert.SetTitle(title);
                alert.SetButton("Ok", delegate {
                    alert.Dismiss();
                });
                alert.SetMessage(message);
                alert.Show();
            });
        }
15. Zastąp abstrakcyjne elementy członkowskie **OnUnRegistered()**, **OnRecoverableError()** i **OnError()**, aby umożliwić skompilowanie kodu:
    
        protected override void OnUnRegistered(Context context, string registrationId)
        {
            Log.Verbose(MyBroadcastReceiver.TAG, "GCM Unregistered: " + registrationId);
    
            createNotification("GCM Unregistered...", "hello device has been unregistered!");
        }
    
        protected override bool OnRecoverableError(Context context, string errorId)
        {
            Log.Warn(MyBroadcastReceiver.TAG, "Recoverable Error: " + errorId);
    
            return base.OnRecoverableError (context, errorId);
        }
    
        protected override void OnError(Context context, string errorId)
        {
            Log.Error(MyBroadcastReceiver.TAG, "GCM Error: " + errorId);
        }

## <a name="run-your-app-in-hello-emulator"></a>Uruchom aplikację w emulatorze hello
Po uruchomieniu tej aplikacji w emulatorze hello, upewnij się, że używasz Android Virtual Device (AVD) obsługującego interfejsy API Google.

> [!IMPORTANT]
> W kolejności tooreceive powiadomienia wypychane należy skonfigurować konto Google na urządzeniu Avd. (W emulatorze hello Przejdź zbyt**ustawienia** i kliknij przycisk **Dodaj konto**.) Ponadto upewnij się, że emulator tego hello jest toohello połączenia internetowego.
> 
> [!NOTE]
> Projekt powiadomień w systemie Android w wersji 5.0 i nowszych znacząco różni się od tego używanego we wcześniejszych wersjach. Aby uzyskać więcej informacji, zobacz [Android Notifications](http://go.microsoft.com/fwlink/?LinkId=615880) (Powiadomienia w systemie Android).
> 
> 

1. W obszarze **Narzędzia** kliknij polecenie **Open Android Emulator Manager** (Otwórz menedżera emulatora systemu Android), zaznacz urządzenie, a następnie kliknij przycisk **Edit** (Edytuj).
   
      ![][18]
2. Wybierz pozycję **Google APIs** (Interfejsy API Google) w polu **Target** (Element docelowy), a następnie kliknij przycisk **OK**.
   
      ![][19]
3. Na górnym pasku narzędzi powitania kliknij **Uruchom**, a następnie wybierz aplikację. Uruchamia hello emulatora i działa aplikacja hello.
   
   Aplikacja Hello pobiera hello *registrationId* z usługi GCM i rejestruje hello Centrum powiadomień.

## <a name="send-notifications-from-your-backend"></a>Wysyłanie powiadomień z poziomu zaplecza
Możesz przetestować odbieranie powiadomień w aplikacji, wysyłając powiadomienia w hello [klasycznego portalu Azure] za pośrednictwem hello debugowania kartę na powitania Centrum powiadomień, jak pokazano na poniższym zrzucie ekranu hello.

![][30]

Powiadomienia wypychane są zwykle wysyłane w usłudze zaplecza, takiej jak Mobile Services czy ASP.NET, za pośrednictwem zgodnej biblioteki. Umożliwia także hello interfejsu API REST bezpośrednio toosend powiadomień wiadomości, jeśli biblioteka nie jest dostępna w danym zapleczu.

Poniżej przedstawiono listę kilka innych samouczków, które mogą podlegać tooreview wysyłania powiadomień:

* ASP.NET: Zobacz [toousers powiadomienia toopush użyciu usługi Notification Hubs].
* Azure Java centra powiadomień SDK: zobacz [jak toouse usługi Notification Hubs za pomocą języka Java](notification-hubs-java-push-notification-tutorial.md) wysyłania powiadomień za pomocą języka Java. To rozwiązanie przetestowano w programie Eclipse pod kątem tworzenia aplikacji dla systemu Android.
* PHP: Zobacz [jak toouse usługi Notification Hubs za pomocą języka PHP](notification-hubs-php-push-notification-tutorial.md).

W hello kolejnych podsekcjach samouczka hello wysyłanie powiadomień za pomocą aplikacji konsoli .NET oraz przy użyciu usługi mobilnej za pośrednictwem skryptu węzła.

#### <a name="optional-send-notifications-by-using-a-net-app"></a>(Opcjonalnie) Wysyłanie powiadomień za pomocą aplikacji .NET
W tej sekcji wyślemy powiadomienia za pomocą aplikacji konsoli .NET.

1. Utwórz nową aplikację konsoli języka Visual C#:
   
      ![][20]
2. W programie Visual Studio kliknij kolejno pozycje **Narzędzia**, **Menedżer pakietów NuGet**, **Konsola menedżera pakietów**.
   
    Spowoduje to wyświetlenie konsoli Menedżera pakietów hello w programie Visual Studio.
3. W oknie konsoli Menedżera pakietów hello, ustaw hello **domyślny projekt** tooyour nowy projekt aplikacji konsoli, a następnie w oknie konsoli hello, wykonaj następujące polecenie hello:
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    Spowoduje to dodanie toohello odwołanie do zestawu SDK usługi Azure Notification Hubs za pomocą hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">pakietu Microsoft.Azure.Notification Hubs NuGet</a>.
   
    ![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-package-manager.png)
4. Otwórz plik Program.cs hello i dodaj następujące hello `using` instrukcji:
   
        using Microsoft.Azure.NotificationHubs;
5. W Twojej `Program` klasy, Dodaj następujące metody hello. Zaktualizuj tekst zastępczy hello na Twojej *DefaultFullSharedAccessSignature* nazwę Centrum i parametry połączenia z hello [klasycznego portalu Azure].
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            await hub.SendGcmNativeNotificationAsync("{ \"data\" : {\"message\":\"Hello from Azure!\"}}");
        }
6. Dodaj hello następujące wiersze w Twojej **Main** metody:
   
         SendNotificationAsync();
         Console.ReadLine();
7. Naciśnij klawisz hello F5 klucza toorun hello aplikacji. Otrzymasz powiadomienie w aplikacji hello.
   
      ![][21]

#### <a name="optional-send-notifications-by-using-a-mobile-service"></a>(Opcjonalnie) Wysyłanie powiadomień wypychanych z poziomu usługi mobilnej
1. Wykonaj czynności opisane w temacie [Wprowadzenie do usług Mobile Services].
2. Zaloguj się toohello [klasycznego portalu Azure]i wybierz usługę mobilną.
3. Wybierz hello **harmonogramu** kartę w górnej części hello.
   
      ![][22]
4. Utwórz nowe zadanie zaplanowane, wstaw nazwę i wybierz opcję **Na żądanie**.
   
      ![][23]
5. Po utworzeniu zadania powitania kliknij nazwę zadania hello. Następnie kliknij przycisk hello **skryptu** kartę na górnym pasku hello.
6. Wstaw hello następującego skryptu w funkcji harmonogramu. Wprowadź symbole zastępcze hello tooreplace się z powiadomienia Centrum nazwy i hello parametrów połączenia dla *DefaultFullSharedAccessSignature* uzyskany wcześniej. Kliknij pozycję **Zapisz**.
   
        var azure = require('azure');
        var notificationHubService = azure.createNotificationHubService('<hub name>', '<connection string>');
        notificationHubService.gcm.send(null,'{"data":{"message" : "Hello from Mobile Services!"}}',
          function (error)
          {
            if (!error) {
               console.warn("Notification successful");
            }
            else
            {
              console.warn("Notification failed" + error);
            }
          }
        );
7. Kliknij przycisk **uruchom raz** na powitania dolnym pasku. W aplikacji powinno zostać odebrane wyskakujące powiadomienie.

## <a name="next-steps"></a>Następne kroki
W tym prostym przykładzie wysłano powiadomienia tooall urządzeń z systemem Android. W kolejności tootarget określonych użytkowników, zobacz samouczek toohello [toousers powiadomienia toopush użyciu usługi Notification Hubs]. Jeśli chcesz toosegment użytkowników na grupy zainteresowań, możesz przeczytać [toosend użyciu usługi Notification Hubs fundamentalne wiadomości]. Dowiedz się więcej na temat toouse centra powiadomień w [wskazówki dotyczące usługi Notification Hubs] w hello [toofor jak usługi Notification Hubs dla systemu Android].

<!-- Anchors. -->
[Enable Google Cloud Messaging]: #register
[Configure your Notification Hub]: #configure-hub
[Connecting your app toohello Notification Hub]: #connecting-app
[Run your app with hello emulator]: #run-app
[Send notifications from your back-end]: #send
[Next steps]:#next-steps

<!-- Images. -->

[11]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-configure-android.png

[13]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-xamarin-android-app1.png
[15]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-xamarin-android-app3.png

[18]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-android-app7.png
[19]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-android-app8.png

[20]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-console-app.png
[21]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-android-toast.png
[22]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-scheduler1.png
[23]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-scheduler2.png

[30]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hubs-debug-hub-gcm.png


<!-- URLs. -->
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253
[Wprowadzenie do usług Mobile Services]: /develop/mobile/tutorials/get-started-xamarin-android/#create-new-service
[JavaScript and HTML]: /develop/mobile/tutorials/get-started-with-push-js

[klasycznego portalu Azure]: https://manage.windowsazure.com/
[wns object]: http://go.microsoft.com/fwlink/p/?LinkId=260591
[wskazówki dotyczące usługi Notification Hubs]: http://msdn.microsoft.com/library/jj927170.aspx
[toofor jak usługi Notification Hubs dla systemu Android]: http://msdn.microsoft.com/library/dn282661.aspx

[toousers powiadomienia toopush użyciu usługi Notification Hubs]: /manage/services/notification-hubs/notify-users-aspnet
[toosend użyciu usługi Notification Hubs fundamentalne wiadomości]: /manage/services/notification-hubs/breaking-news-dotnet
[GCMClient Component page]: http://components.xamarin.com/view/GCMClient
[Xamarin.NotificationHub GitHub page]: https://github.com/SaschaDittmann/Xamarin.NotificationHub
[GitHub]: http://go.microsoft.com/fwlink/p/?LinkId=331329
[Składnik Google Cloud Messaging Client]: http://components.xamarin.com/view/GCMClient/
[Składnik Azure Messaging]: http://components.xamarin.com/view/azure-messaging
