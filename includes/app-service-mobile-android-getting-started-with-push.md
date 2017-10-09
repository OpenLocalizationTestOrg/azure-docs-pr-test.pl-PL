1. <span data-ttu-id="e8bca-101">W Twojej **aplikacji** projektu, hello Otwórz plik `AndroidManifest.xml`.</span><span class="sxs-lookup"><span data-stu-id="e8bca-101">In your **app** project, open hello file `AndroidManifest.xml`.</span></span> <span data-ttu-id="e8bca-102">W kodzie hello w hello następne dwa kroki, Zastąp  *`**my_app_package**`*  o nazwie hello hello pakietu aplikacji dla projektu.</span><span class="sxs-lookup"><span data-stu-id="e8bca-102">In hello code in hello next two steps, replace *`**my_app_package**`* with hello name of hello app package for your project.</span></span> <span data-ttu-id="e8bca-103">Jest to wartość hello hello `package` atrybutu hello `manifest` tagu.</span><span class="sxs-lookup"><span data-stu-id="e8bca-103">This is hello value of hello `package` attribute of hello `manifest` tag.</span></span>
2. <span data-ttu-id="e8bca-104">Dodaj następujące nowe uprawnienia po istniejących hello hello `uses-permission` elementu:</span><span class="sxs-lookup"><span data-stu-id="e8bca-104">Add hello following new permissions after hello existing `uses-permission` element:</span></span>

        <permission android:name="**my_app_package**.permission.C2D_MESSAGE"
            android:protectionLevel="signature" />
        <uses-permission android:name="**my_app_package**.permission.C2D_MESSAGE" />
        <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
        <uses-permission android:name="android.permission.GET_ACCOUNTS" />
        <uses-permission android:name="android.permission.WAKE_LOCK" />
3. <span data-ttu-id="e8bca-105">Dodaj następującego kodu po hello hello `application` tagu początkowego:</span><span class="sxs-lookup"><span data-stu-id="e8bca-105">Add hello following code after hello `application` opening tag:</span></span>

        <receiver android:name="com.microsoft.windowsazure.notifications.NotificationsBroadcastReceiver"
                                         android:permission="com.google.android.c2dm.permission.SEND">
            <intent-filter>
                <action android:name="com.google.android.c2dm.intent.RECEIVE" />
                <category android:name="**my_app_package**" />
            </intent-filter>
        </receiver>
4. <span data-ttu-id="e8bca-106">Otwórz hello pliku *ToDoActivity.java*i Dodaj powitania po instrukcji importu:</span><span class="sxs-lookup"><span data-stu-id="e8bca-106">Open hello file *ToDoActivity.java*, and add hello following import statement:</span></span>

        import com.microsoft.windowsazure.notifications.NotificationsManager;
5. <span data-ttu-id="e8bca-107">Dodaj następujące klasy prywatnej zmiennej toohello hello.</span><span class="sxs-lookup"><span data-stu-id="e8bca-107">Add hello following private variable toohello class.</span></span> <span data-ttu-id="e8bca-108">Zastąp  *`<PROJECT_NUMBER>`*  numerem projektu hello przypisane przez aplikację tooyour Google w hello powyższej procedury.</span><span class="sxs-lookup"><span data-stu-id="e8bca-108">Replace *`<PROJECT_NUMBER>`* with hello project number assigned by Google tooyour app in hello preceding procedure.</span></span>

        public static final String SENDER_ID = "<PROJECT_NUMBER>";
6. <span data-ttu-id="e8bca-109">Zmiana definicji hello *MobileServiceClient* z **prywatnej** za**publiczne statyczne**, więc teraz wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="e8bca-109">Change hello definition of *MobileServiceClient* from **private** too**public static**, so it now looks like this:</span></span>

        public static MobileServiceClient mClient;
