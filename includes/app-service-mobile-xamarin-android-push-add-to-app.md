1. <span data-ttu-id="d210b-101">Utwórz nową klasę w projekcie o nazwie `ToDoBroadcastReceiver`.</span><span class="sxs-lookup"><span data-stu-id="d210b-101">Create a new class in the project called `ToDoBroadcastReceiver`.</span></span>
2. <span data-ttu-id="d210b-102">Dodaj następujące instrukcje using **ToDoBroadcastReceiver** klasy:</span><span class="sxs-lookup"><span data-stu-id="d210b-102">Add the following using statements to **ToDoBroadcastReceiver** class:</span></span>
   
        using Gcm.Client;
        using Microsoft.WindowsAzure.MobileServices;
        using Newtonsoft.Json.Linq;
3. <span data-ttu-id="d210b-103">Dodaj następujące żądania uprawnień pomiędzy **przy użyciu** instrukcje i **przestrzeni nazw** deklaracji:</span><span class="sxs-lookup"><span data-stu-id="d210b-103">Add the following permission requests between the **using** statements and the **namespace** declaration:</span></span>
   
        [assembly: Permission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "com.google.android.c2dm.permission.RECEIVE")]
   
        //GET_ACCOUNTS is only needed for android versions 4.0.3 and below
        [assembly: UsesPermission(Name = "android.permission.GET_ACCOUNTS")]
        [assembly: UsesPermission(Name = "android.permission.INTERNET")]
        [assembly: UsesPermission(Name = "android.permission.WAKE_LOCK")]
4. <span data-ttu-id="d210b-104">Zastąp istniejące **ToDoBroadcastReceiver** klasy definicji z następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="d210b-104">Replace the existing **ToDoBroadcastReceiver** class definition with the following:</span></span>
   
        [BroadcastReceiver(Permission = Gcm.Client.Constants.PERMISSION_GCM_INTENTS)]
        [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_MESSAGE }, 
            Categories = new string[] { "@PACKAGE_NAME@" })]
        [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_REGISTRATION_CALLBACK }, 
            Categories = new string[] { "@PACKAGE_NAME@" })]
        [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_LIBRARY_RETRY }, 
        Categories = new string[] { "@PACKAGE_NAME@" })]
        public class ToDoBroadcastReceiver : GcmBroadcastReceiverBase<PushHandlerService>
        {
            // Set the Google app ID.
            public static string[] senderIDs = new string[] { "<PROJECT_NUMBER>" };
        }
   
    <span data-ttu-id="d210b-105">W powyższym kodzie, należy zastąpić  *`<PROJECT_NUMBER>`*  numer projektu przypisane przez firmę Google podczas przydzielania aplikacji w portalu dla deweloperów Google.</span><span class="sxs-lookup"><span data-stu-id="d210b-105">In the above code, you must replace *`<PROJECT_NUMBER>`* with the project number assigned by Google when you provisioned your app in the Google developer portal.</span></span> 
5. <span data-ttu-id="d210b-106">W pliku projektu ToDoBroadcastReceiver.cs, Dodaj następujący kod, który definiuje **PushHandlerService** klasy:</span><span class="sxs-lookup"><span data-stu-id="d210b-106">In the ToDoBroadcastReceiver.cs project file, add the following code that defines the **PushHandlerService** class:</span></span>
   
        // The ServiceAttribute must be applied to the class.
        [Service] 
        public class PushHandlerService : GcmServiceBase
        {
            public static string RegistrationID { get; private set; }
   
            public PushHandlerService() : base(ToDoBroadcastReceiver.senderIDs) { }
        }
   
    <span data-ttu-id="d210b-107">Należy pamiętać, że ta klasa pochodzi od **GcmServiceBase** i **usługi** musi zostać zastosowany atrybut do tej klasy.</span><span class="sxs-lookup"><span data-stu-id="d210b-107">Note that this class derives from **GcmServiceBase** and that the **Service** attribute must be applied to this class.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="d210b-108">**GcmServiceBase** klasa implementuje **OnRegistered()**, **OnUnRegistered()**, **OnMessage()** i  **OnError()** metody.</span><span class="sxs-lookup"><span data-stu-id="d210b-108">The **GcmServiceBase** class implements the **OnRegistered()**, **OnUnRegistered()**, **OnMessage()** and **OnError()** methods.</span></span> <span data-ttu-id="d210b-109">Konieczne jest przesłonięcie tych metod w **PushHandlerService** klasy.</span><span class="sxs-lookup"><span data-stu-id="d210b-109">You must override these methods in the **PushHandlerService** class.</span></span>
   > 
   > 
