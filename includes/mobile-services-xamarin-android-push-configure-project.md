
1. <span data-ttu-id="f5932-101">W widoku Solution hello (lub **Eksploratora rozwiązań** w programie Visual Studio), powitania kliknij prawym przyciskiem myszy **składniki** folderu, kliknij przycisk **Uzyskaj więcej składników...** , wyszukaj hello **Google Cloud Messaging Client** składników i dodaj go toohello projektu.</span><span class="sxs-lookup"><span data-stu-id="f5932-101">In hello Solution view (or **Solution Explorer** in Visual Studio), right-click hello **Components** folder, click  **Get More Components...**, search for hello **Google Cloud Messaging Client** component and add it toohello project.</span></span>
2. <span data-ttu-id="f5932-102">Otwórz plik projektu o nazwie ToDoActivity.cs hello i dodaj następujące hello za pomocą instrukcji toohello klasy:</span><span class="sxs-lookup"><span data-stu-id="f5932-102">Open hello ToDoActivity.cs project file and add hello following using statement toohello class:</span></span>
   
        using Gcm.Client;
3. <span data-ttu-id="f5932-103">W hello **ToDoActivity** klasy, Dodaj powitania po nowy kod:</span><span class="sxs-lookup"><span data-stu-id="f5932-103">In hello **ToDoActivity** class, add hello following new code:</span></span> 
   
        // Create a new instance field for this activity.
        static ToDoActivity instance = new ToDoActivity();
   
        // Return hello current activity instance.
        public static ToDoActivity CurrentActivity
        {
            get
            {
                return instance;
            }
        }
        // Return hello Mobile Services client.
        public MobileServiceClient CurrentClient
        {
            get
            {
                return client;
            }
        }
   
    <span data-ttu-id="f5932-104">Dzięki temu tooaccess powitania klienta mobilnego wystąpienie z procesu usługi obsługi wypychanej hello.</span><span class="sxs-lookup"><span data-stu-id="f5932-104">This enables you tooaccess hello mobile client instance from hello push handler service process.</span></span>
4. <span data-ttu-id="f5932-105">Dodaj hello następującego kodu toohello **OnCreate** metody po hello **MobileServiceClient** utworzeniu:</span><span class="sxs-lookup"><span data-stu-id="f5932-105">Add hello following code toohello **OnCreate** method, after hello **MobileServiceClient** is created:</span></span>
   
       // Set hello current instance of TodoActivity.
       instance = this;
   
       // Make sure hello GCM client is set up correctly.
       GcmClient.CheckDevice(this);
       GcmClient.CheckManifest(this);
   
       // Register hello app for push notifications.
       GcmClient.Register(this, ToDoBroadcastReceiver.senderIDs);

<span data-ttu-id="f5932-106">Twoje **ToDoActivity** jest teraz gotowy do Dodawanie powiadomień wypychanych.</span><span class="sxs-lookup"><span data-stu-id="f5932-106">Your **ToDoActivity** is now prepared for adding push notifications.</span></span>

