1. W Twojej **aplikacji** projektu, hello Otwórz plik `AndroidManifest.xml`. W kodzie hello w hello następne dwa kroki, Zastąp  *`**my_app_package**`*  o nazwie hello hello pakietu aplikacji dla projektu. Jest to wartość hello hello `package` atrybutu hello `manifest` tagu.
2. Dodaj następujące nowe uprawnienia po istniejących hello hello `uses-permission` elementu:

        <permission android:name="**my_app_package**.permission.C2D_MESSAGE"
            android:protectionLevel="signature" />
        <uses-permission android:name="**my_app_package**.permission.C2D_MESSAGE" />
        <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
        <uses-permission android:name="android.permission.GET_ACCOUNTS" />
        <uses-permission android:name="android.permission.WAKE_LOCK" />
3. Dodaj następującego kodu po hello hello `application` tagu początkowego:

        <receiver android:name="com.microsoft.windowsazure.notifications.NotificationsBroadcastReceiver"
                                         android:permission="com.google.android.c2dm.permission.SEND">
            <intent-filter>
                <action android:name="com.google.android.c2dm.intent.RECEIVE" />
                <category android:name="**my_app_package**" />
            </intent-filter>
        </receiver>
4. Otwórz hello pliku *ToDoActivity.java*i Dodaj powitania po instrukcji importu:

        import com.microsoft.windowsazure.notifications.NotificationsManager;
5. Dodaj następujące klasy prywatnej zmiennej toohello hello. Zastąp  *`<PROJECT_NUMBER>`*  numerem projektu hello przypisane przez aplikację tooyour Google w hello powyższej procedury.

        public static final String SENDER_ID = "<PROJECT_NUMBER>";
6. Zmiana definicji hello *MobileServiceClient* z **prywatnej** za**publiczne statyczne**, więc teraz wygląda następująco:

        public static MobileServiceClient mClient;
7. Dodawanie nowych powiadomień toohandle klasy. W Eksploratorze projektu otwórz hello **src** > **głównego** > **java** węzłów, a następnie kliknij prawym przyciskiem myszy hello pakietu Nazwa węzła. Kliknij przycisk **nowy**, a następnie kliknij przycisk **Klasa Java**.
8. W **nazwa**, typ `MyHandler`, a następnie kliknij przycisk **OK**.

    ![](./media/app-service-mobile-android-configure-push/android-studio-create-class.png)

9. W pliku MyHandler hello Zastąp hello deklaracji klasy z:

        public class MyHandler extends NotificationsHandler {
10. Dodaj następujące instrukcje importu dla hello hello `MyHandler` klasy:

        import com.microsoft.windowsazure.notifications.NotificationsHandler;
        import android.app.NotificationManager;
        import android.app.PendingIntent;
        import android.content.Context;
        import android.content.Intent;
        import android.os.AsyncTask;
        import android.os.Bundle;
        import android.support.v4.app.NotificationCompat;
11. Następnie dodać ten element członkowski toohello `MyHandler` klasy:

        public static final int NOTIFICATION_ID = 1;
12. W hello `MyHandler` klasy, Dodaj hello następującego kodu toooverride hello **onRegistered** metodę, która rejestruje urządzenie z Centrum powiadomień hello usługi mobilnej.

        @Override
        public void onRegistered(Context context,  final String gcmRegistrationId) {
           super.onRegistered(context, gcmRegistrationId);

           new AsyncTask<Void, Void, Void>() {

               protected Void doInBackground(Void... params) {
                   try {
                       ToDoActivity.mClient.getPush().register(gcmRegistrationId);
                       return null;
                   }
                   catch(Exception e) {
                       // handle error                
                   }
                   return null;              
               }
           }.execute();
       }
13. W hello `MyHandler` klasy, Dodaj hello następującego kodu toooverride hello **zdarzenia onReceive** metodę, która powoduje, że toodisplay powiadomień powitania po odebraniu.

        @Override
        public void onReceive(Context context, Bundle bundle) {
               String msg = bundle.getString("message");

               PendingIntent contentIntent = PendingIntent.getActivity(context,
                       0, // requestCode
                       new Intent(context, ToDoActivity.class),
                       0); // flags

               Notification notification = new NotificationCompat.Builder(context)
                       .setSmallIcon(R.drawable.ic_launcher)
                       .setContentTitle("Notification Hub Demo")
                       .setStyle(new NotificationCompat.BigTextStyle().bigText(msg))
                       .setContentText(msg)
                       .setContentIntent(contentIntent)
                       .build();

               NotificationManager notificationManager = (NotificationManager)
                       context.getSystemService(Context.NOTIFICATION_SERVICE);
               notificationManager.notify(NOTIFICATION_ID, notification);
       }
14. W pliku TodoActivity.java hello, zaktualizuj hello **onCreate** metody hello *ToDoActivity* klasy tooregister hello powiadomień obsługi klasy. Upewnij się, że tooadd ten kod po hello *MobileServiceClient* zostanie uruchomiony.

        NotificationsManager.handleNotifications(this, SENDER_ID, MyHandler.class);

    Aplikacja jest teraz zaktualizowane toosupport powiadomień wypychanych.
