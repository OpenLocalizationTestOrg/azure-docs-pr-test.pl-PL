
<span data-ttu-id="843aa-101">W tej sekcji przedstawiono sposób wysyłanie najważniejszych wiadomości oznakowany szablonu powiadomienia z aplikacji konsoli .NET.</span><span class="sxs-lookup"><span data-stu-id="843aa-101">This section shows how to send breaking news as tagged template notifications from a .NET console app.</span></span>

<span data-ttu-id="843aa-102">Jeśli używasz Mobile Apps, zapoznaj się [Dodawanie powiadomień wypychanych do aplikacji mobilnej] samouczka i wybierz platformy u góry.</span><span class="sxs-lookup"><span data-stu-id="843aa-102">If you are using Mobile Apps please refer to the [Add push notifications for Mobile Apps] tutorial and select your platform at the top.</span></span>

<span data-ttu-id="843aa-103">Jeśli chcesz użyć Java lub PHP można znaleźć [jak używać usługi Notification Hubs za pomocą języka Java/PHP].</span><span class="sxs-lookup"><span data-stu-id="843aa-103">If you want to use Java or PHP refer to [How to use Notification Hubs from Java/PHP].</span></span> <span data-ttu-id="843aa-104">Możesz wysłać powiadomienia z dowolnego zaplecza za pomocą [interfejsu REST centra powiadomień].</span><span class="sxs-lookup"><span data-stu-id="843aa-104">You can send notifications from any backend using the [Notification Hubs REST interface].</span></span>

<span data-ttu-id="843aa-105">Jeśli utworzono aplikację konsoli do wysyłania powiadomień, gdy zostanie ukończone, powtórz kroki 1 – 3 [Rozpoczynanie pracy z usługą Notification Hubs].</span><span class="sxs-lookup"><span data-stu-id="843aa-105">Skip steps 1-3 if you created the console app for sending notifications when you completed [Get started with Notification Hubs].</span></span>

1. <span data-ttu-id="843aa-106">W programie Visual Studio Utwórz nową aplikację konsoli języka Visual C#:</span><span class="sxs-lookup"><span data-stu-id="843aa-106">In Visual Studio create a new Visual C# console application:</span></span>
   
       ![][13]
2. <span data-ttu-id="843aa-107">W menu głównym programu Visual Studio, kliknij przycisk **narzędzia**, **Menedżer pakietów biblioteki**, i **Konsola Menedżera pakietów**, wpisz następujące polecenie w oknie konsoli i naciśnij klawisz  **Wprowadź**:</span><span class="sxs-lookup"><span data-stu-id="843aa-107">In the Visual Studio main menu, click **Tools**, **Library Package Manager**, and **Package Manager Console**, then in the console window type the  following and press **Enter**:</span></span>
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    <span data-ttu-id="843aa-108">Spowoduje to dodanie odwołania do zestawu SDK usługi Azure Notification Hubs z użyciem [pakietu NuGet Microsoft.Azure.Notification Hubs].</span><span class="sxs-lookup"><span data-stu-id="843aa-108">This adds a reference to the Azure Notification Hubs SDK using the [Microsoft.Azure.Notification Hubs NuGet package].</span></span>
3. <span data-ttu-id="843aa-109">Otwórz plik Program.cs i dodaj następujące `using` instrukcji:</span><span class="sxs-lookup"><span data-stu-id="843aa-109">Open the file Program.cs and add the following `using` statement:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
4. <span data-ttu-id="843aa-110">W `Program` klasy, dodaj następującą metodę lub zastąp ją, jeśli już istnieje:</span><span class="sxs-lookup"><span data-stu-id="843aa-110">In the `Program` class, add the following method, or replace it if it already exists:</span></span>
   
        private static async void SendTemplateNotificationAsync()
        {
            // Define the notification hub.
            NotificationHubClient hub =
                NotificationHubClient.CreateClientFromConnectionString(
                    "<connection string with full access>", "<hub name>");
   
            // Create an array of breaking news categories.
            var categories = new string[] { "World", "Politics", "Business",
                                            "Technology", "Science", "Sports"};
   
            // Sending the notification as a template notification. All template registrations that contain
            // "messageParam" and the proper tags will receive the notifications.
            // This includes APNS, GCM, WNS, and MPNS template registrations.
   
            Dictionary<string, string> templateParams = new Dictionary<string, string>();
   
            foreach (var category in categories)
            {
                templateParams["messageParam"] = "Breaking " + category + " News!";
                await hub.SendTemplateNotificationAsync(templateParams, category);
            }
         }
   
    <span data-ttu-id="843aa-111">Ten kod wysyła powiadomienie szablonu dla każdej z sześciu tagów w tablicy ciągów.</span><span class="sxs-lookup"><span data-stu-id="843aa-111">This code sends a template notification for each of the six tags in the string array.</span></span> <span data-ttu-id="843aa-112">Tagi powoduje, że urządzenia będą otrzymywać powiadomienia tylko w przypadku zarejestrowanych kategorii.</span><span class="sxs-lookup"><span data-stu-id="843aa-112">The use of tags makes sure that devices receive notifications only for the registered categories.</span></span>
