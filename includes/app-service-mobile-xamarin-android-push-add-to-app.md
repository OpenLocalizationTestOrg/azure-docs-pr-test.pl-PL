1. <span data-ttu-id="cfbcc-101">Utwórz nową klasę w projekcie hello o nazwie `ToDoBroadcastReceiver`.</span><span class="sxs-lookup"><span data-stu-id="cfbcc-101">Create a new class in hello project called `ToDoBroadcastReceiver`.</span></span>
2. <span data-ttu-id="cfbcc-102">Dodaj następujące hello za pomocą instrukcji**ToDoBroadcastReceiver** klasy:</span><span class="sxs-lookup"><span data-stu-id="cfbcc-102">Add hello following using statements too**ToDoBroadcastReceiver** class:</span></span>
   
        using Gcm.Client;
        using Microsoft.WindowsAzure.MobileServices;
        using Newtonsoft.Json.Linq;
3. <span data-ttu-id="cfbcc-103">Dodaj następujące żądania uprawnień pomiędzy hello hello **przy użyciu** instrukcje i hello **przestrzeni nazw** deklaracji:</span><span class="sxs-lookup"><span data-stu-id="cfbcc-103">Add hello following permission requests between hello **using** statements and hello **namespace** declaration:</span></span>
   
        [assembly: Permission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "com.google.android.c2dm.permission.RECEIVE")]
   
        //GET_ACCOUNTS is only needed for android versions 4.0.3 and below
        [assembly: UsesPermission(Name = "android.permission.GET_ACCOUNTS")]
        [assembly: UsesPermission(Name = "android.permission.INTERNET")]
        [assembly: UsesPermission(Name = "android.permission.WAKE_LOCK")]
4. <span data-ttu-id="cfbcc-104">Zamień istniejące hello **ToDoBroadcastReceiver** definicji hello następujące klasy:</span><span class="sxs-lookup"><span data-stu-id="cfbcc-104">Replace hello existing **ToDoBroadcastReceiver** class definition with hello following:</span></span>
   
        [BroadcastReceiver(Permission = Gcm.Client.Constants.PERMISSION_GCM_INTENTS)]
        [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_MESSAGE }, 
            Categories = new string[] { "@PACKAGE_NAME@" })]
        [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_REGISTRATION_CALLBACK }, 
            Categories = new string[] { "@PACKAGE_NAME@" })]
        [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_LIBRARY_RETRY }, 
        Categories = new string[] { "@PACKAGE_NAME@" })]
        public class ToDoBroadcastReceiver : GcmBroadcastReceiverBase<PushHandlerService>
        {
            // Set hello Google app ID.
            public static string[] senderIDs = new string[] { "<PROJECT_NUMBER>" };
        }
   
    <span data-ttu-id="cfbcc-105">W hello powyżej kodu, musisz zastąpić  *`<PROJECT_NUMBER>`*  numerem projektu hello przypisane przez firmę Google podczas przydzielania aplikacji w portalu dla deweloperów Google hello.</span><span class="sxs-lookup"><span data-stu-id="cfbcc-105">In hello above code, you must replace *`<PROJECT_NUMBER>`* with hello project number assigned by Google when you provisioned your app in hello Google developer portal.</span></span> 
5. <span data-ttu-id="cfbcc-106">W pliku projektu ToDoBroadcastReceiver.cs hello Dodaj hello następującego kodu, który definiuje hello **PushHandlerService** klasy:</span><span class="sxs-lookup"><span data-stu-id="cfbcc-106">In hello ToDoBroadcastReceiver.cs project file, add hello following code that defines hello **PushHandlerService** class:</span></span>
   
        // hello ServiceAttribute must be applied toohello class.
        [Service] 
        public class PushHandlerService : GcmServiceBase
        {
            public static string RegistrationID { get; private set; }
   
            public PushHandlerService() : base(ToDoBroadcastReceiver.senderIDs) { }
        }
   
    <span data-ttu-id="cfbcc-107">Należy pamiętać, że ta klasa pochodzi od **GcmServiceBase** i że hello **usługi** atrybut musi być zastosowany toothis klasy.</span><span class="sxs-lookup"><span data-stu-id="cfbcc-107">Note that this class derives from **GcmServiceBase** and that hello **Service** attribute must be applied toothis class.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="cfbcc-108">Witaj **GcmServiceBase** klasa implementuje hello **OnRegistered()**, **OnUnRegistered()**, **OnMessage()** i  **OnError()** metody.</span><span class="sxs-lookup"><span data-stu-id="cfbcc-108">hello **GcmServiceBase** class implements hello **OnRegistered()**, **OnUnRegistered()**, **OnMessage()** and **OnError()** methods.</span></span> <span data-ttu-id="cfbcc-109">Konieczne jest przesłonięcie tych metod w hello **PushHandlerService** klasy.</span><span class="sxs-lookup"><span data-stu-id="cfbcc-109">You must override these methods in hello **PushHandlerService** class.</span></span>
   > 
   > 
