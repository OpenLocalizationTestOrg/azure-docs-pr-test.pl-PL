1. W Twojej **aplikacji** projekt, otwórz plik `AndroidManifest.xml`. Dodaj następujący kod po `application` tagu początkowego:

    ```xml
    <service android:name=".ToDoMessagingService">
        <intent-filter>
            <action android:name="com.google.firebase.MESSAGING_EVENT"/>
        </intent-filter>
    </service>
    <service android:name=".ToDoInstanceIdService">
        <intent-filter>
            <action android:name="com.google.firebase.INSTANCE_ID_EVENT"/>
        </intent-filter>
    </service>
    ```

2. Otwórz plik `ToDoActivity.java`i wprowadź następujące zmiany:

    - Dodaj instrukcję import:

        ```java
        import com.google.firebase.iid.FirebaseInstanceId;
        ```

    - Zmień definicję `MobileServiceClient` z **prywatnej** do **statycznego prywatnego**, więc teraz wygląda następująco:

        ```java
        private static MobileServiceClient mClient;
        ```

    - Dodaj `registerPush` metody:

        ```java
        public static void registerPush() {
            final String token = FirebaseInstanceId.getInstance().getToken();
            if (token != null) {
                new AsyncTask<Void, Void, Void>() {
                    protected Void doInBackground(Void... params) {
                        mClient.getPush().register(token);
                        return null;
                    }
                }.execute();
            }
        }
        ```

    - Aktualizacja **onCreate** metody `ToDoActivity` klasy. Upewnij się, że Dodaj ten kod po `MobileServiceClient` zostanie uruchomiony.

        ```java
        registerPush();
        ```

3. Dodaj nową klasę do obsługi powiadomień. Otwórz w Eksploratorze projektu **aplikacji** > **java** > **nazw swój projekt** węzłów, a następnie kliknij prawym przyciskiem myszy węzeł nazwę pakietu. Kliknij przycisk **nowy**, a następnie kliknij przycisk **Klasa Java**. W polu Nazwa wpisz `ToDoMessagingService`, a następnie kliknij przycisk OK. Następnie zastąp deklaracji klasy z:

    ```java
    import android.app.Notification;
    import android.app.NotificationManager;
    import android.app.PendingIntent;
    import android.content.Context;
    import android.content.Intent;

    import com.google.firebase.messaging.FirebaseMessagingService;
    import com.google.firebase.messaging.RemoteMessage;

    public class ToDoMessagingService extends FirebaseMessagingService {

        private static final int NOTIFICATION_ID = 1;

        @Override
        public void onMessageReceived(RemoteMessage remoteMessage) {
            String message = remoteMessage.getData().get("message");
            if (message != null) {
                sendNotification("Notification Hub Demo", message);
            }
        }

        private void sendNotification(String title, String messageBody) {
            PendingIntent contentIntent = PendingIntent.getActivity(this, 0, new Intent(this, ToDoActivity.class), 0);
            Notification.Builder notificationBuilder = new Notification.Builder(this)
                    .setSmallIcon(R.drawable.ic_launcher)
                    .setContentTitle(title)
                    .setContentText(messageBody)
                    .setContentIntent(contentIntent);
            NotificationManager notificationManager = (NotificationManager) getSystemService(Context.NOTIFICATION_SERVICE);
            if (notificationManager != null) {
                notificationManager.notify(NOTIFICATION_ID, notificationBuilder.build());
            }
        }
    }
    ```

4. Dodaj kolejną klasę do obsługi aktualizacji tokenu. Utwórz `ToDoInstanceIdService` java klasy i Zastąp deklaracji klasy z:

    ```java
    import com.google.firebase.iid.FirebaseInstanceIdService;

    public class ToDoInstanceIdService extends FirebaseInstanceIdService {

        @Override
        public void onTokenRefresh() {
            ToDoActivity.registerPush();
        }
    }
    ```

Aplikacja jest teraz zaktualizowana do obsługi powiadomień wypychanych.