6. <span data-ttu-id="d210b-110">Dodaj następujący kod do **PushHandlerService** klasy, która zastępuje **OnRegistered** obsługi zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="d210b-110">Add the following code to the **PushHandlerService** class that overrides the **OnRegistered** event handler.</span></span> 
   
        protected override void OnRegistered(Context context, string registrationId)
        {
            System.Diagnostics.Debug.WriteLine("The device has been registered with GCM.", "Success!");
   
            // Get the MobileServiceClient from the current activity instance.
            MobileServiceClient client = ToDoActivity.CurrentActivity.CurrentClient;
            var push = client.GetPush();
   
            // Define a message body for GCM.
            const string templateBodyGCM = "{\"data\":{\"message\":\"$(messageParam)\"}}";
   
            // Define the template registration as JSON.
            JObject templates = new JObject();
            templates["genericMessage"] = new JObject
            {
              {"body", templateBodyGCM }
            };
   
            try
            {
                // Make sure we run the registration on the same thread as the activity, 
                // to avoid threading errors.
                ToDoActivity.CurrentActivity.RunOnUiThread(
   
                    // Register the template with Notification Hubs.
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
   
    <span data-ttu-id="d210b-111">Ta metoda używa zwrócony identyfikator rejestracji usługi GCM do rejestracji przy użyciu platformy Azure dla powiadomień wypychanych.</span><span class="sxs-lookup"><span data-stu-id="d210b-111">This method uses the returned GCM registration ID to register with Azure for push notifications.</span></span> <span data-ttu-id="d210b-112">Tagów można dodać tylko do rejestracji po jego utworzeniu.</span><span class="sxs-lookup"><span data-stu-id="d210b-112">Tags can only be added to the registration after it is created.</span></span> <span data-ttu-id="d210b-113">Aby uzyskać więcej informacji, zobacz [porady: Dodawanie tagów do instalacji urządzenia, aby włączyć wypychania do znaczników](../articles/app-service-mobile/app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#tags).</span><span class="sxs-lookup"><span data-stu-id="d210b-113">For more information, see [How to: Add tags to a device installation to enable push-to-tags](../articles/app-service-mobile/app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#tags).</span></span>
7. <span data-ttu-id="d210b-114">Zastąpienie **OnMessage** metody w **PushHandlerService** następującym kodem:</span><span class="sxs-lookup"><span data-stu-id="d210b-114">Override the **OnMessage** method in **PushHandlerService** with the following code:</span></span>
   
       protected override void OnMessage(Context context, Intent intent)
       {          
           string message = string.Empty;
   
           // Extract the push notification message from the intent.
           if (intent.Extras.ContainsKey("message"))
           {
               message = intent.Extras.Get("message").ToString();
               var title = "New item added:";
   
               // Create a notification manager to send the notification.
               var notificationManager = 
                   GetSystemService(Context.NotificationService) as NotificationManager;
   
               // Create a new intent to show the notification in the UI. 
               PendingIntent contentIntent = 
                   PendingIntent.GetActivity(context, 0, 
                   new Intent(this, typeof(ToDoActivity)), 0);              
   
               // Create the notification using the builder.
               var builder = new Notification.Builder(context);
               builder.SetAutoCancel(true);
               builder.SetContentTitle(title);
               builder.SetContentText(message);
               builder.SetSmallIcon(Resource.Drawable.ic_launcher);
               builder.SetContentIntent(contentIntent);
               var notification = builder.Build();
   
               // Display the notification in the Notifications Area.
               notificationManager.Notify(1, notification);
   
           }
       }
8. <span data-ttu-id="d210b-115">Zastąpienie **OnUnRegistered()** i **OnError()** metody z następującym kodem.</span><span class="sxs-lookup"><span data-stu-id="d210b-115">Override the **OnUnRegistered()** and **OnError()** methods with the following code.</span></span>
   
       protected override void OnUnRegistered(Context context, string registrationId)
       {
           throw new NotImplementedException();
       }
   
       protected override void OnError(Context context, string errorId)
       {
           System.Diagnostics.Debug.WriteLine(
               string.Format("Error occurred in the notification: {0}.", errorId));
       }

