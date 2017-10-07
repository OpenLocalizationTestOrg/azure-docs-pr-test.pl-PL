---
title: "aaaGet wprowadzenie do usługi Azure Notification Hubs dla aplikacji dla urządzeń Kindle | Dokumentacja firmy Microsoft"
description: "Z tego samouczka dowiesz się, jak toosend usługi Azure Notification Hubs toouse wypychanie powiadomień aplikacji dla urządzeń Kindle tooa."
services: notification-hubs
documentationcenter: 
author: ysxu
manager: erikre
editor: 
ms.assetid: 346fc8e5-294b-4e4f-9f27-7a82d9626e93
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-kindle
ms.devlang: Java
ms.topic: hero-article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 7c28d64372cd2d90bab9cd9bf818d333f3478f7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-notification-hubs-for-kindle-apps"></a>Rozpoczynanie pracy z usługą Notification Hubs dla aplikacji dla urządzeń Kindle
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a>Omówienie
Ten samouczek pokazuje, jak toosend usługi Azure Notification Hubs toouse wypychanie powiadomień aplikacji dla urządzeń Kindle tooa.
Utworzysz pustą aplikację dla urządzeń Kindle służącą do odbierania powiadomień wypychanych przy użyciu usługi Amazon Device Messaging (ADM).

## <a name="prerequisites"></a>Wymagania wstępne
Ten samouczek wymaga następujących hello:

* Pobierz hello zestawu SDK systemu Android (założono, że używany jest program Eclipse) z hello <a href="http://go.microsoft.com/fwlink/?LinkId=389797">witryny systemu Android</a>.
* Wykonaj kroki hello w <a href="https://developer.amazon.com/appsandservices/resources/development-tools/ide-tools/tech-docs/01-setting-up-your-development-environment">ustawienie Up Your Development Environment</a> tooset się środowisko rozwoju dla urządzeń Kindle.

## <a name="add-a-new-app-toohello-developer-portal"></a>Dodawanie nowego portalu deweloperów toohello aplikacji
1. Najpierw utwórz aplikację w hello [portalu dla deweloperów firmy Amazon].
   
    ![][0]
2. Kopiuj hello **klucz aplikacji**.
   
    ![][1]
3. W portalu powitania kliknij nazwę hello aplikacji, a następnie kliknij hello **Device Messaging** kartę.
   
    ![][2]
4. Kliknij pozycję **Create a New Security Profile** (Utwórz nowy profil zabezpieczeń), a następnie utwórz nowy profil zabezpieczeń (na przykład **profil zabezpieczeń TestAdm**). Następnie kliknij przycisk **Save** (Zapisz).
   
    ![][3]
5. Kliknij przycisk **profile zabezpieczeń** tooview hello zabezpieczeń profil, który został utworzony. Kopiuj hello **identyfikator klienta** i **klucz tajny klienta** do późniejszego użycia.
   
    ![][4]

## <a name="create-an-api-key"></a>Tworzenie klucza interfejsu API
1. Otwórz wiersz polecenia z uprawnieniami administratora.
2. Przejdź toohello folderu zestawu SDK systemu Android.
3. Wprowadź hello następujące polecenie:
   
        keytool -list -v -alias androiddebugkey -keystore ./debug.keystore
   
    ![][5]
4. Dla hello **keystore** hasła, typ **android**.
5. Kopiuj hello **MD5** linii papilarnych.
6. W portalu dla deweloperów hello, na powitania **wiadomości** , kliknij pozycję **Android/Kindle** , a następnie wprowadź nazwę hello hello pakietu aplikacji (na przykład **com.sample.notificationhubtest**) i hello **MD5** wartość, a następnie kliknij przycisk **Wygeneruj klucz interfejsu API**.

## <a name="add-credentials-toohello-hub"></a>Dodaj Centrum toohello poświadczeń
W portalu hello dodać powitania klienta, a klucz tajny klienta identyfikator toohello **Konfiguruj** kartę Centrum powiadomień.

## <a name="set-up-your-application"></a>Konfigurowanie aplikacji
> [!NOTE]
> Podczas tworzenia aplikacji użyj co najmniej poziomu 17 interfejsu API.
> 
> 

Dodaj projekcie Eclipse tooyour biblioteki usługi ADM hello:

