
1. <span data-ttu-id="199f1-101">W widoku Solution (lub **Eksploratora rozwiązań** w programie Visual Studio), kliknij prawym przyciskiem myszy **składniki** folderu, kliknij przycisk **Uzyskaj więcej składników...** , wyszukaj **Google Cloud Messaging Client** składników i dodaj go do projektu.</span><span class="sxs-lookup"><span data-stu-id="199f1-101">In the Solution view (or **Solution Explorer** in Visual Studio), right-click the **Components** folder, click  **Get More Components...**, search for the **Google Cloud Messaging Client** component and add it to the project.</span></span>
2. <span data-ttu-id="199f1-102">Otwórz plik projektu o nazwie ToDoActivity.cs i dodaj następującą instrukcję do klasy using:</span><span class="sxs-lookup"><span data-stu-id="199f1-102">Open the ToDoActivity.cs project file and add the following using statement to the class:</span></span>
   
        using Gcm.Client;
3. <span data-ttu-id="199f1-103">W **ToDoActivity** klasy, Dodaj następujący kod:</span><span class="sxs-lookup"><span data-stu-id="199f1-103">In the **ToDoActivity** class, add the following new code:</span></span> 
   
        // Create a new instance field for this activity.
        static ToDoActivity instance = new ToDoActivity();
   
        // Return the current activity instance.
        public static ToDoActivity CurrentActivity
        {
            get
            {
                return instance;
            }
        }
        // Return the Mobile Services client.
        public MobileServiceClient CurrentClient
        {
            get
            {
                return client;
            }
        }
   
    <span data-ttu-id="199f1-104">Dzięki temu można uzyskać dostępu do wystąpienia klientów urządzeń przenośnych z procesu wypychanej obsługi usługi.</span><span class="sxs-lookup"><span data-stu-id="199f1-104">This enables you to access the mobile client instance from the push handler service process.</span></span>
4. <span data-ttu-id="199f1-105">Dodaj następujący kod do **OnCreate** metody, po **MobileServiceClient** utworzeniu:</span><span class="sxs-lookup"><span data-stu-id="199f1-105">Add the following code to the **OnCreate** method, after the **MobileServiceClient** is created:</span></span>
   
       // Set the current instance of TodoActivity.
       instance = this;
   
       // Make sure the GCM client is set up correctly.
       GcmClient.CheckDevice(this);
       GcmClient.CheckManifest(this);
   
       // Register the app for push notifications.
       GcmClient.Register(this, ToDoBroadcastReceiver.senderIDs);

<span data-ttu-id="199f1-106">Twoje **ToDoActivity** jest teraz gotowy do Dodawanie powiadomień wypychanych.</span><span class="sxs-lookup"><span data-stu-id="199f1-106">Your **ToDoActivity** is now prepared for adding push notifications.</span></span>