7. <span data-ttu-id="e8bca-110">Dodawanie nowych powiadomień toohandle klasy.</span><span class="sxs-lookup"><span data-stu-id="e8bca-110">Add a new class toohandle notifications.</span></span> <span data-ttu-id="e8bca-111">W Eksploratorze projektu otwórz hello **src** > **głównego** > **java** węzłów, a następnie kliknij prawym przyciskiem myszy hello pakietu Nazwa węzła.</span><span class="sxs-lookup"><span data-stu-id="e8bca-111">In Project Explorer, open hello **src** > **main** > **java** nodes, and right-click hello package name node.</span></span> <span data-ttu-id="e8bca-112">Kliknij przycisk **nowy**, a następnie kliknij przycisk **Klasa Java**.</span><span class="sxs-lookup"><span data-stu-id="e8bca-112">Click **New**, and then click **Java Class**.</span></span>
8. <span data-ttu-id="e8bca-113">W **nazwa**, typ `MyHandler`, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="e8bca-113">In **Name**, type `MyHandler`, and then click **OK**.</span></span>

    ![](./media/app-service-mobile-android-configure-push/android-studio-create-class.png)

9. <span data-ttu-id="e8bca-114">W pliku MyHandler hello Zastąp hello deklaracji klasy z:</span><span class="sxs-lookup"><span data-stu-id="e8bca-114">In hello MyHandler file, replace hello class declaration with:</span></span>

        public class MyHandler extends NotificationsHandler {
10. <span data-ttu-id="e8bca-115">Dodaj następujące instrukcje importu dla hello hello `MyHandler` klasy:</span><span class="sxs-lookup"><span data-stu-id="e8bca-115">Add hello following import statements for hello `MyHandler` class:</span></span>

        import com.microsoft.windowsazure.notifications.NotificationsHandler;
        import android.app.NotificationManager;
        import android.app.PendingIntent;
        import android.content.Context;
        import android.content.Intent;
        import android.os.AsyncTask;
        import android.os.Bundle;
        import android.support.v4.app.NotificationCompat;
11. <span data-ttu-id="e8bca-116">Następnie dodać ten element członkowski toohello `MyHandler` klasy:</span><span class="sxs-lookup"><span data-stu-id="e8bca-116">Next add this member toohello `MyHandler` class:</span></span>

        public static final int NOTIFICATION_ID = 1;
12. <span data-ttu-id="e8bca-117">W hello `MyHandler` klasy, Dodaj hello następującego kodu toooverride hello **onRegistered** metodę, która rejestruje urządzenie z Centrum powiadomień hello usługi mobilnej.</span><span class="sxs-lookup"><span data-stu-id="e8bca-117">In hello `MyHandler` class, add hello following code toooverride hello **onRegistered** method, which registers your device with hello mobile service notification hub.</span></span>

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
       <span data-ttu-id="e8bca-118">}</span><span class="sxs-lookup"><span data-stu-id="e8bca-118">}</span></span>
13. <span data-ttu-id="e8bca-119">W hello `MyHandler` klasy, Dodaj hello następującego kodu toooverride hello **zdarzenia onReceive** metodę, która powoduje, że toodisplay powiadomień powitania po odebraniu.</span><span class="sxs-lookup"><span data-stu-id="e8bca-119">In hello `MyHandler` class, add hello following code toooverride hello **onReceive** method, which causes hello notification toodisplay when it is received.</span></span>

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
       <span data-ttu-id="e8bca-120">}</span><span class="sxs-lookup"><span data-stu-id="e8bca-120">}</span></span>
14. <span data-ttu-id="e8bca-121">W pliku TodoActivity.java hello, zaktualizuj hello **onCreate** metody hello *ToDoActivity* klasy tooregister hello powiadomień obsługi klasy.</span><span class="sxs-lookup"><span data-stu-id="e8bca-121">Back in hello TodoActivity.java file, update hello **onCreate** method of hello *ToDoActivity* class tooregister hello notification handler class.</span></span> <span data-ttu-id="e8bca-122">Upewnij się, że tooadd ten kod po hello *MobileServiceClient* zostanie uruchomiony.</span><span class="sxs-lookup"><span data-stu-id="e8bca-122">Make sure tooadd this code after hello *MobileServiceClient* is instantiated.</span></span>

        NotificationsManager.handleNotifications(this, SENDER_ID, MyHandler.class);

    <span data-ttu-id="e8bca-123">Aplikacja jest teraz zaktualizowane toosupport powiadomień wypychanych.</span><span class="sxs-lookup"><span data-stu-id="e8bca-123">Your app is now updated toosupport push notifications.</span></span>
