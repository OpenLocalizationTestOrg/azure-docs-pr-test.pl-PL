---
title: "tooAndroid powiadomienia wypychane aaaSending przy użyciu usługi Azure Notification Hubs | Dokumentacja firmy Microsoft"
description: "Z tego samouczka, dowiesz się, jak toouse usługi Azure Notification Hubs toopush powiadomienia tooAndroid urządzeń."
services: notification-hubs
documentationcenter: android
keywords: powiadomienia wypychane, powiadomienie wypychane, powiadomienia wypychane w systemie android
author: ysxu
manager: erikre
editor: 
ms.assetid: 8268c6ef-af63-433c-b14e-a20b04a0342a
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: hero-article
ms.date: 07/05/2016
ms.author: yuaxu
ms.openlocfilehash: 6b15a477d86cf1e6efffb21c5bcef0de7761af79
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="sending-push-notifications-tooandroid-with-azure-notification-hubs"></a>Wysyłanie tooAndroid powiadomień wypychanych przy użyciu usługi Azure Notification Hubs
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a>Omówienie
> [!IMPORTANT]
> W tym temacie przedstawiono powiadomienia wypychane za pomocą usługi Google Cloud Messaging (GCM). Jeśli używasz firmy Google Firebase Cloud Messaging (FCM), zobacz [tooAndroid powiadomień wypychanych wysyłająca z usługi Azure Notification Hubs i FCM](notification-hubs-android-push-notification-google-fcm-get-started.md).
> 
> 

Ten samouczek pokazuje, jak toosend usługi Azure Notification Hubs toouse push aplikacji systemu Android tooan powiadomienia.
Utworzysz pustą aplikację dla systemu Android służącą do odbierania powiadomień wypychanych przy użyciu usługi Google Cloud Messaging (GCM).

[!INCLUDE [notification-hubs-hero-slug](../../includes/notification-hubs-hero-slug.md)]

Kod ukończyć powitalnych dla tego samouczka można pobrać z witryny GitHub [tutaj](https://github.com/Azure/azure-notificationhubs-samples/tree/master/Android/GetStarted).

## <a name="prerequisites"></a>Wymagania wstępne
> [!IMPORTANT]
> toocomplete tego samouczka, musi mieć aktywne konto platformy Azure. Jeśli go nie masz, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut. Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-android-get-started).
> 
> 

