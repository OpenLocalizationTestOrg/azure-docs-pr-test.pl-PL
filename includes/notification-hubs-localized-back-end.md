



<span data-ttu-id="51e3d-101">Po wysłaniu szablonu powiadomień, się, że wystarczy tylko tooprovide zbiór właściwości, w tym przypadku wyślemy hello zbiór właściwości zawierający hello zlokalizowanej wersji bieżącej wiadomości powitania, na przykład:</span><span class="sxs-lookup"><span data-stu-id="51e3d-101">When you send template notifications you only need tooprovide a set of properties, in our case we will send hello set of properties containing hello localized version of hello current news, for instance:</span></span>

    {
        "News_English": "World News in English!",
        "News_French": "World News in French!",
        "News_Mandarin": "World News in Mandarin!"
    }


<span data-ttu-id="51e3d-102">W tej sekcji przedstawiono sposób toosend powiadomienia za pomocą aplikacji konsoli</span><span class="sxs-lookup"><span data-stu-id="51e3d-102">This section shows how toosend notifications using a console app</span></span>

<span data-ttu-id="51e3d-103">Hello uwzględnione Sklep Windows tooboth emisje kodu i urządzeń z systemem iOS, ponieważ hello wewnętrznej bazy danych można emisji tooany hello obsługiwanych urządzeń.</span><span class="sxs-lookup"><span data-stu-id="51e3d-103">hello included code broadcasts tooboth Windows Store and iOS devices, since hello backend can broadcast tooany of hello supported devices.</span></span>

### <a name="toosend-notifications-using-a-c-console-app"></a><span data-ttu-id="51e3d-104">toosend powiadomień przy użyciu aplikacji konsolowej C#</span><span class="sxs-lookup"><span data-stu-id="51e3d-104">toosend notifications using a C# console app</span></span>
<span data-ttu-id="51e3d-105">Modyfikowanie hello `SendTemplateNotificationAsync` w aplikacji konsoli hello wcześniej utworzony z powitania po kodzie metody.</span><span class="sxs-lookup"><span data-stu-id="51e3d-105">Modify hello `SendTemplateNotificationAsync` method in hello console app you previously created with hello following code.</span></span> <span data-ttu-id="51e3d-106">Zwróć uwagę, jak w tym przypadku nie ma toosend nie konieczności wielu powiadomienia dla innych języków i platform.</span><span class="sxs-lookup"><span data-stu-id="51e3d-106">Notice how in this case there is no need toosend multiple notifications for different locales and platforms.</span></span>

        private static async void SendTemplateNotificationAsync()
        {
            // Define hello notification hub.
            NotificationHubClient hub = 
                NotificationHubClient.CreateClientFromConnectionString(
                    "<connection string with full access>", "<hub name>");

            // Sending hello notification as a template notification. All template registrations that contain 
            // "messageParam" or "News_<local selected>" and hello proper tags will receive hello notifications. 
            // This includes APNS, GCM, WNS, and MPNS template registrations.
            Dictionary<string, string> templateParams = new Dictionary<string, string>();

            // Create an array of breaking news categories.
            var categories = new string[] { "World", "Politics", "Business", "Technology", "Science", "Sports"};
            var locales = new string[] { "English", "French", "Mandarin" };

            foreach (var category in categories)
            {
                templateParams["messageParam"] = "Breaking " + category + " News!";

                // Sending localized News for each tag too...
                foreach( var locale in locales)
                {
                    string key = "News_" + locale;

                    // Your real localized news content would go here.
                    templateParams[key] = "Breaking " + category + " News in " + locale + "!";
                }

                await hub.SendTemplateNotificationAsync(templateParams, category);
            }
        }


<span data-ttu-id="51e3d-107">Należy pamiętać, że to proste wywołanie będzie dostarczać zlokalizowanych część wiadomości powitania zbyt**wszystkie** urządzenia, niezależnie od platformy hello jako kompilacje Centrum powiadomień, a następnie dostarcza hello poprawne subskrybowane natywnego ładunku tooall hello urządzeń tooa konkretnym elementem tag.</span><span class="sxs-lookup"><span data-stu-id="51e3d-107">Note that this simple call will deliver hello localized piece of news too**all** your devices, irrespective of hello platform, as your Notification Hub builds and delivers hello correct native payload tooall hello devices subscribed tooa specific tag.</span></span>

### <a name="sending-hello-notification-with-mobile-services"></a><span data-ttu-id="51e3d-108">Wysyłanie powiadomień hello w usłudze Mobile Services</span><span class="sxs-lookup"><span data-stu-id="51e3d-108">Sending hello notification with Mobile Services</span></span>
<span data-ttu-id="51e3d-109">W Twojej harmonogram usługi mobilnej można użyć hello następującego skryptu:</span><span class="sxs-lookup"><span data-stu-id="51e3d-109">In your Mobile Service scheduler, you can use hello following script:</span></span>

    var azure = require('azure');
    var notificationHubService = azure.createNotificationHubService('<hub name>', '<connection string with full access>');
    var notification = {
            "News_English": "World News in English!",
            "News_French": "World News in French!",
            "News_Mandarin", "World News in Mandarin!"
    }
    notificationHubService.send('World', notification, function(error) {
        if (!error) {
            console.warn("Notification successful");
        }
    });


