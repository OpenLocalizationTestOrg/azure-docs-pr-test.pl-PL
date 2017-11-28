1. <span data-ttu-id="e25ea-101">W Twojej **aplikacji** projekt, otwórz plik `AndroidManifest.xml`.</span><span class="sxs-lookup"><span data-stu-id="e25ea-101">In your **app** project, open the file `AndroidManifest.xml`.</span></span> <span data-ttu-id="e25ea-102">W kodzie następne dwa kroki, Zastąp  *`**my_app_package**`*  z nazwą pakietu aplikacji dla projektu.</span><span class="sxs-lookup"><span data-stu-id="e25ea-102">In the code in the next two steps, replace *`**my_app_package**`* with the name of the app package for your project.</span></span> <span data-ttu-id="e25ea-103">Jest to wartość `package` atrybutu `manifest` znacznika.</span><span class="sxs-lookup"><span data-stu-id="e25ea-103">This is the value of the `package` attribute of the `manifest` tag.</span></span>
2. <span data-ttu-id="e25ea-104">Dodaj następujące nowe uprawnienia po istniejącej `uses-permission` elementu:</span><span class="sxs-lookup"><span data-stu-id="e25ea-104">Add the following new permissions after the existing `uses-permission` element:</span></span>

        <permission android:name="**my_app_package**.permission.C2D_MESSAGE"
            android:protectionLevel="signature" />
        <uses-permission android:name="**my_app_package**.permission.C2D_MESSAGE" />
        <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
        <uses-permission android:name="android.permission.GET_ACCOUNTS" />
        <uses-permission android:name="android.permission.WAKE_LOCK" />
3. <span data-ttu-id="e25ea-105">Dodaj następujący kod po `application` tagu początkowego:</span><span class="sxs-lookup"><span data-stu-id="e25ea-105">Add the following code after the `application` opening tag:</span></span>

        <receiver android:name="com.microsoft.windowsazure.notifications.NotificationsBroadcastReceiver"
                                         android:permission="com.google.android.c2dm.permission.SEND">
            <intent-filter>
                <action android:name="com.google.android.c2dm.intent.RECEIVE" />
                <category android:name="**my_app_package**" />
            </intent-filter>
        </receiver>
4. <span data-ttu-id="e25ea-106">Otwórz plik *ToDoActivity.java*i dodaj następującą instrukcję import:</span><span class="sxs-lookup"><span data-stu-id="e25ea-106">Open the file *ToDoActivity.java*, and add the following import statement:</span></span>

        import com.microsoft.windowsazure.notifications.NotificationsManager;
5. <span data-ttu-id="e25ea-107">Dodaj następujące prywatne zmienną do klasy.</span><span class="sxs-lookup"><span data-stu-id="e25ea-107">Add the following private variable to the class.</span></span> <span data-ttu-id="e25ea-108">Zastąp  *`<PROJECT_NUMBER>`*  numer projektu przypisany przez firmę Google do aplikacji w poprzedniej procedurze.</span><span class="sxs-lookup"><span data-stu-id="e25ea-108">Replace *`<PROJECT_NUMBER>`* with the project number assigned by Google to your app in the preceding procedure.</span></span>

        public static final String SENDER_ID = "<PROJECT_NUMBER>";
6. <span data-ttu-id="e25ea-109">Zmień definicję *MobileServiceClient* z **prywatnej** do **publiczne statyczne**, więc teraz wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="e25ea-109">Change the definition of *MobileServiceClient* from **private** to **public static**, so it now looks like this:</span></span>

        public static MobileServiceClient mClient;