5. <span data-ttu-id="843aa-113">W powyższym kodzie Zamień `<hub name>` i `<connection string with full access>` symbole zastępcze nazwą Centrum powiadomień i parametry połączenia dla *DefaultFullSharedAccessSignature* na pulpicie nawigacyjnym Centrum powiadomień.</span><span class="sxs-lookup"><span data-stu-id="843aa-113">In the above code, replace the `<hub name>` and `<connection string with full access>` placeholders with your notification hub name and the connection  string for *DefaultFullSharedAccessSignature* from the dashboard of your notification hub.</span></span>
6. <span data-ttu-id="843aa-114">Dodaj następujące wiersze do metody **Main**:</span><span class="sxs-lookup"><span data-stu-id="843aa-114">Add the following lines in the **Main** method:</span></span>
   
         SendTemplateNotificationAsync();
         Console.ReadLine();
7. <span data-ttu-id="843aa-115">Tworzenie aplikacji konsoli.</span><span class="sxs-lookup"><span data-stu-id="843aa-115">Build the console app.</span></span>

<!-- Images. -->
[13]: ./media/notification-hubs-back-end/notification-hub-create-console-app.png

<!-- URLs. -->
<span data-ttu-id="843aa-116">[Rozpoczynanie pracy z usługą Notification Hubs]: ../articles/notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md</span><span class="sxs-lookup"><span data-stu-id="843aa-116">[Get started with Notification Hubs]: ../articles/notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md</span></span>
<span data-ttu-id="843aa-117">[interfejsu REST centra powiadomień]: http://msdn.microsoft.com/library/windowsazure/dn223264.aspx</span><span class="sxs-lookup"><span data-stu-id="843aa-117">[Notification Hubs REST interface]: http://msdn.microsoft.com/library/windowsazure/dn223264.aspx</span></span>
<span data-ttu-id="843aa-118">[Dodawanie powiadomień wypychanych do aplikacji mobilnej]: ../articles/app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md</span><span class="sxs-lookup"><span data-stu-id="843aa-118">[Add push notifications for Mobile Apps]: ../articles/app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md</span></span>
<span data-ttu-id="843aa-119">[jak używać usługi Notification Hubs za pomocą języka Java/PHP]: ../articles/notification-hubs/notification-hubs-java-push-notification-tutorial.md</span><span class="sxs-lookup"><span data-stu-id="843aa-119">[How to use Notification Hubs from Java/PHP]: ../articles/notification-hubs/notification-hubs-java-push-notification-tutorial.md</span></span>
<span data-ttu-id="843aa-120">[pakietu NuGet Microsoft.Azure.Notification Hubs]: http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/</span><span class="sxs-lookup"><span data-stu-id="843aa-120">[Microsoft.Azure.Notification Hubs NuGet package]: http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/</span></span>