6. <span data-ttu-id="cfbcc-110">Dodaj hello następującego kodu toohello **PushHandlerService** klasy, która zastępuje hello **OnRegistered** obsługi zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="cfbcc-110">Add hello following code toohello **PushHandlerService** class that overrides hello **OnRegistered** event handler.</span></span> 
   
        protected override void OnRegistered(Context context, string registrationId)
        {
            System.Diagnostics.Debug.WriteLine("hello device has been registered with GCM.", "Success!");
   
            // Get hello MobileServiceClient from hello current activity instance.
            MobileServiceClient client = ToDoActivity.CurrentActivity.CurrentClient;
            var push = client.GetPush();
   
            // Define a message body for GCM.
            const string templateBodyGCM = "{\"data\":{\"message\":\"$(messageParam)\"}}";
   
            // Define hello template registration as JSON.
            JObject templates = new JObject();
            templates["genericMessage"] = new JObject
            {
              {"body", templateBodyGCM }
            };
   
            try
            {
                // Make sure we run hello registration on hello same thread as hello activity, 
                // tooavoid threading errors.
                ToDoActivity.CurrentActivity.RunOnUiThread(
   
                    // Register hello template with Notification Hubs.
                    async () => await push.RegisterAsync(registrationId, templates));
   
                System.Diagnostics.Debug.WriteLine(
                    string.Format("Push Installation Id", push.InstallationId.ToString()));
            }
            catch (Exception ex)
            {
                System.Diagnostics.Debug.WriteLine(
                    string.Format("Error with Azure push registration: {0}", ex.Message));
            }
        }
   
    <span data-ttu-id="cfbcc-111">Ta metoda używa hello zwrócił GCM tooregister identyfikator rejestracji z platformy Azure, aby powiadomienia wypychane.</span><span class="sxs-lookup"><span data-stu-id="cfbcc-111">This method uses hello returned GCM registration ID tooregister with Azure for push notifications.</span></span> <span data-ttu-id="cfbcc-112">Tagi mogą być dodawane tylko toohello rejestracji po jego utworzeniu.</span><span class="sxs-lookup"><span data-stu-id="cfbcc-112">Tags can only be added toohello registration after it is created.</span></span> <span data-ttu-id="cfbcc-113">Aby uzyskać więcej informacji, zobacz [porady: Dodawanie tagów tooa urządzenia instalacji tooenable wypychania do znaczników](../articles/app-service-mobile/app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#tags).</span><span class="sxs-lookup"><span data-stu-id="cfbcc-113">For more information, see [How to: Add tags tooa device installation tooenable push-to-tags](../articles/app-service-mobile/app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#tags).</span></span>
7. <span data-ttu-id="cfbcc-114">Zastąpienie hello **OnMessage** metody w **PushHandlerService** z hello następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="cfbcc-114">Override hello **OnMessage** method in **PushHandlerService** with hello following code:</span></span>
   
       protected override void OnMessage(Context context, Intent intent)
       {          
           string message = string.Empty;
   
           // Extract hello push notification message from hello intent.
           if (intent.Extras.ContainsKey("message"))
           {
               message = intent.Extras.Get("message").ToString();
               var title = "New item added:";
   
               // Create a notification manager toosend hello notification.
               var notificationManager = 
                   GetSystemService(Context.NotificationService) as NotificationManager;
   
               // Create a new intent tooshow hello notification in hello UI. 
               PendingIntent contentIntent = 
                   PendingIntent.GetActivity(context, 0, 
                   new Intent(this, typeof(ToDoActivity)), 0);              
   
               // Create hello notification using hello builder.
               var builder = new Notification.Builder(context);
               builder.SetAutoCancel(true);
               builder.SetContentTitle(title);
               builder.SetContentText(message);
               builder.SetSmallIcon(Resource.Drawable.ic_launcher);
               builder.SetContentIntent(contentIntent);
               var notification = builder.Build();
   
               // Display hello notification in hello Notifications Area.
               notificationManager.Notify(1, notification);
   
           }
       }
8. <span data-ttu-id="cfbcc-115">Zastąpienie hello **OnUnRegistered()** i **OnError()** metod hello następującego kodu.</span><span class="sxs-lookup"><span data-stu-id="cfbcc-115">Override hello **OnUnRegistered()** and **OnError()** methods with hello following code.</span></span>
   
       protected override void OnUnRegistered(Context context, string registrationId)
       {
           throw new NotImplementedException();
       }
   
       protected override void OnError(Context context, string errorId)
       {
           System.Diagnostics.Debug.WriteLine(
               string.Format("Error occurred in hello notification: {0}.", errorId));
       }

