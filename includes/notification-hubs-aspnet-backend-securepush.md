## <a name="webapi-project"></a><span data-ttu-id="47b84-101">WebAPI projektu</span><span class="sxs-lookup"><span data-stu-id="47b84-101">WebAPI Project</span></span>
1. <span data-ttu-id="47b84-102">W programie Visual Studio Otwórz hello **AppBackend** projektu, który został utworzony w hello **Powiadom użytkowników** samouczka.</span><span class="sxs-lookup"><span data-stu-id="47b84-102">In Visual Studio, open hello **AppBackend** project that you created in hello **Notify Users** tutorial.</span></span>
2. <span data-ttu-id="47b84-103">W Notifications.cs, Zastąp hello całego **powiadomienia** klasy z hello następującego kodu.</span><span class="sxs-lookup"><span data-stu-id="47b84-103">In Notifications.cs, replace hello whole **Notifications** class with hello following code.</span></span> <span data-ttu-id="47b84-104">Należy się symbole zastępcze hello tooreplace z parametrów połączenia dla Centrum powiadomień, a nazwa Centrum hello (z pełnym dostępem).</span><span class="sxs-lookup"><span data-stu-id="47b84-104">Be sure tooreplace hello placeholders with your connection string (with full access) for your notification hub, and hello hub name.</span></span> <span data-ttu-id="47b84-105">Te wartości można uzyskać z hello [klasycznego portalu Azure](http://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="47b84-105">You can obtain these values from hello [Azure Classic Portal](http://manage.windowsazure.com).</span></span> <span data-ttu-id="47b84-106">Ten moduł reprezentuje teraz hello różnych bezpieczne powiadomień, które będą wysyłane.</span><span class="sxs-lookup"><span data-stu-id="47b84-106">This module now represents hello different secure notifications that will be sent.</span></span> <span data-ttu-id="47b84-107">W pełnej implementacji hello powiadomienia będą przechowywane w bazie danych; dla uproszczenia w tym przypadku są przechowywane ich w pamięci.</span><span class="sxs-lookup"><span data-stu-id="47b84-107">In a complete implementation, hello notifications will be stored in a database; for simplicity, in this case we store them in memory.</span></span>
   
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

1. <span data-ttu-id="47b84-108">W NotificationsController.cs, Zastąp kod hello wewnątrz hello **NotificationsController** klasy definicji z hello następującego kodu.</span><span class="sxs-lookup"><span data-stu-id="47b84-108">In NotificationsController.cs, replace hello code inside hello **NotificationsController** class definition with hello following code.</span></span> <span data-ttu-id="47b84-109">Ten składnik implementuje bezpieczny sposób hello urządzenia tooretrieve hello powiadomienia o, a także tootrigger sposób (na potrzeby tego samouczka hello) urządzeń tooyour bezpiecznego wypychania.</span><span class="sxs-lookup"><span data-stu-id="47b84-109">This component implements a way for hello device tooretrieve hello notification securely, and also provides a way (for hello purposes of this tutorial) tootrigger a secure push tooyour devices.</span></span> <span data-ttu-id="47b84-110">Należy pamiętać, że podczas wysyłania Centrum powiadomień toohello powiadomień hello, tylko powiadomienie zostanie wysłane raw o identyfikatorze hello hello powiadomienia (i żaden komunikat rzeczywiste):</span><span class="sxs-lookup"><span data-stu-id="47b84-110">Note that when sending hello notification toohello notification hub, we only send a raw notification with hello ID of hello notification (and no actual message):</span></span>
   
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


<span data-ttu-id="47b84-111">Należy pamiętać, że hello `Post` metody teraz nie wysyłania wyskakujących powiadomień.</span><span class="sxs-lookup"><span data-stu-id="47b84-111">Note that hello `Post` method now does not send a toast notification.</span></span> <span data-ttu-id="47b84-112">Wysyła powiadomienie raw, które zawiera tylko hello identyfikator powiadomień, a nie poufną zawartością.</span><span class="sxs-lookup"><span data-stu-id="47b84-112">It sends a raw notification that contains only hello notification ID, and not any sensitive content.</span></span> <span data-ttu-id="47b84-113">Ponadto upewnij się, że toocomment hello operacji dla platform hello, dla których nie masz zostały skonfigurowane w Centrum powiadomień, jak będą powodować błędy wysyłania.</span><span class="sxs-lookup"><span data-stu-id="47b84-113">Also, make sure toocomment hello send operation for hello platforms for which you do not have credentials configured on your notification hub, as they will result in errors.</span></span>

1. <span data-ttu-id="47b84-114">Teraz ponownie wdrożymy ten tooan aplikacji witryny sieci Web Azure w kolejności toomake go ze wszystkich urządzeń.</span><span class="sxs-lookup"><span data-stu-id="47b84-114">Now we will re-deploy this app tooan Azure Website in order toomake it accessible from all devices.</span></span> <span data-ttu-id="47b84-115">Kliknij prawym przyciskiem myszy na powitania **AppBackend** projekt i wybierz **publikowania**.</span><span class="sxs-lookup"><span data-stu-id="47b84-115">Right-click on hello **AppBackend** project and select **Publish**.</span></span>
2. <span data-ttu-id="47b84-116">Wybierz urządzenie docelowe publikowania witryny sieci Web platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="47b84-116">Select Azure Website as your publish target.</span></span> <span data-ttu-id="47b84-117">Zaloguj się przy użyciu konta platformy Azure i wybierz istniejącą lub nową witrynę sieci Web i zanotuj hello **docelowy adres URL** właściwości w hello **połączenia** kartę. Odnoszą się adres URL toothis Twojego *wewnętrznej bazy danych punktu końcowego* dalszej części tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="47b84-117">Log in with your Azure account and select an existing or new Website, and make a note of hello **destination URL** property in hello **Connection** tab. We will refer toothis URL as your *backend endpoint* later in this tutorial.</span></span> <span data-ttu-id="47b84-118">Kliknij przycisk **Opublikuj**.</span><span class="sxs-lookup"><span data-stu-id="47b84-118">Click **Publish**.</span></span>

