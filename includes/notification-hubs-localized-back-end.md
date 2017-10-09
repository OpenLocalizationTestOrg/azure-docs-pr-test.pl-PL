



Po wysłaniu szablonu powiadomień, się, że wystarczy tylko tooprovide zbiór właściwości, w tym przypadku wyślemy hello zbiór właściwości zawierający hello zlokalizowanej wersji bieżącej wiadomości powitania, na przykład:

    {
        "News_English": "World News in English!",
        "News_French": "World News in French!",
        "News_Mandarin": "World News in Mandarin!"
    }


W tej sekcji przedstawiono sposób toosend powiadomienia za pomocą aplikacji konsoli

Hello uwzględnione Sklep Windows tooboth emisje kodu i urządzeń z systemem iOS, ponieważ hello wewnętrznej bazy danych można emisji tooany hello obsługiwanych urządzeń.

### <a name="toosend-notifications-using-a-c-console-app"></a>toosend powiadomień przy użyciu aplikacji konsolowej C#
Modyfikowanie hello `SendTemplateNotificationAsync` w aplikacji konsoli hello wcześniej utworzony z powitania po kodzie metody. Zwróć uwagę, jak w tym przypadku nie ma toosend nie konieczności wielu powiadomienia dla innych języków i platform.

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


Należy pamiętać, że to proste wywołanie będzie dostarczać zlokalizowanych część wiadomości powitania zbyt**wszystkie** urządzenia, niezależnie od platformy hello jako kompilacje Centrum powiadomień, a następnie dostarcza hello poprawne subskrybowane natywnego ładunku tooall hello urządzeń tooa konkretnym elementem tag.

### <a name="sending-hello-notification-with-mobile-services"></a>Wysyłanie powiadomień hello w usłudze Mobile Services
W Twojej harmonogram usługi mobilnej można użyć hello następującego skryptu:

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