Ponadto tooan aktywne konto platformy Azure wymienionym powyżej, ten samouczek wymaga tylko hello najnowszą wersję [Android Studio](http://go.microsoft.com/fwlink/?LinkId=389797).

Wykonanie czynności opisanych w tym samouczku jest wymaganiem wstępnym dla wszystkich innych samouczków usługi Notification Hubs dotyczących aplikacji dla systemu Android.

## <a name="creating-a-project-that-supports-google-cloud-messaging"></a>Tworzenie projektu obsługującego usługę Google Cloud Messaging
[!INCLUDE [mobile-services-enable-Google-cloud-messaging](../../includes/mobile-services-enable-google-cloud-messaging.md)]

## <a name="configure-a-new-notification-hub"></a>Konfigurowanie nowego centrum powiadomień
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

&emsp;&emsp;6.   W hello **ustawienia** bloku, wybierz opcję **usługi powiadomień** , a następnie **Google (GCM)**. Wprowadź klucz hello interfejsu API i kliknij przycisk **zapisać**.

&emsp;&emsp;![Azure Notification Hubs — Google (GCM)](./media/notification-hubs-android-get-started/notification-hubs-gcm-api.png)

Centrum powiadomień jest teraz skonfigurowany toowork z usługą GCM i masz hello tooboth ciągów połączenia zarejestrować tooreceive Twojej aplikacji oraz wysyłać powiadomienia wypychane.

## <a id="connecting-app"></a>Łączenie aplikacji toohello Centrum powiadomień
### <a name="create-a-new-android-project"></a>Tworzenie nowego projektu dla systemu Android
1. W programie Android Studio utwórz nowy projekt programu Android Studio.
   
   ![Android Studio — nowy projekt][13]
2. Wybierz hello **Telefon i Tablet** współczynnik i hello **Minimum SDK** , które mają toosupport. Następnie kliknij przycisk **Next** (Dalej).
   
   ![Android Studio — przepływ pracy tworzenia projektu][14]
3. Wybierz **pusty działania** dla działania głównego hello, kliknij przycisk **dalej**, a następnie kliknij przycisk **Zakończ**.

### <a name="add-google-play-services-toohello-project"></a>Dodaj projekt toohello usług Google Play
[!INCLUDE [Add Play Services](../../includes/notification-hubs-android-studio-add-google-play-services.md)]

### <a name="adding-azure-notification-hubs-libraries"></a>Dodawanie bibliotek usługi Azure Notification Hubs
1. W hello `Build.Gradle` pliku hello **aplikacji**, Dodaj następujące wiersze w hello hello **zależności** sekcji.
   
        compile 'com.microsoft.azure:notification-hubs-android-sdk:0.4@aar'
        compile 'com.microsoft.azure:azure-notifications-handler:1.0.1@aar'
2. Dodaj następujące repozytorium po hello hello **zależności** sekcji.
   
        repositories {
            maven {
                url "http://dl.bintray.com/microsoftazuremobile/SDK"
            }
        }

### <a name="updating-hello-androidmanifestxml"></a>Aktualizowanie pliku AndroidManifest.xml hello.
1. toosupport GCM musimy zaimplementować identyfikator wystąpienia usługi odbiornika w naszym kodzie, który jest używany zbyt[uzyskiwania tokenów rejestracji](https://developers.google.com/cloud-messaging/android/client#sample-register) przy użyciu [interfejsu API firmy Google Instance ID](https://developers.google.com/instance-id/). W tym samouczku nazwiemy klasy hello `MyInstanceIDService`. 
   
    Dodaj następujące usługi definicji toohello pliku AndroidManifest.xml wewnątrz hello hello `<application>` tagu. Zastąp hello `<your package>` symbol zastępczy hello rzeczywistą nazwą pakietu wyświetlaną u góry hello hello `AndroidManifest.xml` pliku.
   
        <service android:name="<your package>.MyInstanceIDService" android:exported="false">
            <intent-filter>
                <action android:name="com.google.android.gms.iid.InstanceID"/>
            </intent-filter>
        </service>
2. Po uzyskaniu tokenu rejestracji usługi GCM z interfejsu API Instance ID hello, użyjemy go za[Zarejestruj hello Centrum powiadomień Azure](notification-hubs-push-notification-registration-management.md). Firma Microsoft będzie obsługę rejestracji w tle hello przy użyciu `IntentService` o nazwie `RegistrationIntentService`. Ta usługa będzie również odpowiadać za [odświeżanie naszego tokenu rejestracji usługi GCM](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens).
   
    Dodaj następujące usługi definicji toohello pliku AndroidManifest.xml wewnątrz hello hello `<application>` tagu. Zastąp hello `<your package>` symbol zastępczy hello rzeczywistą nazwą pakietu wyświetlaną u góry hello hello `AndroidManifest.xml` pliku. 
   
        <service
            android:name="<your package>.RegistrationIntentService"
            android:exported="false">
        </service>
3. Zdefiniujemy również odbiornik tooreceive powiadomienia. Dodaj powitania po odbiornika definicji toohello pliku AndroidManifest.xml wewnątrz hello `<application>` tagu. Zastąp hello `<your package>` symbol zastępczy hello rzeczywistą nazwą pakietu wyświetlaną u góry hello hello `AndroidManifest.xml` pliku.
   
        <receiver android:name="com.microsoft.windowsazure.notifications.NotificationsBroadcastReceiver"
            android:permission="com.google.android.c2dm.permission.SEND">
            <intent-filter>
                <action android:name="com.google.android.c2dm.intent.RECEIVE" />
                <category android:name="<your package name>" />
            </intent-filter>
        </receiver>
4. Dodaj uprawnienia poniżej hello powiązane z powitania po niezbędne usługi GCM `</application>` tagu. Upewnij się, że tooreplace `<your package>` z hello nazwą pakietu wyświetlaną u góry hello hello `AndroidManifest.xml` pliku.
   
    Aby uzyskać więcej informacji o tych uprawnieniach, zobacz [Setup a GCM Client app for Android](https://developers.google.com/cloud-messaging/android/client#manifest) (Konfigurowanie aplikacji klienta usługi GCM dla systemu Android).
   
        <uses-permission android:name="android.permission.INTERNET"/>
        <uses-permission android:name="android.permission.GET_ACCOUNTS"/>
        <uses-permission android:name="android.permission.WAKE_LOCK"/>
        <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
   
        <permission android:name="<your package>.permission.C2D_MESSAGE" android:protectionLevel="signature" />
        <uses-permission android:name="<your package>.permission.C2D_MESSAGE"/>

### <a name="adding-code"></a>Dodawanie kodu
1. W widoku projektu hello, rozwiń węzeł **aplikacji** > **src** > **głównego** > **java**. Kliknij prawym przyciskiem folder pakietu w węźle **java**, kliknij pozycję **New** (Nowy), a następnie kliknij pozycję **Java Class** (Klasa Java). Dodaj nową klasę o nazwie `NotificationSettings`. 
   
    ![Android Studio – nowa klasa Java][6]
   
    Upewnij się, że te trzy symbole zastępcze w hello następującego kodu dla hello hello tooupdate `NotificationSettings` klasy:
   
   * **SenderId**: hello numer projektu uzyskany wcześniej w hello [Google Cloud Console](http://cloud.google.com/console).
   * **HubListenConnectionString**: hello **DefaultListenAccessSignature** parametry połączenia Centrum. Możesz skopiować te parametry połączenia, klikając **zasady dostępu** na powitania **ustawienia** bloku Centrum w hello [Azure Portal].
   * **HubName**: Użyj hello nazwy Centrum powiadomień wyświetlaną w bloku Centrum hello w hello [Azure Portal].
     
     `NotificationSettings` — kod:
     
       public class NotificationSettings {
     
           public static String SenderId = "<Your project number>";
           public static String HubName = "<Your HubName>";
           public static String HubListenConnectionString = "<Your default listen connection string>";
       }
2. Przy użyciu powyższych kroków hello, Dodaj kolejną nową klasę o nazwie `MyInstanceIDService`. Będzie to nasza implementacja usługi odbiornika interfejsu Instance ID.
   
    Witaj kod dla tej klasy będzie wywoływać naszych `IntentService` za[tokenu usługi GCM hello odświeżania](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) w tle hello.
   
        import android.content.Intent;
        import android.util.Log;
        import com.google.android.gms.iid.InstanceIDListenerService;

        public class MyInstanceIDService extends InstanceIDListenerService {

            private static final String TAG = "MyInstanceIDService";

            @Override
            public void onTokenRefresh() {

                Log.i(TAG, "Refreshing GCM Registration Token");

                Intent intent = new Intent(this, RegistrationIntentService.class);
                startService(intent);
            }
        };


1. Dodaj inny nowy projekt tooyour klasy o nazwie `RegistrationIntentService`. Będzie to implementacja hello naszych `IntentService` która będzie obsługiwać [odświeżanie tokenu usługi GCM hello](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) i [rejestrowanie w Centrum powiadomień hello](notification-hubs-push-notification-registration-management.md).
   
    Witaj Użyj następującego kodu dla tej klasy.
   
        import android.app.IntentService;
        import android.content.Intent;
        import android.content.SharedPreferences;
        import android.preference.PreferenceManager;
        import android.util.Log;
   
        import com.google.android.gms.gcm.GoogleCloudMessaging;
        import com.google.android.gms.iid.InstanceID;
        import com.microsoft.windowsazure.messaging.NotificationHub;
   
        public class RegistrationIntentService extends IntentService {
   
            private static final String TAG = "RegIntentService";
   
            private NotificationHub hub;
   
            public RegistrationIntentService() {
                super(TAG);
            }
   
            @Override
            protected void onHandleIntent(Intent intent) {        
                SharedPreferences sharedPreferences = PreferenceManager.getDefaultSharedPreferences(this);
                String resultString = null;
                String regID = null;
   
                try {
                    InstanceID instanceID = InstanceID.getInstance(this);
                    String token = instanceID.getToken(NotificationSettings.SenderId,
                            GoogleCloudMessaging.INSTANCE_ID_SCOPE);        
                    Log.i(TAG, "Got GCM Registration Token: " + token);
   
                    // Storing hello registration id that indicates whether hello generated token has been
                    // sent tooyour server. If it is not stored, send hello token tooyour server,
                    // otherwise your server should have already received hello token.
                    if ((regID=sharedPreferences.getString("registrationID", null)) == null) {        
                        NotificationHub hub = new NotificationHub(NotificationSettings.HubName,
                                NotificationSettings.HubListenConnectionString, this);
                        Log.i(TAG, "Attempting tooregister with NH using token : " + token);
   
                        regID = hub.register(token).getRegistrationId();
   
                        // If you want toouse tags...
                        // Refer too: https://azure.microsoft.com/en-us/documentation/articles/notification-hubs-routing-tag-expressions/
                        // regID = hub.register(token, "tag1", "tag2").getRegistrationId();
   
                        resultString = "Registered Successfully - RegId : " + regID;
                        Log.i(TAG, resultString);        
                        sharedPreferences.edit().putString("registrationID", regID ).apply();
                    } else {
                        resultString = "Previously Registered Successfully - RegId : " + regID;
                    }
                } catch (Exception e) {
                    Log.e(TAG, resultString="Failed toocomplete token refresh", e);
                    // If an exception happens while fetching hello new token or updating our registration data
                    // on a third-party server, this ensures that we'll attempt hello update at a later time.
                }
   
                // Notify UI that registration has completed.
                if (MainActivity.isVisible) {
                    MainActivity.mainActivity.ToastNotify(resultString);
                }
            }
        }
2. W Twojej `MainActivity` klasy, Dodaj następujące hello `import` instrukcje powyżej hello deklaracji klasy.
   
        import com.google.android.gms.common.ConnectionResult;
        import com.google.android.gms.common.GoogleApiAvailability;
        import com.google.android.gms.gcm.*;
        import com.microsoft.windowsazure.notifications.NotificationsManager;
        import android.util.Log;
        import android.widget.TextView;
        import android.widget.Toast;
3. Dodaj następujące prywatne elementy członkowskie u góry hello klasy hello hello. Będą one używane [Sprawdź hello dostępności usług Google Play zgodnie z zaleceniami firmy Google](https://developers.google.com/android/guides/setup#ensure_devices_have_the_google_play_services_apk).
   
        public static MainActivity mainActivity;
        public static Boolean isVisible = false;    
        private GoogleCloudMessaging gcm;
        private static final int PLAY_SERVICES_RESOLUTION_REQUEST = 9000;
4. W Twojej `MainActivity` klasy, Dodaj hello następujące metody toohello dostępności usług Google Play. 
   
        /**
         * Check hello device toomake sure it has hello Google Play Services APK. If
         * it doesn't, display a dialog that allows users toodownload hello APK from
         * hello Google Play Store or enable it in hello device's system settings.
         */
        private boolean checkPlayServices() {
            GoogleApiAvailability apiAvailability = GoogleApiAvailability.getInstance();
            int resultCode = apiAvailability.isGooglePlayServicesAvailable(this);
            if (resultCode != ConnectionResult.SUCCESS) {
                if (apiAvailability.isUserResolvableError(resultCode)) {
                    apiAvailability.getErrorDialog(this, resultCode, PLAY_SERVICES_RESOLUTION_REQUEST)
                            .show();
                } else {
                    Log.i(TAG, "This device is not supported by Google Play Services.");
                    ToastNotify("This device is not supported by Google Play Services.");
                    finish();
                }
                return false;
            }
            return true;
        }
5. W Twojej `MainActivity` klasy, Dodaj hello następującego kodu, który będzie sprawdzać dostępność usług Google Play przed wywołaniem z `IntentService` tooget Twojego tokenu rejestracji usługi GCM i rejestrowanie w Centrum powiadomień.
   
        public void registerWithNotificationHubs()
        {
            Log.i(TAG, " Registering with Notification Hubs");
   
            if (checkPlayServices()) {
                // Start IntentService tooregister this application with GCM.
                Intent intent = new Intent(this, RegistrationIntentService.class);
                startService(intent);
            }
        }
6. W hello `OnCreate` metody hello `MainActivity` klasy, Dodaj hello następującego procesu rejestracji hello toostart kod po utworzeniu działania.
   
        @Override
        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);
   
            mainActivity = this;
            NotificationsManager.handleNotifications(this, NotificationSettings.SenderId, MyHandler.class);
            registerWithNotificationHubs();
        }
7. Dodaj te dodatkowe metody toohello `MainActivity` tooverify aplikacji stanu i zgłosić stan w aplikacji.
   
        @Override
        protected void onStart() {
            super.onStart();
            isVisible = true;
        }
   
        @Override
        protected void onPause() {
            super.onPause();
            isVisible = false;
        }
   
        @Override
        protected void onResume() {
            super.onResume();
            isVisible = true;
        }
   
        @Override
        protected void onStop() {
            super.onStop();
            isVisible = false;
        }
   
        public void ToastNotify(final String notificationMessage) {
            runOnUiThread(new Runnable() {
                @Override
                public void run() {
                    Toast.makeText(MainActivity.this, notificationMessage, Toast.LENGTH_LONG).show();
                    TextView helloText = (TextView) findViewById(R.id.text_hello);
                    helloText.setText(notificationMessage);
                }
            });
        }
8. Witaj `ToastNotify` metoda używa hello *"Hello World"* `TextView` kontrolować stan tooreport i powiadomień w aplikacji hello. W układzie activity_main.xml Dodaj hello następującym identyfikatorze dla tego formantu.
   
       android:id="@+id/text_hello"
9. Następnie dodamy podklasę dla naszego odbiornika zdefiniowanego w pliku AndroidManifest.xml hello. Dodaj inny nowy projekt tooyour klasy o nazwie `MyHandler`.
10. Dodaj następujące instrukcje import u góry hello hello `MyHandler.java`:
    
        import android.app.NotificationManager;
        import android.app.PendingIntent;
        import android.content.Context;
        import android.content.Intent;
        import android.os.Bundle;
        import android.support.v4.app.NotificationCompat;
        import com.microsoft.windowsazure.notifications.NotificationsHandler;
11. Dodaj następującego kodu dla hello hello `MyHandler` co podklasą klasy `com.microsoft.windowsazure.notifications.NotificationsHandler`.
    
    Ten kod zastępuje hello `OnReceive` metody, więc program hello obsługi będzie zgłaszać odbierane powiadomienia. Program Hello obsługi wysyła również Menedżera powiadomień systemu Android toohello powiadomień wypychanych hello przy użyciu hello `sendNotification()` metody. Witaj `sendNotification()` — metoda powinna być wykonywana w przypadku aplikacji hello nie jest uruchomiona i Otrzymano powiadomienie.
    
        public class MyHandler extends NotificationsHandler {
            public static final int NOTIFICATION_ID = 1;
            private NotificationManager mNotificationManager;
            NotificationCompat.Builder builder;
            Context ctx;
    
            @Override
            public void onReceive(Context context, Bundle bundle) {
                ctx = context;
                String nhMessage = bundle.getString("message");
                sendNotification(nhMessage);
                if (MainActivity.isVisible) {
                    MainActivity.mainActivity.ToastNotify(nhMessage);
                }
            }
    
            private void sendNotification(String msg) {
    
                Intent intent = new Intent(ctx, MainActivity.class);
                intent.addFlags(Intent.FLAG_ACTIVITY_CLEAR_TOP);
    
                mNotificationManager = (NotificationManager)
                        ctx.getSystemService(Context.NOTIFICATION_SERVICE);
    
                PendingIntent contentIntent = PendingIntent.getActivity(ctx, 0,
                        intent, PendingIntent.FLAG_ONE_SHOT);
    
                Uri defaultSoundUri = RingtoneManager.getDefaultUri(RingtoneManager.TYPE_NOTIFICATION);
                NotificationCompat.Builder mBuilder =
                        new NotificationCompat.Builder(ctx)
                                .setSmallIcon(R.mipmap.ic_launcher)
                                .setContentTitle("Notification Hub Demo")
                                .setStyle(new NotificationCompat.BigTextStyle()
                                        .bigText(msg))
                                .setSound(defaultSoundUri)
                                .setContentText(msg);
    
                mBuilder.setContentIntent(contentIntent);
                mNotificationManager.notify(NOTIFICATION_ID, mBuilder.build());
            }
        }
12. W programie Android Studio hello paska menu, kliknij przycisk **kompilacji** > **Odbuduj projekt** toomake się upewnić, że nie istnieją wcześniejsze błędy w kodzie.

## <a name="sending-push-notifications"></a>Wysyłanie powiadomień wypychanych
Możesz przetestować odbieranie powiadomień wypychanych w aplikacji, wysyłając je za pośrednictwem hello [Azure Portal] -Wyszukaj hello **Rozwiązywanie problemów** sekcji w bloku Centrum hello, jak pokazano poniżej.

![Azure Notification Hubs — Wysyłanie testowe](./media/notification-hubs-android-get-started/notification-hubs-test-send.png)

[!INCLUDE [notification-hubs-sending-notifications-from-the-portal](../../includes/notification-hubs-sending-notifications-from-the-portal.md)]

## <a name="optional-send-push-notifications-directly-from-hello-app"></a>(Opcjonalnie) Wysyłanie powiadomień wypychanych bezpośrednio z aplikacji hello
Zwykle powiadomienia są wysyłane przy użyciu serwera zaplecza. W niektórych przypadkach może być powiadomień wypychanych stanie toosend toobe bezpośrednio z powitania klienta aplikacji. W tej sekcji opisano, jak hello toosend powiadomień z powitania klienta przy użyciu [interfejsu API REST Centrum powiadomień Azure](https://msdn.microsoft.com/library/azure/dn223264.aspx).

1. W widoku projektu programu Android Studio rozwiń węzeł **App** > **src** > **main** > **res** > **layout**. Otwórz hello `activity_main.xml` układu plik i kliknij przycisk hello **tekst** karcie tooupdate hello zawartość tekstową pliku hello. Zmodyfikuj go przy użyciu hello poniższego kodu, który dodaje nowe `Button` i `EditText` Centrum powiadomień toohello komunikatów powiadomień wypychanych służy do wysyłania. Dodaj ten kod bezpośrednio przed u dołu hello `</RelativeLayout>`.
   
        <Button
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="@string/send_button"
        android:id="@+id/sendbutton"
        android:layout_centerVertical="true"
        android:layout_centerHorizontal="true"
        android:onClick="sendNotificationButtonOnClick" />
   
        <EditText
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:id="@+id/editTextNotificationMessage"
        android:layout_above="@+id/sendbutton"
        android:layout_centerHorizontal="true"
        android:layout_marginBottom="42dp"
        android:hint="@string/notification_message_hint" />
2. W widoku projektu programu Android Studio rozwiń węzeł **App** > **src** > **main** > **res** > **values**. Otwórz hello `strings.xml` i Dodaj wartości ciągu hello, które odwołują się nowe hello `Button` i `EditText` kontrolki. Dodaj te u dołu hello hello pliku, bezpośrednio przed `</resources>`.
   
        <string name="send_button">Send Notification</string>
        <string name="notification_message_hint">Enter notification message text</string>
3. W Twojej `NotificationSetting.java` plików, Dodaj następujące ustawienie toohello hello `NotificationSettings` klasy.
   
    Aktualizacja `HubFullAccess` z hello **DefaultFullSharedAccessSignature** parametry połączenia Centrum. Ten ciąg połączenia można skopiować z hello [Azure Portal] , klikając **zasady dostępu** na powitania **ustawienia** bloku dla Centrum powiadomień.
   
        public static String HubFullAccess = "<Enter Your DefaultFullSharedAccess Connection string>";
4. W Twojej `MainActivity.java` plików, Dodaj następujące hello `import` instrukcje powyżej hello `MainActivity` klasy.
   
        import java.io.BufferedOutputStream;
        import java.io.BufferedReader;
        import java.io.InputStreamReader;
        import java.io.OutputStream;
        import java.net.HttpURLConnection;
        import java.net.URL;
        import java.net.URLEncoder;
        import javax.crypto.Mac;
        import javax.crypto.spec.SecretKeySpec;
        import android.util.Base64;
        import android.view.View;
        import android.widget.EditText;
5. W Twojej `MainActivity.java` plików, Dodaj następujące elementy członkowskie u góry hello hello hello `MainActivity` klasy.    
   
        private String HubEndpoint = null;
        private String HubSasKeyName = null;
        private String HubSasKeyValue = null;
6. Należy utworzyć tooauthenticate tokenu sygnatury (SaS) Centrum powiadomień tooyour wiadomości toosend POST żądania. To zrobić, analizując hello dane klucza z parametrów połączenia hello i następnie utworzenie hello tokenu sygnatury dostępu współdzielonego, jak wspomniano w hello [wspólne pojęcia](http://msdn.microsoft.com/library/azure/dn495627.aspx) dokumentacji interfejsu API REST. powitania po kod jest przykładem implementacji.
   
    W `MainActivity.java`, Dodaj następujące metody toohello hello `MainActivity` klasy tooparse parametrów połączenia.
   
        /**
         * Example code from http://msdn.microsoft.com/library/azure/dn495627.aspx
         * tooparse hello connection string so a SaS authentication token can be
         * constructed.
         *
         * @param connectionString This must be hello DefaultFullSharedAccess connection
         *                         string for this example.
         */
        private void ParseConnectionString(String connectionString)
        {
            String[] parts = connectionString.split(";");
            if (parts.length != 3)
                throw new RuntimeException("Error parsing connection string: "
                        + connectionString);
   
            for (int i = 0; i < parts.length; i++) {
                if (parts[i].startsWith("Endpoint")) {
                    this.HubEndpoint = "https" + parts[i].substring(11);
                } else if (parts[i].startsWith("SharedAccessKeyName")) {
                    this.HubSasKeyName = parts[i].substring(20);
                } else if (parts[i].startsWith("SharedAccessKey")) {
                    this.HubSasKeyValue = parts[i].substring(16);
                }
            }
        }
7. W `MainActivity.java`, Dodaj następujące metody toohello hello `MainActivity` klasy toocreate token uwierzytelniania sygnatury dostępu współdzielonego.
   
        /**
         * Example code from http://msdn.microsoft.com/library/azure/dn495627.aspx to
         * construct a SaS token from hello access key tooauthenticate a request.
         *
         * @param uri hello unencoded resource URI string for this operation. hello resource
         *            URI is hello full URI of hello Service Bus resource toowhich access is
         *            claimed. For example,
         *            "http://<namespace>.servicebus.windows.net/<hubName>"
         */
        private String generateSasToken(String uri) {
   
            String targetUri;
            String token = null;
            try {
                targetUri = URLEncoder
                        .encode(uri.toString().toLowerCase(), "UTF-8")
                        .toLowerCase();
   
                long expiresOnDate = System.currentTimeMillis();
                int expiresInMins = 60; // 1 hour
                expiresOnDate += expiresInMins * 60 * 1000;
                long expires = expiresOnDate / 1000;
                String toSign = targetUri + "\n" + expires;
   
                // Get an hmac_sha1 key from hello raw key bytes
                byte[] keyBytes = HubSasKeyValue.getBytes("UTF-8");
                SecretKeySpec signingKey = new SecretKeySpec(keyBytes, "HmacSHA256");
   
                // Get an hmac_sha1 Mac instance and initialize with hello signing key
                Mac mac = Mac.getInstance("HmacSHA256");
                mac.init(signingKey);
   
                // Compute hello hmac on input data bytes
                byte[] rawHmac = mac.doFinal(toSign.getBytes("UTF-8"));
   
                // Using android.util.Base64 for Android Studio instead of
                // Apache commons codec
                String signature = URLEncoder.encode(
                        Base64.encodeToString(rawHmac, Base64.NO_WRAP).toString(), "UTF-8");
   
                // Construct authorization string
                token = "SharedAccessSignature sr=" + targetUri + "&sig="
                        + signature + "&se=" + expires + "&skn=" + HubSasKeyName;
            } catch (Exception e) {
                if (isVisible) {
                    ToastNotify("Exception Generating SaS : " + e.getMessage().toString());
                }
            }
   
            return token;
        }
8. W `MainActivity.java`, Dodaj następujące metody toohello hello `MainActivity` hello toohandle klasy **Wyślij powiadomienie E-mail** kliknij przycisk i wysyłać powiadomienia wypychane hello Centrum toohello wiadomości przy użyciu hello wbudowanego interfejsu API REST.
   
        /**
         * Send Notification button click handler. This method parses the
         * DefaultFullSharedAccess connection string and generates a SaS token. The
         * token is added toohello Authorization header on hello POST request toothe
         * notification hub. hello text in hello editTextNotificationMessage control
         * is added as hello JSON body for hello request tooadd a GCM message toohello hub.
         *
         * @param v
         */
        public void sendNotificationButtonOnClick(View v) {
            EditText notificationText = (EditText) findViewById(R.id.editTextNotificationMessage);
            final String json = "{\"data\":{\"message\":\"" + notificationText.getText().toString() + "\"}}";
   
            new Thread()
            {
                public void run()
                {
                    try
                    {
                        // Based on reference documentation...
                        // http://msdn.microsoft.com/library/azure/dn223273.aspx
                        ParseConnectionString(NotificationSettings.HubFullAccess);
                        URL url = new URL(HubEndpoint + NotificationSettings.HubName +
                                "/messages/?api-version=2015-01");
   
                        HttpURLConnection urlConnection = (HttpURLConnection)url.openConnection();
   
                        try {
                            // POST request
                            urlConnection.setDoOutput(true);
   
                            // Authenticate hello POST request with hello SaS token
                            urlConnection.setRequestProperty("Authorization", 
                                generateSasToken(url.toString()));
   
                            // Notification format should be GCM
                            urlConnection.setRequestProperty("ServiceBusNotification-Format", "gcm");
   
                            // Include any tags
                            // Example below targets 3 specific tags
                            // Refer too: https://azure.microsoft.com/en-us/documentation/articles/notification-hubs-routing-tag-expressions/
                            // urlConnection.setRequestProperty("ServiceBusNotification-Tags", 
                            //        "tag1 || tag2 || tag3");
   
                            // Send notification message
                            urlConnection.setFixedLengthStreamingMode(json.length());
                            OutputStream bodyStream = new BufferedOutputStream(urlConnection.getOutputStream());
                            bodyStream.write(json.getBytes());
                            bodyStream.close();
   
                            // Get reponse
                            urlConnection.connect();
                            int responseCode = urlConnection.getResponseCode();
                            if ((responseCode != 200) && (responseCode != 201)) {
                                BufferedReader br = new BufferedReader(new InputStreamReader((urlConnection.getErrorStream())));
                                String line;
                                StringBuilder builder = new StringBuilder("Send Notification returned " +
                                        responseCode + " : ")  ;
                                while ((line = br.readLine()) != null) {
                                    builder.append(line);
                                }
   
                                ToastNotify(builder.toString());
                            }
                        } finally {
                            urlConnection.disconnect();
                        }
                    }
                    catch(Exception e)
                    {
                        if (isVisible) {
                            ToastNotify("Exception Sending Notification : " + e.getMessage().toString());
                        }
                    }
                }
            }.start();
        }

## <a name="testing-your-app"></a>Testowanie aplikacji
#### <a name="push-notifications-in-hello-emulator"></a>Powiadomienia wypychane w emulatorze hello
Jeśli chcesz tootest powiadomienia wypychane w emulatorze, upewnij się, że obraz emulatora obsługuje poziom interfejsu API Google hello wybrany dla aplikacji. Jeśli obraz nie obsługuje natywnych interfejsów API Google, będzie na końcu hello **usługi\_nie\_dostępne** wyjątku.

Ponadto toohello powyżej, upewnij się, że dodano Twoje tooyour konto Google uruchamiania emulatora w obszarze **ustawienia** > **kont**. W przeciwnym razie Twojej tooregister prób w usłudze GCM mogą spowodować hello **uwierzytelniania\_** wyjątku.

#### <a name="running-hello-application"></a>Uruchomienie aplikacji hello
1. Uruchamianie aplikacji hello i zwróć uwagę, że identyfikator rejestracji hello jest zgłaszany oznacza pomyślną rejestrację.
   
      ![Testowanie w systemie Android — rejestracja kanału][18]
2. Wprowadź toobe komunikat powiadomienia, wysyłane tooall urządzenia Android, które zostały zarejestrowane przy użyciu koncentratora hello.
   
      ![Testowanie w systemie Android — wysyłanie komunikatu][19]

3. Naciśnij przycisk **Send Notification** (Wyślij powiadomienie). Zostaną wyświetlone wszystkie urządzenia, na których jest uruchomiona aplikacja hello `AlertDialog` wystąpienia z komunikatu powiadomienia wypychane hello. Urządzenia, które nie zostały uruchomione aplikacji hello, ale zostały wcześniej zarejestrowane dla powiadomień wypychanych, otrzymasz powiadomienie w hello Menedżera powiadomień systemu Android. Można je wyświetlić, szybko przesuwając w dół od hello lewym górnym rogu.
   
      ![Testowanie w systemie Android — powiadomienia][21]

## <a name="next-steps"></a>Następne kroki
Firma Microsoft zaleca hello [toousers powiadomienia toopush użyciu usługi Notification Hubs] samouczka jako hello następnego kroku. Przedstawiono w nim sposób toosend powiadomień z zaplecza ASP.NET za pomocą tagów tootarget określonych użytkowników.

Jeśli chcesz toosegment użytkowników na grupy zainteresowań, zapoznaj się hello [toosend użyciu usługi Notification Hubs fundamentalne wiadomości] samouczka.

toolearn więcej ogólnych informacji o usłudze Notification Hubs, zobacz nasze [wskazówki dotyczące usługi Notification Hubs].

<!-- Images. -->
[6]: ./media/notification-hubs-android-get-started/notification-hub-android-new-class.png

[12]: ./media/notification-hubs-android-get-started/notification-hub-connection-strings.png

[13]: ./media/notification-hubs-android-get-started/notification-hubs-android-studio-new-project.png
[14]: ./media/notification-hubs-android-get-started/notification-hubs-android-studio-choose-form-factor.png
[15]: ./media/notification-hubs-android-get-started/notification-hub-create-android-app4.png
[16]: ./media/notification-hubs-android-get-started/notification-hub-create-android-app5.png
[17]: ./media/notification-hubs-android-get-started/notification-hub-create-android-app6.png

[18]: ./media/notification-hubs-android-get-started/notification-hubs-android-studio-registered.png
[19]: ./media/notification-hubs-android-get-started/notification-hubs-android-studio-set-message.png

[20]: ./media/notification-hubs-android-get-started/notification-hub-create-console-app.png
[21]: ./media/notification-hubs-android-get-started/notification-hubs-android-studio-received-message.png
[22]: ./media/notification-hubs-android-get-started/notification-hub-scheduler1.png
[23]: ./media/notification-hubs-android-get-started/notification-hub-scheduler2.png
[29]: ./media/mobile-services-android-get-started-push/mobile-eclipse-import-Play-library.png

[30]: ./media/notification-hubs-android-get-started/notification-hubs-debug-hub-gcm.png

[31]: ./media/notification-hubs-android-get-started/notification-hubs-android-studio-add-ui.png


<!-- URLs. -->
[Get started with push notifications in Mobile Services]: ../mobile-services-javascript-backend-android-get-started-push.md  
[Mobile Services Android SDK]: https://go.microsoft.com/fwLink/?LinkID=280126&clcid=0x409
[Referencing a library project]: http://go.microsoft.com/fwlink/?LinkId=389800
[Azure Classic Portal]: https://manage.windowsazure.com/
[wskazówki dotyczące usługi Notification Hubs]: http://msdn.microsoft.com/library/jj927170.aspx
[toousers powiadomienia toopush użyciu usługi Notification Hubs]: notification-hubs-aspnet-backend-gcm-android-push-to-user-google-notification.md
[toosend użyciu usługi Notification Hubs fundamentalne wiadomości]: notification-hubs-aspnet-backend-android-xplat-segmented-gcm-push-notification.md
[Azure Portal]: https://portal.azure.com
