
W tej sekcji przedstawiono, jak toosend fundamentalne wiadomości jako oznakowane szablonu powiadomienia z aplikacji konsoli .NET.

Jeśli używane są aplikacje mobilne można znaleźć toohello [Dodawanie powiadomień wypychanych do aplikacji mobilnej] samouczka i wybierz platformy u góry hello.

Jeśli chcesz toouse Java lub PHP można znaleźć za[jak toouse usługi Notification Hubs za pomocą języka Java/PHP]. Możesz wysłać powiadomienia z dowolnego zaplecza za pomocą [interfejsu REST centra powiadomień].

Jeśli utworzono aplikacji konsoli hello wysyłania powiadomień, gdy zostanie ukończone, powtórz kroki 1 – 3 [Rozpoczynanie pracy z usługą Notification Hubs].

1. W programie Visual Studio Utwórz nową aplikację konsoli języka Visual C#:
   
       ![][13]
2. W menu głównym programu Visual Studio hello, kliknij przycisk **narzędzia**, **Menedżer pakietów biblioteki**, i **Konsola Menedżera pakietów**, następnie w oknie konsoli hello wpisz następujące polecenie i naciśnij klawisz **Wprowadź**:
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    Spowoduje to dodanie toohello odwołanie do zestawu SDK usługi Azure Notification Hubs za pomocą hello [pakietu Microsoft.Azure.Notification Hubs NuGet].
3. Otwórz plik hello Program.cs i dodaj następujące hello `using` instrukcji:
   
        using Microsoft.Azure.NotificationHubs;
4. W hello `Program` klasy, Dodaj następujące metody hello lub zastąp ją, jeśli już istnieje:
   
        private static async void SendTemplateNotificationAsync()
        {
            // Define hello notification hub.
            NotificationHubClient hub =
                NotificationHubClient.CreateClientFromConnectionString(
                    "<connection string with full access>", "<hub name>");
   
            // Create an array of breaking news categories.
            var categories = new string[] { "World", "Politics", "Business",
                                            "Technology", "Science", "Sports"};
   
            // Sending hello notification as a template notification. All template registrations that contain
            // "messageParam" and hello proper tags will receive hello notifications.
            // This includes APNS, GCM, WNS, and MPNS template registrations.
   
            Dictionary<string, string> templateParams = new Dictionary<string, string>();
   
            foreach (var category in categories)
            {
                templateParams["messageParam"] = "Breaking " + category + " News!";
                await hub.SendTemplateNotificationAsync(templateParams, category);
            }
         }
   
    Ten kod wysyła powiadomienie szablonu dla każdej z sześciu tagi hello w tablicy ciągów hello. Hello Użyj tagów powoduje, że urządzenia będą otrzymywać powiadomienia tylko w przypadku kategorii hello zarejestrowany.
5. W hello powyżej kodu, Zastąp hello `<hub name>` i `<connection string with full access>` symbole zastępcze z powiadomienia Centrum nazwy i hello parametrów połączenia dla *DefaultFullSharedAccessSignature* z pulpitu nawigacyjnego hello Centrum powiadomień .
6. Dodaj następujące wiersze w hello hello **Main** metody:
   
         SendTemplateNotificationAsync();
         Console.ReadLine();
7. Tworzenie aplikacji konsoli hello.

<!-- Images. -->
[13]: ./media/notification-hubs-back-end/notification-hub-create-console-app.png

<!-- URLs. -->
[Rozpoczynanie pracy z usługą Notification Hubs]: ../articles/notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md
[interfejsu REST centra powiadomień]: http://msdn.microsoft.com/library/windowsazure/dn223264.aspx
[Dodawanie powiadomień wypychanych do aplikacji mobilnej]: ../articles/app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md
[jak toouse usługi Notification Hubs za pomocą języka Java/PHP]: ../articles/notification-hubs/notification-hubs-java-push-notification-tutorial.md
[pakietu Microsoft.Azure.Notification Hubs NuGet]: http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/
