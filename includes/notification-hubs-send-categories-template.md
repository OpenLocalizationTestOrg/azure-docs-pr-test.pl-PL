
<span data-ttu-id="540e0-101">W tej sekcji przedstawiono, jak toosend fundamentalne wiadomości jako oznakowane szablonu powiadomienia z aplikacji konsoli .NET.</span><span class="sxs-lookup"><span data-stu-id="540e0-101">This section shows how toosend breaking news as tagged template notifications from a .NET console app.</span></span>

<span data-ttu-id="540e0-102">Jeśli używane są aplikacje mobilne można znaleźć toohello [Dodawanie powiadomień wypychanych do aplikacji mobilnej] samouczka i wybierz platformy u góry hello.</span><span class="sxs-lookup"><span data-stu-id="540e0-102">If you are using Mobile Apps please refer toohello [Add push notifications for Mobile Apps] tutorial and select your platform at hello top.</span></span>

<span data-ttu-id="540e0-103">Jeśli chcesz toouse Java lub PHP można znaleźć za[jak toouse usługi Notification Hubs za pomocą języka Java/PHP].</span><span class="sxs-lookup"><span data-stu-id="540e0-103">If you want toouse Java or PHP refer too[How toouse Notification Hubs from Java/PHP].</span></span> <span data-ttu-id="540e0-104">Możesz wysłać powiadomienia z dowolnego zaplecza za pomocą [interfejsu REST centra powiadomień].</span><span class="sxs-lookup"><span data-stu-id="540e0-104">You can send notifications from any backend using the [Notification Hubs REST interface].</span></span>

<span data-ttu-id="540e0-105">Jeśli utworzono aplikacji konsoli hello wysyłania powiadomień, gdy zostanie ukończone, powtórz kroki 1 – 3 [Rozpoczynanie pracy z usługą Notification Hubs].</span><span class="sxs-lookup"><span data-stu-id="540e0-105">Skip steps 1-3 if you created hello console app for sending notifications when you completed [Get started with Notification Hubs].</span></span>

1. <span data-ttu-id="540e0-106">W programie Visual Studio Utwórz nową aplikację konsoli języka Visual C#:</span><span class="sxs-lookup"><span data-stu-id="540e0-106">In Visual Studio create a new Visual C# console application:</span></span>
   
       ![][13]
2. <span data-ttu-id="540e0-107">W menu głównym programu Visual Studio hello, kliknij przycisk **narzędzia**, **Menedżer pakietów biblioteki**, i **Konsola Menedżera pakietów**, następnie w oknie konsoli hello wpisz następujące polecenie i naciśnij klawisz **Wprowadź**:</span><span class="sxs-lookup"><span data-stu-id="540e0-107">In hello Visual Studio main menu, click **Tools**, **Library Package Manager**, and **Package Manager Console**, then in hello console window type the  following and press **Enter**:</span></span>
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    <span data-ttu-id="540e0-108">Spowoduje to dodanie toohello odwołanie do zestawu SDK usługi Azure Notification Hubs za pomocą hello [pakietu Microsoft.Azure.Notification Hubs NuGet].</span><span class="sxs-lookup"><span data-stu-id="540e0-108">This adds a reference toohello Azure Notification Hubs SDK using hello [Microsoft.Azure.Notification Hubs NuGet package].</span></span>
3. <span data-ttu-id="540e0-109">Otwórz plik hello Program.cs i dodaj następujące hello `using` instrukcji:</span><span class="sxs-lookup"><span data-stu-id="540e0-109">Open hello file Program.cs and add hello following `using` statement:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
4. <span data-ttu-id="540e0-110">W hello `Program` klasy, Dodaj następujące metody hello lub zastąp ją, jeśli już istnieje:</span><span class="sxs-lookup"><span data-stu-id="540e0-110">In hello `Program` class, add hello following method, or replace it if it already exists:</span></span>
   
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
   
    <span data-ttu-id="540e0-111">Ten kod wysyła powiadomienie szablonu dla każdej z sześciu tagi hello w tablicy ciągów hello.</span><span class="sxs-lookup"><span data-stu-id="540e0-111">This code sends a template notification for each of hello six tags in hello string array.</span></span> <span data-ttu-id="540e0-112">Hello Użyj tagów powoduje, że urządzenia będą otrzymywać powiadomienia tylko w przypadku kategorii hello zarejestrowany.</span><span class="sxs-lookup"><span data-stu-id="540e0-112">hello use of tags makes sure that devices receive notifications only for hello registered categories.</span></span>
5. <span data-ttu-id="540e0-113">W hello powyżej kodu, Zastąp hello `<hub name>` i `<connection string with full access>` symbole zastępcze z powiadomienia Centrum nazwy i hello parametrów połączenia dla *DefaultFullSharedAccessSignature* z pulpitu nawigacyjnego hello Centrum powiadomień .</span><span class="sxs-lookup"><span data-stu-id="540e0-113">In hello above code, replace hello `<hub name>` and `<connection string with full access>` placeholders with your notification hub name and hello connection  string for *DefaultFullSharedAccessSignature* from hello dashboard of your notification hub.</span></span>
6. <span data-ttu-id="540e0-114">Dodaj następujące wiersze w hello hello **Main** metody:</span><span class="sxs-lookup"><span data-stu-id="540e0-114">Add hello following lines in hello **Main** method:</span></span>
   
         SendTemplateNotificationAsync();
         Console.ReadLine();
7. <span data-ttu-id="540e0-115">Tworzenie aplikacji konsoli hello.</span><span class="sxs-lookup"><span data-stu-id="540e0-115">Build hello console app.</span></span>

<!-- Images. -->
[13]: ./media/notification-hubs-back-end/notification-hub-create-console-app.png

<!-- URLs. -->
[Rozpoczynanie pracy z usługą Notification Hubs]: ../articles/notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md
[interfejsu REST centra powiadomień]: http://msdn.microsoft.com/library/windowsazure/dn223264.aspx
[Dodawanie powiadomień wypychanych do aplikacji mobilnej]: ../articles/app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md
[jak toouse usługi Notification Hubs za pomocą języka Java/PHP]: ../articles/notification-hubs/notification-hubs-java-push-notification-tutorial.md
[pakietu Microsoft.Azure.Notification Hubs NuGet]: http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/