1. biblioteki usługi ADM hello tooobtain, [Pobierz hello SDK]. Wyodrębnij plik zip zestawu SDK hello.
2. W programie Eclipse kliknij prawym przyciskiem myszy projekt, a następnie kliknij pozycję **Properties** (Właściwości). Wybierz **ścieżka kompilacji języka Java** na powitania po lewej i wybierz opcję hello ** bibliotek ** u góry hello. Kliknij przycisk **Dodaj zewnętrzne Jar**i wybierz hello plik `\SDK\Android\DeviceMessaging\lib\amazon-device-messaging-*.jar` z katalogu hello, w którym wyodrębniono hello zestaw SDK Amazon.
3. Pobierz hello NotificationHubs zestawu SDK systemu Android (link).
4. Rozpakuj pakiet hello, a następnie przeciągnij plik hello `notification-hubs-sdk.jar` do hello `libs` folderu w środowisku Eclipse.

Edytowanie użytkownika toosupport manifestu aplikacji usługi ADM:

1. Dodaj przestrzeń nazw Amazon hello hello głównego elementu manifestu:

        xmlns:amazon="http://schemas.amazon.com/apk/res/android"

1. Dodaj uprawnienia jako pierwszy element hello w elemencie manifestu hello. SUBSTITUTE **[YOUR PACKAGE NAME]** z pakietem hello używane toocreate aplikacji.
   
        <permission
         android:name="[YOUR PACKAGE NAME].permission.RECEIVE_ADM_MESSAGE"
         android:protectionLevel="signature" />
   
        <uses-permission android:name="android.permission.INTERNET"/>
   
        <uses-permission android:name="[YOUR PACKAGE NAME].permission.RECEIVE_ADM_MESSAGE" />
   
        <!-- This permission allows your app access tooreceive push notifications
        from ADM. -->
        <uses-permission android:name="com.amazon.device.messaging.permission.RECEIVE" />
   
        <!-- ADM uses WAKE_LOCK tookeep hello processor from sleeping when a message is received. -->
        <uses-permission android:name="android.permission.WAKE_LOCK" />
2. Wstaw po elemencie jako hello pierwszy element podrzędny elementu aplikacji hello hello. Należy pamiętać, toosubstitute **[YOUR SERVICE NAME]** obsługi komunikatów ADM tworzonym w następnej sekcji hello (takie jak hello pakiet), i zastąp nazwą hello **[YOUR PACKAGE NAME]** z hello Nazwa pakietu, z którego użyto do utworzenia aplikacji.
   
        <amazon:enable-feature
              android:name="com.amazon.device.messaging"
                     android:required="true"/>
        <service
            android:name="[YOUR SERVICE NAME]"
            android:exported="false" />
   
        <receiver
            android:name="[YOUR SERVICE NAME]$Receiver" />
   
            <!-- This permission ensures that only ADM can send your app registration broadcasts. -->
            android:permission="com.amazon.device.messaging.permission.SEND" >
   
            <!-- toointeract with ADM, your app must listen for hello following intents. -->
            <intent-filter>
          <action android:name="com.amazon.device.messaging.intent.REGISTRATION" />
          <action android:name="com.amazon.device.messaging.intent.RECEIVE" />
   
          <!-- Replace hello name in hello category tag with your app's package name. -->
          <category android:name="[YOUR PACKAGE NAME]" />
            </intent-filter>
        </receiver>

## <a name="create-your-adm-message-handler"></a>Tworzenie programu obsługi usługi ADM
1. Utwórz nową klasę, która dziedziczy `com.amazon.device.messaging.ADMMessageHandlerBase` i nadaj mu nazwę `MyADMMessageHandler`, jak pokazano w hello następującej ilustracji:
   
    ![][6]
2. Dodaj następujące hello `import` instrukcji:
   
        import android.app.NotificationManager;
        import android.app.PendingIntent;
        import android.content.Context;
        import android.content.Intent;
        import android.support.v4.app.NotificationCompat;
        import com.amazon.device.messaging.ADMMessageReceiver;
        import com.microsoft.windowsazure.messaging.NotificationHub
