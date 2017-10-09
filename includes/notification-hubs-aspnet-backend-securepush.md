## <a name="webapi-project"></a>WebAPI projektu
1. W programie Visual Studio Otwórz hello **AppBackend** projektu, który został utworzony w hello **Powiadom użytkowników** samouczka.
2. W Notifications.cs, Zastąp hello całego **powiadomienia** klasy z hello następującego kodu. Należy się symbole zastępcze hello tooreplace z parametrów połączenia dla Centrum powiadomień, a nazwa Centrum hello (z pełnym dostępem). Te wartości można uzyskać z hello [klasycznego portalu Azure](http://manage.windowsazure.com). Ten moduł reprezentuje teraz hello różnych bezpieczne powiadomień, które będą wysyłane. W pełnej implementacji hello powiadomienia będą przechowywane w bazie danych; dla uproszczenia w tym przypadku są przechowywane ich w pamięci.
   
        public class Notification
        {
            public int Id { get; set; }
            public string Payload { get; set; }
            public bool Read { get; set; }
        }

        public class Notifications
        {
            public static Notifications Instance = new Notifications();

            private List<Notification> notifications = new List<Notification>();

            public NotificationHubClient Hub { get; set; }

            private Notifications() {
                Hub = NotificationHubClient.CreateClientFromConnectionString("{conn string with full access}",     "{hub name}");
            }

            public Notification CreateNotification(string payload)
            {
                var notification = new Notification() {
                Id = notifications.Count,
                Payload = payload,
                Read = false
                };

                notifications.Add(notification);

                return notification;
            }

            public Notification ReadNotification(int id)
            {
                return notifications.ElementAt(id);
            }
        }

1. W NotificationsController.cs, Zastąp kod hello wewnątrz hello **NotificationsController** klasy definicji z hello następującego kodu. Ten składnik implementuje bezpieczny sposób hello urządzenia tooretrieve hello powiadomienia o, a także tootrigger sposób (na potrzeby tego samouczka hello) urządzeń tooyour bezpiecznego wypychania. Należy pamiętać, że podczas wysyłania Centrum powiadomień toohello powiadomień hello, tylko powiadomienie zostanie wysłane raw o identyfikatorze hello hello powiadomienia (i żaden komunikat rzeczywiste):
   
       public NotificationsController()
       {
           Notifications.Instance.CreateNotification("This is a secure notification!");
       }
   
       // GET api/notifications/id
       public Notification Get(int id)
       {
           return Notifications.Instance.ReadNotification(id);
       }
   
       public async Task<HttpResponseMessage> Post()
       {
           var secureNotificationInTheBackend = Notifications.Instance.CreateNotification("Secure confirmation.");
           var usernameTag = "username:" + HttpContext.Current.User.Identity.Name;
   
           // windows
           var rawNotificationToBeSent = new Microsoft.Azure.NotificationHubs.WindowsNotification(secureNotificationInTheBackend.Id.ToString(),
                           new Dictionary<string, string> {
                               {"X-WNS-Type", "wns/raw"}
                           });
           await Notifications.Instance.Hub.SendNotificationAsync(rawNotificationToBeSent, usernameTag);
   
           // apns
           await Notifications.Instance.Hub.SendAppleNativeNotificationAsync("{\"aps\": {\"content-available\": 1}, \"secureId\": \"" + secureNotificationInTheBackend.Id.ToString() + "\"}", usernameTag);
   
           // gcm
           await Notifications.Instance.Hub.SendGcmNativeNotificationAsync("{\"data\": {\"secureId\": \"" + secureNotificationInTheBackend.Id.ToString() + "\"}}", usernameTag);

            return Request.CreateResponse(HttpStatusCode.OK);
        }


Należy pamiętać, że hello `Post` metody teraz nie wysyłania wyskakujących powiadomień. Wysyła powiadomienie raw, które zawiera tylko hello identyfikator powiadomień, a nie poufną zawartością. Ponadto upewnij się, że toocomment hello operacji dla platform hello, dla których nie masz zostały skonfigurowane w Centrum powiadomień, jak będą powodować błędy wysyłania.

1. Teraz ponownie wdrożymy ten tooan aplikacji witryny sieci Web Azure w kolejności toomake go ze wszystkich urządzeń. Kliknij prawym przyciskiem myszy na powitania **AppBackend** projekt i wybierz **publikowania**.
2. Wybierz urządzenie docelowe publikowania witryny sieci Web platformy Azure. Zaloguj się przy użyciu konta platformy Azure i wybierz istniejącą lub nową witrynę sieci Web i zanotuj hello **docelowy adres URL** właściwości w hello **połączenia** kartę. Odnoszą się adres URL toothis Twojego *wewnętrznej bazy danych punktu końcowego* dalszej części tego samouczka. Kliknij przycisk **Opublikuj**.

