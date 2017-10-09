
1. W widoku Solution hello (lub **Eksploratora rozwiązań** w programie Visual Studio), powitania kliknij prawym przyciskiem myszy **składniki** folderu, kliknij przycisk **Uzyskaj więcej składników...** , wyszukaj hello **Google Cloud Messaging Client** składników i dodaj go toohello projektu.
2. Otwórz plik projektu o nazwie ToDoActivity.cs hello i dodaj następujące hello za pomocą instrukcji toohello klasy:
   
        using Gcm.Client;
3. W hello **ToDoActivity** klasy, Dodaj powitania po nowy kod: 
   
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
   
    Dzięki temu tooaccess powitania klienta mobilnego wystąpienie z procesu usługi obsługi wypychanej hello.
4. Dodaj hello następującego kodu toohello **OnCreate** metody po hello **MobileServiceClient** utworzeniu:
   
       // Set hello current instance of TodoActivity.
       instance = this;
   
       // Make sure hello GCM client is set up correctly.
       GcmClient.CheckDevice(this);
       GcmClient.CheckManifest(this);
   
       // Register hello app for push notifications.
       GcmClient.Register(this, ToDoBroadcastReceiver.senderIDs);

Twoje **ToDoActivity** jest teraz gotowy do Dodawanie powiadomień wypychanych.