7. <span data-ttu-id="e25ea-110">Dodaj nową klasę do obsługi powiadomień.</span><span class="sxs-lookup"><span data-stu-id="e25ea-110">Add a new class to handle notifications.</span></span> <span data-ttu-id="e25ea-111">Otwórz w Eksploratorze projektu **src** > **głównego** > **java** węzłów, a następnie kliknij prawym przyciskiem myszy węzeł nazwę pakietu.</span><span class="sxs-lookup"><span data-stu-id="e25ea-111">In Project Explorer, open the **src** > **main** > **java** nodes, and right-click the package name node.</span></span> <span data-ttu-id="e25ea-112">Kliknij przycisk **nowy**, a następnie kliknij przycisk **Klasa Java**.</span><span class="sxs-lookup"><span data-stu-id="e25ea-112">Click **New**, and then click **Java Class**.</span></span>
8. <span data-ttu-id="e25ea-113">W **nazwa**, typ `MyHandler`, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="e25ea-113">In **Name**, type `MyHandler`, and then click **OK**.</span></span>

    ![](./media/app-service-mobile-android-configure-push/android-studio-create-class.png)

9. <span data-ttu-id="e25ea-114">W pliku MyHandler Zastąp deklaracji klasy z:</span><span class="sxs-lookup"><span data-stu-id="e25ea-114">In the MyHandler file, replace the class declaration with:</span></span>

        public class MyHandler extends NotificationsHandler {
10. <span data-ttu-id="e25ea-115">Dodaj następujące instrukcje importu dla `MyHandler` klasy:</span><span class="sxs-lookup"><span data-stu-id="e25ea-115">Add the following import statements for the `MyHandler` class:</span></span>

        import com.microsoft.windowsazure.notifications.NotificationsHandler;
        import android.app.NotificationManager;
        import android.app.PendingIntent;
        import android.content.Context;
        import android.content.Intent;
        import android.os.AsyncTask;
        import android.os.Bundle;
        import android.support.v4.app.NotificationCompat;
11. <span data-ttu-id="e25ea-116">Następnie dodać ten element członkowski do `MyHandler` klasy:</span><span class="sxs-lookup"><span data-stu-id="e25ea-116">Next add this member to the `MyHandler` class:</span></span>

        public static final int NOTIFICATION_ID = 1;
12. <span data-ttu-id="e25ea-117">W `MyHandler` klasy, Dodaj następujący kod, aby zastąpić **onRegistered** metodę, która rejestruje urządzenie w Centrum powiadomień usługi mobilnej.</span><span class="sxs-lookup"><span data-stu-id="e25ea-117">In the `MyHandler` class, add the following code to override the **onRegistered** method, which registers your device with the mobile service notification hub.</span></span>

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
       <span data-ttu-id="e25ea-118">}</span><span class="sxs-lookup"><span data-stu-id="e25ea-118">}</span></span>
13. <span data-ttu-id="e25ea-119">W `MyHandler` klasy, Dodaj następujący kod, aby zastąpić **zdarzenia onReceive** metodę, która powoduje, że powiadomienie, aby wyświetlić po odebraniu.</span><span class="sxs-lookup"><span data-stu-id="e25ea-119">In the `MyHandler` class, add the following code to override the **onReceive** method, which causes the notification to display when it is received.</span></span>

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
       <span data-ttu-id="e25ea-120">}</span><span class="sxs-lookup"><span data-stu-id="e25ea-120">}</span></span>
14. <span data-ttu-id="e25ea-121">W pliku TodoActivity.java aktualizacji **onCreate** metody *ToDoActivity* klasy można zarejestrować klasy obsługi powiadomień.</span><span class="sxs-lookup"><span data-stu-id="e25ea-121">Back in the TodoActivity.java file, update the **onCreate** method of the *ToDoActivity* class to register the notification handler class.</span></span> <span data-ttu-id="e25ea-122">Upewnij się, że Dodaj ten kod po *MobileServiceClient* zostanie uruchomiony.</span><span class="sxs-lookup"><span data-stu-id="e25ea-122">Make sure to add this code after the *MobileServiceClient* is instantiated.</span></span>

        NotificationsManager.handleNotifications(this, SENDER_ID, MyHandler.class);

    <span data-ttu-id="e25ea-123">Aplikacja jest teraz zaktualizowana do obsługi powiadomień wypychanych.</span><span class="sxs-lookup"><span data-stu-id="e25ea-123">Your app is now updated to support push notifications.</span></span>