3. Dodaj następujące kod w utworzonej klasie hello hello. Należy pamiętać o toosubstitute hello Centrum nazwy i parametry połączenia (nasłuchiwanie):
   
        public static final int NOTIFICATION_ID = 1;
        private NotificationManager mNotificationManager;
        NotificationCompat.Builder builder;
          private static NotificationHub hub;
        public static NotificationHub getNotificationHub(Context context) {
            Log.v("com.wa.hellokindlefire", "getNotificationHub");
            if (hub == null) {
                hub = new NotificationHub("[hub name]", "[listen connection string]", context);
            }
            return hub;
        }
   
        public MyADMMessageHandler() {
                super("MyADMMessageHandler");
            }
   
            public static class Receiver extends ADMMessageReceiver
            {
                public Receiver()
                {
                    super(MyADMMessageHandler.class);
                }
            }
   
            private void sendNotification(String msg) {
                Context ctx = getApplicationContext();
   
                mNotificationManager = (NotificationManager)
                    ctx.getSystemService(Context.NOTIFICATION_SERVICE);
   
            PendingIntent contentIntent = PendingIntent.getActivity(ctx, 0,
                  new Intent(ctx, MainActivity.class), 0);
   
            NotificationCompat.Builder mBuilder =
                  new NotificationCompat.Builder(ctx)
                  .setSmallIcon(R.mipmap.ic_launcher)
                  .setContentTitle("Notification Hub Demo")
                  .setStyle(new NotificationCompat.BigTextStyle()
                         .bigText(msg))
                  .setContentText(msg);
   
             mBuilder.setContentIntent(contentIntent);
             mNotificationManager.notify(NOTIFICATION_ID, mBuilder.build());
        }
4. Dodaj hello następującego kodu toohello `OnMessage()` metody:
   
        String nhMessage = intent.getExtras().getString("msg");
        sendNotification(nhMessage);
5. Dodaj hello następującego kodu toohello `OnRegistered` metody:
   
            try {
        getNotificationHub(getApplicationContext()).register(registrationId);
            } catch (Exception e) {
        Log.e("[your package name]", "Fail onRegister: " + e.getMessage(), e);
            }
6. Dodaj hello następującego kodu toohello `OnUnregistered` metody:
   
         try {
             getNotificationHub(getApplicationContext()).unregister();
         } catch (Exception e) {
             Log.e("[your package name]", "Fail onUnregister: " + e.getMessage(), e);
         }
7. W hello `MainActivity` metody, Dodaj powitania po instrukcji importu:
   
        import com.amazon.device.messaging.ADM;
8. Dodaj następującego kodu na końcu hello hello hello `OnCreate` metody:
   
        final ADM adm = new ADM(this);
        if (adm.getRegistrationId() == null)
        {
           adm.startRegister();
        } else {
            new AsyncTask() {
                  @Override
                  protected Object doInBackground(Object... params) {
                     try {                         MyADMMessageHandler.getNotificationHub(getApplicationContext()).register(adm.getRegistrationId());
                     } catch (Exception e) {
                         Log.e("com.wa.hellokindlefire", "Failed registration with hub", e);
                         return e;
                     }
                     return null;
                 }
               }.execute(null, null, null);
        }

## <a name="add-your-api-key-tooyour-app"></a>Dodaj aplikację tooyour klucza interfejsu API
1. W programie Eclipse Utwórz nowy plik o nazwie **api_key.txt** w hello katalogu zasobów projektu.
2. Witaj Otwórz plik i skopiuj hello klucz interfejsu API wygenerowany w portalu dla deweloperów firmy Amazon hello.

## <a name="run-hello-app"></a>Uruchamianie aplikacji hello
1. Uruchom hello emulator.
2. W emulatorze hello, szybko przesuń od góry hello, a następnie kliknij przycisk **ustawienia**, a następnie kliknij przycisk **Moje konto** i zarejestruj prawidłowe konto Amazon.
3. W środowisku Eclipse uruchamianie aplikacji hello.

> [!NOTE]
> Jeśli wystąpi problem, Sprawdź czas hello hello emulatora (lub urządzenia). wartość czasu Hello musi być dokładna. czas hello toochange hello emulatora urządzenia Kindle, możesz uruchomić hello następujące polecenie z katalogu narzędzi platformy zestawu SDK systemu Android:
> 
> 

        adb shell  date -s "yyyymmdd.hhmmss"

## <a name="send-a-message"></a>Wysyłanie komunikatu
toosend wiadomości przy użyciu programu .NET:

        static void Main(string[] args)
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("[conn string]", "[hub name]");

            hub.SendAdmNativeNotificationAsync("{\"data\":{\"msg\" : \"Hello from .NET!\"}}").Wait();
        }

![][7]

<!-- URLs. -->
[portalu dla deweloperów firmy Amazon]: https://developer.amazon.com/home.html
[Pobierz hello SDK]: https://developer.amazon.com/public/resources/development-tools/sdk

[0]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-portal1.png
[1]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-portal2.png
[2]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-portal3.png
[3]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-portal4.png
[4]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-portal5.png
[5]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-cmd-window.png
[6]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-new-java-class.png
[7]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-notification.png
