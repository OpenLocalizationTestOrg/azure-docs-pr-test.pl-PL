## <a name="create-hello-webapi-project"></a>Utwórz hello WebAPI projektu
Nowego zaplecza ASP.NET WebAPI zostaną utworzone w kolejnych sekcjach hello i będzie mieć trzy główne cele:

1. **Uwierzytelnianie klientów**: program obsługi komunikatów zostanie dodany nowszych żądań klientów tooauthenticate i skojarz hello użytkownika z żądaniem hello.
2. **Rejestracje powiadomień klienta**: później, należy dodać kontroler toohandle nowe rejestracje klienta tooreceive powiadomień. Witaj nazwę uwierzytelnionego użytkownika zostanie automatycznie dodane rejestracji toohello jako [tag](https://msdn.microsoft.com/library/azure/dn530749.aspx).
3. **Wysyłanie powiadomień tooClients**: później zostaną dodane również tooprovide kontrolera sposób tootrigger użytkownika toodevices bezpiecznego wypychania i klientów skojarzonych z tagiem hello. 

Witaj następujące kroki pokazują, jak toocreate hello nowego zaplecza ASP.NET WebAPI: 

> [!IMPORTANT]
> Jeśli używasz programu Visual Studio 2015 lub starszym, przed rozpoczęciem tego samouczka, upewnij się, że zainstalowano najnowszą wersję hello hello Menedżera pakietów NuGet. toocheck, uruchamiania programu Visual Studio. Z hello **narzędzia** menu, kliknij przycisk **rozszerzenia i aktualizacje**. Wyszukaj **Menedżera pakietów NuGet** dla używanej wersji programu Visual Studio i upewnij się, że masz hello najnowszej wersji. Jeśli nie, odinstaluj, a następnie ponownie zainstalować hello Menedżera pakietów NuGet.
> 
> ![][B4]
> 
> [!NOTE]
> Upewnij się, że zainstalowano hello Visual Studio [zestawu Azure SDK](https://azure.microsoft.com/downloads/) wdrożenia witryny sieci Web.
> 
> 

1. Uruchom program Visual Studio lub Visual Studio Express. Kliknij przycisk **Eksploratora serwera** i zaloguj się na tooyour konto platformy Azure. Visual Studio będzie konieczne jest podpisany w zasobach witryny sieci web hello toocreate Twojego konta.
2. W programie Visual Studio, kliknij przycisk **pliku**, następnie kliknij przycisk **nowy**, następnie **projektu**, rozwiń węzeł **szablony**, **Visual C#**, następnie kliknij przycisk **sieci Web** i **aplikacji sieci Web ASP.NET**, nazwa typu hello **AppBackend**, a następnie kliknij przycisk **OK**. 
   
    ![][B1]
3. W hello **nowy projekt ASP.NET** okna dialogowego, kliknij przycisk **interfejsu API sieci Web**, następnie kliknij przycisk **OK**.
   
    ![][B2]
4. W hello **Konfigurowanie aplikacji sieci Web Microsoft Azure** okno dialogowe, wybierz subskrypcję, a **planu usługi aplikacji** zostały już utworzone. Można również wybrać **Utwórz nowy plan usługi aplikacji** i utwórz je z okna dialogowego hello. Ten samouczek nie wymaga bazy danych. Po wybraniu planu usługi aplikacji, kliknij przycisk **OK** toocreate hello projektu.
   
    ![][B5]

## <a name="authenticating-clients-toohello-webapi-backend"></a>Uwierzytelnianie klientów toohello WebAPI wewnętrznej bazy danych
W tej sekcji utworzysz nową klasę programu obsługi wiadomości o nazwie **AuthenticationTestHandler** dla hello nowego zaplecza. Ta klasa pochodzi od [DelegatingHandler](https://msdn.microsoft.com/library/system.net.http.delegatinghandler.aspx) i dodawane jako program obsługi komunikatów, więc może przetwarzać wszystkie żądania kierowane do hello wewnętrznej bazy danych. 

1. W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy hello **AppBackend** projektu, kliknij przycisk **Dodaj**, następnie kliknij przycisk **klasy**. Nazwa nowej klasy hello **AuthenticationTestHandler.cs**i kliknij przycisk **Dodaj** toogenerate hello klasy. Ta klasa będzie używana tooauthenticate użytkowników przy użyciu *uwierzytelnianie podstawowe* dla uproszczenia. Pamiętaj, że Twoja aplikacja może używać dowolnego schematu uwierzytelniania.
2. W AuthenticationTestHandler.cs, Dodaj następujące hello `using` instrukcji:
   
        using System.Net.Http;
        using System.Threading;
        using System.Security.Principal;
        using System.Net;
        using System.Text;
        using System.Threading.Tasks;

3. W AuthenticationTestHandler.cs, zastępując hello `AuthenticationTestHandler` klasy definicji z hello następującego kodu. 
   
    Ten program obsługi autoryzacji żądania hello gdy wszystkie spełnione są następujące trzy warunki hello:
   
   * Żądanie hello uwzględnione *autoryzacji* nagłówka. 
   * Żądanie hello używa *podstawowe* uwierzytelniania. 
   * ciąg nazwy użytkownika Hello i haśle hello są hello tych samych parametrach.
     
     W przeciwnym razie hello żądanie zostanie odrzucone. Nie jest to rzeczywiste podejście do uwierzytelniania i autoryzacji. Jest to bardzo prosty przykład na potrzeby tego samouczka.
     
     Jeśli komunikat żądania hello uwierzytelnieniu i autoryzacji przez hello `AuthenticationTestHandler`, hello uwierzytelnianie podstawowe użytkownika zostaną dołączone toohello bieżącego żądania na powitania [element HttpContext](https://msdn.microsoft.com/library/system.web.httpcontext.current.aspx). Informacje o użytkowniku w hello element HttpContext będzie używany przez inny kontroler (RegisterController) nowszego tooadd [tag](https://msdn.microsoft.com/library/azure/dn530749.aspx) żądanie rejestracji toohello powiadomień.
     
       public class AuthenticationTestHandler : DelegatingHandler   {       protected override Task<HttpResponseMessage> SendAsync(       HttpRequestMessage request, CancellationToken cancellationToken)       {           var authorizationHeader = request.Headers.GetValues("Authorization").First();
     
               if (authorizationHeader != null && authorizationHeader
                   .StartsWith("Basic ", StringComparison.InvariantCultureIgnoreCase))
               {
                   string authorizationUserAndPwdBase64 =
                       authorizationHeader.Substring("Basic ".Length);
                   string authorizationUserAndPwd = Encoding.Default
                       .GetString(Convert.FromBase64String(authorizationUserAndPwdBase64));
                   string user = authorizationUserAndPwd.Split(':')[0];
                   string password = authorizationUserAndPwd.Split(':')[1];
     
                   if (verifyUserAndPwd(user, password))
                   {
                       // Attach hello new principal object toohello current HttpContext object
                       HttpContext.Current.User =
                           new GenericPrincipal(new GenericIdentity(user), new string[0]);
                       System.Threading.Thread.CurrentPrincipal =
                           System.Web.HttpContext.Current.User;
                   }
                   else return Unauthorized();
               }
               else return Unauthorized();
     
               return base.SendAsync(request, cancellationToken);
           }
     
           private bool verifyUserAndPwd(string user, string password)
           {
               // This is not a real authentication scheme.
               return user == password;
           }
     
           private Task<HttpResponseMessage> Unauthorized()
           {
               var response = new HttpResponseMessage(HttpStatusCode.Forbidden);
               var tsc = new TaskCompletionSource<HttpResponseMessage>();
               tsc.SetResult(response);
               return tsc.Task;
           }
       }
     
     > [!NOTE]
     > **Uwaga dotycząca zabezpieczeń**: hello `AuthenticationTestHandler` klasa nie zapewnia uwierzytelniania wartość true. Jest używane tylko toomimic uwierzytelniania podstawowego i nie jest bezpieczna. W swoich aplikacjach i usługach produkcyjnych musisz zaimplementować mechanizm bezpiecznego uwierzytelniania.                
     > 
     > 
4. Dodaj następującego kodu na końcu hello hello hello `Register` metoda hello **App_Start/WebApiConfig.cs** obsługi wiadomości powitania tooregister klasy:
   
        config.MessageHandlers.Add(new AuthenticationTestHandler());
5. Zapisz zmiany.

## <a name="registering-for-notifications-using-hello-webapi-backend"></a>Rejestrowanie na potrzeby powiadomień za pomocą hello WebAPI wewnętrznej bazy danych
W tej sekcji dodamy nowe toohandle zaplecza WebAPI toohello kontrolera żądań tooregister użytkownika i urządzenie na potrzeby powiadomień dotyczących usługi notification hubs przy użyciu powitania klienta biblioteki. Kontroler Hello doda tag użytkownika dla użytkownika hello, który został uwierzytelniony i dołączyć toohello element HttpContext przez hello `AuthenticationTestHandler`. Hello tag będzie mieć format ciągu hello, `"username:<actual username>"`.

1. W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy hello **AppBackend** projektu, a następnie kliknij przycisk **Zarządzaj pakietami NuGet**.
2. Na powitania po lewej stronie, kliknij przycisk **Online**i wyszukaj **Microsoft.Azure.NotificationHubs** w hello **wyszukiwania** pole.
3. Kliknij na liście wyników hello **centra powiadomień Microsoft Azure**, a następnie kliknij przycisk **zainstalować**. Ukończenie instalacji hello, a następnie zamknij okno Menedżera pakietów NuGet hello.
   
    Spowoduje to dodanie toohello odwołanie do zestawu SDK usługi Azure Notification Hubs za pomocą hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">pakietu Microsoft.Azure.Notification Hubs NuGet</a>.
4. Teraz utworzymy nowy plik klasy reprezentujące hello połączenia z powiadomieniami toosend używane Centrum powiadomień. W Eksploratorze rozwiązań hello, kliknij prawym przyciskiem myszy hello **modele** folderu, kliknij przycisk **Dodaj**, następnie kliknij przycisk **klasy**. Nazwa nowej klasy hello **Notifications.cs**, następnie kliknij przycisk **Dodaj** toogenerate hello klasy. 
   
    ![][B6]
5. W Notifications.cs, Dodaj następujące hello `using` instrukcji u góry pliku hello hello:
   
        using Microsoft.Azure.NotificationHubs;
6. Zastąp hello `Notifications` klasy definicji hello następujący i wprowadzić symbole zastępcze hello dwa tooreplace się przy użyciu parametrów połączenia hello (z pełnym dostępem) dla Centrum powiadomień, a hello nazwy Centrum (dostępne pod adresem [klasycznego portalu Azure ](http://manage.windowsazure.com)):
   
        public class Notifications
        {
            public static Notifications Instance = new Notifications();
   
            public NotificationHubClient Hub { get; set; }
   
            private Notifications() {
                Hub = NotificationHubClient.CreateClientFromConnectionString("<your hub's DefaultFullSharedAccessSignature>", 
                                                                             "<hub name>");
            }
        }
7. Następnie utworzymy nowy kontroler o nazwie **RegisterController**. W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy hello **kontrolerów** folderu, następnie kliknij przycisk **Dodaj**, następnie kliknij przycisk **kontrolera**. Kliknij przycisk hello **kontroler 2 interfejsu API sieci Web — pusty** elementu, a następnie kliknij przycisk **Dodaj**. Nazwa nowej klasy hello **RegisterController**, a następnie kliknij przycisk **Dodaj** ponownie toogenerate hello kontrolera.
   
    ![][B7]
   
    ![][B8]
8. W RegisterController.cs, Dodaj następujące hello `using` instrukcji:
   
        using Microsoft.Azure.NotificationHubs;
        using Microsoft.Azure.NotificationHubs.Messaging;
        using AppBackend.Models;
        using System.Threading.Tasks;
        using System.Web;
9. Dodaj następujące kodu wewnątrz hello hello `RegisterController` definicji klasy. Należy pamiętać, że w tym kodzie, możemy dodać tag użytkownika dla użytkownika hello, który jest dołączony toohello element HttpContext. Hello użytkownik został uwierzytelniony i dołączony toohello element HttpContext przez filtr wiadomość hello dodaliśmy, `AuthenticationTestHandler`. Można również dodać tooverify kontroli opcjonalne, które hello użytkownika ma uprawnienia tooregister dla hello wymagane tagi.
   
        private NotificationHubClient hub;
   
        public RegisterController()
        {
            hub = Notifications.Instance.Hub;
        }
   
        public class DeviceRegistration
        {
            public string Platform { get; set; }
            public string Handle { get; set; }
            public string[] Tags { get; set; }
        }
   
        // POST api/register
        // This creates a registration id
        public async Task<string> Post(string handle = null)
        {
            string newRegistrationId = null;
   
            // make sure there are no existing registrations for this push handle (used for iOS and Android)
            if (handle != null)
            {
                var registrations = await hub.GetRegistrationsByChannelAsync(handle, 100);
   
                foreach (RegistrationDescription registration in registrations)
                {
                    if (newRegistrationId == null)
                    {
                        newRegistrationId = registration.RegistrationId;
                    }
                    else
                    {
                        await hub.DeleteRegistrationAsync(registration);
                    }
                }
            }
   
            if (newRegistrationId == null) 
                newRegistrationId = await hub.CreateRegistrationIdAsync();
   
            return newRegistrationId;
        }
   
        // PUT api/register/5
        // This creates or updates a registration (with provided channelURI) at hello specified id
        public async Task<HttpResponseMessage> Put(string id, DeviceRegistration deviceUpdate)
        {
            RegistrationDescription registration = null;
            switch (deviceUpdate.Platform)
            {
                case "mpns":
                    registration = new MpnsRegistrationDescription(deviceUpdate.Handle);
                    break;
                case "wns":
                    registration = new WindowsRegistrationDescription(deviceUpdate.Handle);
                    break;
                case "apns":
                    registration = new AppleRegistrationDescription(deviceUpdate.Handle);
                    break;
                case "gcm":
                    registration = new GcmRegistrationDescription(deviceUpdate.Handle);
                    break;
                default:
                    throw new HttpResponseException(HttpStatusCode.BadRequest);
            }
   
            registration.RegistrationId = id;
            var username = HttpContext.Current.User.Identity.Name;
   
            // add check if user is allowed tooadd these tags
            registration.Tags = new HashSet<string>(deviceUpdate.Tags);
            registration.Tags.Add("username:" + username);
   
            try
            {
                await hub.CreateOrUpdateRegistrationAsync(registration);
            }
            catch (MessagingException e)
            {
                ReturnGoneIfHubResponseIsGone(e);
            }
   
            return Request.CreateResponse(HttpStatusCode.OK);
        }
   
        // DELETE api/register/5
        public async Task<HttpResponseMessage> Delete(string id)
        {
            await hub.DeleteRegistrationAsync(id);
            return Request.CreateResponse(HttpStatusCode.OK);
        }
   
        private static void ReturnGoneIfHubResponseIsGone(MessagingException e)
        {
            var webex = e.InnerException as WebException;
            if (webex.Status == WebExceptionStatus.ProtocolError)
            {
                var response = (HttpWebResponse)webex.Response;
                if (response.StatusCode == HttpStatusCode.Gone)
                    throw new HttpRequestException(HttpStatusCode.Gone.ToString());
            }
        }
10. Zapisz zmiany.

## <a name="sending-notifications-from-hello-webapi-backend"></a>Wysyłanie powiadomień z zaplecza WebAPI hello
W tej sekcji możesz dodać nowego kontrolera, który opisuje sposób dla klienta urządzenia toosend powiadomienie oparte na powitania username tag przy użyciu Biblioteka zarządzania usługi centra powiadomień Azure w hello zaplecza ASP.NET WebAPI.

1. Utwórz kolejny nowy kontroler o nazwie **NotificationsController**. Utwórz go hello taki sam sposób utworzyć hello **RegisterController** w poprzedniej sekcji hello.
2. W NotificationsController.cs, Dodaj następujące hello `using` instrukcji:
   
        using AppBackend.Models;
        using System.Threading.Tasks;
        using System.Web;
3. Dodaj następujące metody toohello hello **NotificationsController** klasy.
   
    Ten kod wysyłania typ powiadomienia, oparte na powitania usługi powiadomień platformy (PNS) `pns` parametru. Witaj wartość `to_tag` jest używane tooset hello *username* tagu na wiadomość powitania. Ten tag musi być zgodny z tagiem username aktywnej rejestracji centrum powiadomień. komunikat z powiadomieniem Hello jest pobierane z hello treści żądania POST hello i sformatowany dla elementu docelowego hello systemu powiadomień platformy. 
   
    W zależności od hello czy obsługiwanych urządzeń, użyj tooreceive powiadomień platformy powiadomień usługi (PNS) różnych powiadomienia są obsługiwane przy użyciu różnych formatach. Na przykład w przypadku urządzeń z systemem Windows możesz użyć [wyskakujących powiadomień za pomocą usługi WNS](https://msdn.microsoft.com/library/windows/apps/br230849.aspx), które nie są bezpośrednio obsługiwane przez inną usługę PNS. Dzięki zaplecza musi tooformat hello powiadomień do obsługiwanych powiadomień dla hello systemu powiadomień platformy urządzeń, który planujesz toosupport. Następnie użyj interfejsu API wysyłania odpowiednie hello na powitania [NotificationHubClient — klasa](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.notificationhubclient_methods.aspx)
   
        public async Task<HttpResponseMessage> Post(string pns, [FromBody]string message, string to_tag)
        {
            var user = HttpContext.Current.User.Identity.Name;
            string[] userTag = new string[2];
            userTag[0] = "username:" + to_tag;
            userTag[1] = "from:" + user;
   
            Microsoft.Azure.NotificationHubs.NotificationOutcome outcome = null;
            HttpStatusCode ret = HttpStatusCode.InternalServerError;
   
            switch (pns.ToLower())
            {
                case "wns":
                    // Windows 8.1 / Windows Phone 8.1
                    var toast = @"<toast><visual><binding template=""ToastText01""><text id=""1"">" + 
                                "From " + user + ": " + message + "</text></binding></visual></toast>";
                    outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, userTag);
                    break;
                case "apns":
                    // iOS
                    var alert = "{\"aps\":{\"alert\":\"" + "From " + user + ": " + message + "\"}}";
                    outcome = await Notifications.Instance.Hub.SendAppleNativeNotificationAsync(alert, userTag);
                    break;
                case "gcm":
                    // Android
                    var notif = "{ \"data\" : {\"message\":\"" + "From " + user + ": " + message + "\"}}";
                    outcome = await Notifications.Instance.Hub.SendGcmNativeNotificationAsync(notif, userTag);
                    break;
            }
   
            if (outcome != null)
            {
                if (!((outcome.State == Microsoft.Azure.NotificationHubs.NotificationOutcomeState.Abandoned) ||
                    (outcome.State == Microsoft.Azure.NotificationHubs.NotificationOutcomeState.Unknown)))
                {
                    ret = HttpStatusCode.OK;
                }
            }
   
            return Request.CreateResponse(ret);
        }
4. Naciśnij klawisz **F5** toorun hello aplikacji i tooensure hello dokładność pracy wykonanej do tej pory. Aplikacja Hello powinno uruchomić przeglądarki sieci web i wyświetlenie strony głównej hello ASP.NET. 

## <a name="publish-hello-new-webapi-backend"></a>Publikowanie hello nowego zaplecza WebAPI
1. Teraz wdrożymy ten tooan aplikacji witryny sieci Web Azure w kolejności toomake go ze wszystkich urządzeń. Kliknij prawym przyciskiem myszy na powitania **AppBackend** projekt i wybierz **publikowania**.
2. Wybierz pozycję **Microsoft Azure App Service** jako docelową lokalizację publikacji, a następnie kliknij przycisk **Publikuj**. Zostanie otwarte okno dialogowe Tworzenie usługi App Service hello, które pomaga w utworzeniu wszystkich aplikacji sieci web serwera hello niezbędnych zasobów Azure toorun hello ASP.NET na platformie Azure.

    ![][B15]
3. W hello **Tworzenie usługi App Service** okno dialogowe, wybierz konto platformy Azure. Kliknij pozycję **Zmień typ** i wybierz pozycję **Aplikacja sieci Web**. Zachowaj hello **Nazwa aplikacji sieci Web** hello danego i wybierz pozycję **subskrypcji**, **grupy zasobów**, i **planu usługi App Service**.  Kliknij przycisk **Utwórz**.

4. Zanotuj hello **adres URL witryny** właściwości w hello **Podsumowanie** sekcji. Odnoszą się adres URL toothis Twojego *wewnętrznej bazy danych punktu końcowego* dalszej części tego samouczka. Kliknij przycisk **Opublikuj**.

5. Po zakończeniu pracy Kreatora hello, powoduje ona publikowanie tooAzure aplikacji sieci web ASP.NET hello, a następnie spowoduje uruchomienie hello aplikacji hello domyślnej przeglądarki.  Twoja aplikacja będzie widoczna w usłudze Azure App Service.

adres URL Hello używa hello Nazwa aplikacji sieci web, określony wcześniej, z hello format http://<app_name>.azurewebsites.net.

[B1]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push1.png
[B2]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push2.png
[B3]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push3.png
[B4]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push4.png
[B5]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push5.png
[B6]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push6.png
[B7]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push7.png
[B8]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push8.png
[B14]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push14.png
[B15]: ./media/notification-hubs-aspnet-backend-notifyusers/publish-to-app-service.png
[B16]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-notify-users16.PNG
[B18]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-notify-users18.PNG
