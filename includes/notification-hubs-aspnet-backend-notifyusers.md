## <a name="create-the-webapi-project"></a><span data-ttu-id="148fb-101">Tworzenie projektu interfejsu WebAPI</span><span class="sxs-lookup"><span data-stu-id="148fb-101">Create the WebAPI Project</span></span>
<span data-ttu-id="148fb-102">W kolejnych sekcjach zostanie utworzone nowe zaplecze interfejsu WebAPI w strukturze ASP.NET, które będzie mieć trzy główne funkcje:</span><span class="sxs-lookup"><span data-stu-id="148fb-102">A new ASP.NET WebAPI backend will be created in the sections that follow and it will have three main purposes:</span></span>

1. <span data-ttu-id="148fb-103">**Uwierzytelnianie klientów**: później zostanie dodana procedura obsługi komunikatów w celu uwierzytelnienia żądań klientów i kojarzenia użytkownika z żądaniem.</span><span class="sxs-lookup"><span data-stu-id="148fb-103">**Authenticating Clients**: A message handler will be added later to authenticate client requests and associate the user with the request.</span></span>
2. <span data-ttu-id="148fb-104">**Rejestracje powiadomień klienta**: później dodasz kontroler do obsługi nowych rejestracji, aby urządzenie klienckie mogło otrzymywać powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="148fb-104">**Client Notification Registrations**: Later, you will add a controller to handle new registrations for a client device to receive notifications.</span></span> <span data-ttu-id="148fb-105">Nazwa uwierzytelnionego użytkownika zostanie automatycznie dodana do rejestracji jako [tag](https://msdn.microsoft.com/library/azure/dn530749.aspx).</span><span class="sxs-lookup"><span data-stu-id="148fb-105">The authenticated user name will automatically be added to the registration as a [tag](https://msdn.microsoft.com/library/azure/dn530749.aspx).</span></span>
3. <span data-ttu-id="148fb-106">**Wysyłanie powiadomień do klientów**: później dodasz również kontroler udostępniający użytkownikom możliwość wyzwalania bezpiecznej operacji wypychania do urządzeń i klientów skojarzonych z tagiem.</span><span class="sxs-lookup"><span data-stu-id="148fb-106">**Sending Notifications to Clients**: Later, you will also add a controller to provide a way for a user to trigger a secure push to devices and clients associated with the tag.</span></span> 

<span data-ttu-id="148fb-107">W następujących krokach przedstawiono sposób tworzenia nowego zaplecza interfejsu WebAPI w strukturze ASP.NET:</span><span class="sxs-lookup"><span data-stu-id="148fb-107">The following steps show how to create the new ASP.NET WebAPI backend:</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="148fb-108">Jeśli używasz programu Visual Studio 2015 lub starszego, przed rozpoczęciem tego samouczka upewnij się, że masz zainstalowaną najnowszą wersję Menedżera pakietów NuGet.</span><span class="sxs-lookup"><span data-stu-id="148fb-108">If you are using Visual Studio 2015 or earlier, before starting this tutorial, please ensure that you have installed the latest version of the NuGet Package Manager.</span></span> <span data-ttu-id="148fb-109">Aby to sprawdzić, uruchom program Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="148fb-109">To check, start Visual Studio.</span></span> <span data-ttu-id="148fb-110">W menu **Narzędzia** kliknij polecenie **Rozszerzenia i aktualizacje**.</span><span class="sxs-lookup"><span data-stu-id="148fb-110">From the **Tools** menu, click **Extensions and Updates**.</span></span> <span data-ttu-id="148fb-111">Wyszukaj pozycję **Menedżer pakietów NuGet** dla używanej przez Ciebie wersji programu Visual Studio i sprawdź, czy masz najnowszą wersję.</span><span class="sxs-lookup"><span data-stu-id="148fb-111">Search for **NuGet Package Manager** for your version of Visual Studio, and make sure you have the latest version.</span></span> <span data-ttu-id="148fb-112">Jeśli nie, odinstaluj, a następnie ponownie zainstaluj Menedżera pakietów NuGet.</span><span class="sxs-lookup"><span data-stu-id="148fb-112">If not, please uninstall, then reinstall the NuGet Package Manager.</span></span>
> 
> ![][B4]
> 
> [!NOTE]
> <span data-ttu-id="148fb-113">Upewnij się, że masz zainstalowany [zestaw Azure SDK](https://azure.microsoft.com/downloads/) programu Visual Studio na potrzeby wdrażania witryny internetowej.</span><span class="sxs-lookup"><span data-stu-id="148fb-113">Make sure you have installed the Visual Studio [Azure SDK](https://azure.microsoft.com/downloads/) for website deployment.</span></span>
> 
> 

1. <span data-ttu-id="148fb-114">Uruchom program Visual Studio lub Visual Studio Express.</span><span class="sxs-lookup"><span data-stu-id="148fb-114">Start Visual Studio or Visual Studio Express.</span></span> <span data-ttu-id="148fb-115">Kliknij pozycję **Eksplorator serwera** i zaloguj się do konta platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="148fb-115">Click **Server Explorer** and sign in to your Azure account.</span></span> <span data-ttu-id="148fb-116">Program Visual Studio będzie wymagał zalogowania w celu tworzenia zasobów witryny internetowej na Twoim koncie.</span><span class="sxs-lookup"><span data-stu-id="148fb-116">Visual Studio will need you signed in to create the web site resources on your account.</span></span>
2. <span data-ttu-id="148fb-117">W programie Visual Studio kliknij pozycję **Plik**, a następnie kliknij polecenie **Nowy** i **Projekt**. Rozwiń węzeł **Szablony**, **Visual C#**, kliknij pozycję **Sieć Web** i **Aplikacja sieci Web ASP.NET**, wpisz nazwę **AppBackend**, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="148fb-117">In Visual Studio, click **File**, then click **New**, then **Project**, expand **Templates**, **Visual C#**, then click **Web** and **ASP.NET Web Application**, type the name **AppBackend**, and then click **OK**.</span></span> 
   
    ![][B1]
3. <span data-ttu-id="148fb-118">W oknie dialogowym **Nowy projekt ASP.NET** kliknij pozycję **Interfejs API sieci Web**, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="148fb-118">In the **New ASP.NET Project** dialog, click **Web API**, then click **OK**.</span></span>
   
    ![][B2]
4. <span data-ttu-id="148fb-119">W oknie dialogowym **Konfiguruj aplikację sieci Web platformy Microsoft Azure** wybierz subskrypcję i **Plan usługi App Service**, który już został utworzony.</span><span class="sxs-lookup"><span data-stu-id="148fb-119">In the **Configure Microsoft Azure Web App** dialog, choose a subscription, and an **App Service plan** you have already created.</span></span> <span data-ttu-id="148fb-120">Możesz również wybrać pozycję **Utwórz nowy plan usługi App Service** i utworzyć go w oknie dialogowym.</span><span class="sxs-lookup"><span data-stu-id="148fb-120">You can also choose **Create a new app service plan** and create one from the dialog.</span></span> <span data-ttu-id="148fb-121">Ten samouczek nie wymaga bazy danych.</span><span class="sxs-lookup"><span data-stu-id="148fb-121">You do not need a database for this tutorial.</span></span> <span data-ttu-id="148fb-122">Po wybraniu planu usługi App Service kliknij przycisk **OK**, aby utworzyć projekt.</span><span class="sxs-lookup"><span data-stu-id="148fb-122">Once you have selected your app service plan, click **OK** to create the project.</span></span>
   
    ![][B5]

## <a name="authenticating-clients-to-the-webapi-backend"></a><span data-ttu-id="148fb-123">Uwierzytelnianie klientów w zapleczu interfejsu WebAPI</span><span class="sxs-lookup"><span data-stu-id="148fb-123">Authenticating Clients to the WebAPI Backend</span></span>
<span data-ttu-id="148fb-124">W tej sekcji utworzysz nową klasę procedury obsługi komunikatów o nazwie **AuthenticationTestHandler** dla nowego zaplecza.</span><span class="sxs-lookup"><span data-stu-id="148fb-124">In this section, you will create a new message handler class named **AuthenticationTestHandler** for the new backend.</span></span> <span data-ttu-id="148fb-125">Ta klasa pochodzi od klasy [DelegatingHandler](https://msdn.microsoft.com/library/system.net.http.delegatinghandler.aspx) i jest dodawana jako procedura obsługi komunikatów na potrzeby przetwarzania wszystkich żądań przychodzących do zaplecza.</span><span class="sxs-lookup"><span data-stu-id="148fb-125">This class is derived from [DelegatingHandler](https://msdn.microsoft.com/library/system.net.http.delegatinghandler.aspx) and added as a message handler so it can process all requests coming into the backend.</span></span> 

1. <span data-ttu-id="148fb-126">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy projekt **AppBackend**, kliknij polecenie **Dodaj**, a następnie kliknij pozycję **Klasa**.</span><span class="sxs-lookup"><span data-stu-id="148fb-126">In Solution Explorer, right-click the **AppBackend** project, click **Add**, then click **Class**.</span></span> <span data-ttu-id="148fb-127">Nadaj nowej klasie nazwę **AuthenticationTestHandler.cs**, a następnie kliknij przycisk **Dodaj**, aby wygenerować klasę.</span><span class="sxs-lookup"><span data-stu-id="148fb-127">Name the new class **AuthenticationTestHandler.cs**, and click **Add** to generate the class.</span></span> <span data-ttu-id="148fb-128">Ta klasa będzie używana do uwierzytelniania użytkowników za pomocą *Uwierzytelniania podstawowego* dla uproszczenia.</span><span class="sxs-lookup"><span data-stu-id="148fb-128">This class will be used to authenticate users using *Basic Authentication* for simplicity.</span></span> <span data-ttu-id="148fb-129">Pamiętaj, że Twoja aplikacja może używać dowolnego schematu uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="148fb-129">Note that your app can use any authentication scheme.</span></span>
2. <span data-ttu-id="148fb-130">W klasie AuthenticationTestHandler.cs dodaj następujące instrukcje `using`:</span><span class="sxs-lookup"><span data-stu-id="148fb-130">In AuthenticationTestHandler.cs, add the following `using` statements:</span></span>
   
        using System.Net.Http;
        using System.Threading;
        using System.Security.Principal;
        using System.Net;
        using System.Text;
        using System.Threading.Tasks;

3. <span data-ttu-id="148fb-131">W klasie AuthenticationTestHandler.cs zastąp definicję klasy `AuthenticationTestHandler` następującym kodem.</span><span class="sxs-lookup"><span data-stu-id="148fb-131">In AuthenticationTestHandler.cs, replacing the `AuthenticationTestHandler` class definition with the following code.</span></span> 
   
    <span data-ttu-id="148fb-132">Ta procedura obsługi będzie autoryzować żądania, gdy wszystkie trzy następujące warunki będą spełnione:</span><span class="sxs-lookup"><span data-stu-id="148fb-132">This handler will authorize the request when the following three conditions are all true:</span></span>
   
   * <span data-ttu-id="148fb-133">Żądanie zawiera nagłówek *Authorization*.</span><span class="sxs-lookup"><span data-stu-id="148fb-133">The request included an *Authorization* header.</span></span> 
   * <span data-ttu-id="148fb-134">Żądanie używa uwierzytelniania *basic*.</span><span class="sxs-lookup"><span data-stu-id="148fb-134">The request uses *basic* authentication.</span></span> 
   * <span data-ttu-id="148fb-135">Ciąg nazwy użytkownika i ciąg hasła to ten sam ciąg.</span><span class="sxs-lookup"><span data-stu-id="148fb-135">The user name string and the password string are the same string.</span></span>
     
     <span data-ttu-id="148fb-136">W przeciwnym razie żądanie zostanie odrzucone.</span><span class="sxs-lookup"><span data-stu-id="148fb-136">Otherwise, the request will be rejected.</span></span> <span data-ttu-id="148fb-137">Nie jest to rzeczywiste podejście do uwierzytelniania i autoryzacji.</span><span class="sxs-lookup"><span data-stu-id="148fb-137">This is not a true authentication and authorization approach.</span></span> <span data-ttu-id="148fb-138">Jest to bardzo prosty przykład na potrzeby tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="148fb-138">It is just a very simple example for this tutorial.</span></span>
     
     <span data-ttu-id="148fb-139">Jeśli komunikat żądania zostanie uwierzytelniony i autoryzowany przez klasę `AuthenticationTestHandler`, użytkownik podstawowego uwierzytelniania zostanie dołączony do bieżącego żądania w obiekcie [HttpContext](https://msdn.microsoft.com/library/system.web.httpcontext.current.aspx).</span><span class="sxs-lookup"><span data-stu-id="148fb-139">If the request message is authenticated and authorized by the `AuthenticationTestHandler`, then the basic authentication user will be attached to the current request on the [HttpContext](https://msdn.microsoft.com/library/system.web.httpcontext.current.aspx).</span></span> <span data-ttu-id="148fb-140">Informacje o użytkowniku w obiekcie HttpContext zostaną później użyte przez inny kontroler (RegisterController) w celu dodania [tagu](https://msdn.microsoft.com/library/azure/dn530749.aspx) do żądania rejestracji powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="148fb-140">User information in the HttpContext will be used by another controller (RegisterController) later to add a [tag](https://msdn.microsoft.com/library/azure/dn530749.aspx) to the notification registration request.</span></span>
     
       <span data-ttu-id="148fb-141">public class AuthenticationTestHandler : DelegatingHandler   {       protected override Task<HttpResponseMessage> SendAsync(       HttpRequestMessage request, CancellationToken cancellationToken)       {           var authorizationHeader = request.Headers.GetValues("Authorization").First();</span><span class="sxs-lookup"><span data-stu-id="148fb-141">public class AuthenticationTestHandler : DelegatingHandler   {       protected override Task<HttpResponseMessage> SendAsync(       HttpRequestMessage request, CancellationToken cancellationToken)       {           var authorizationHeader = request.Headers.GetValues("Authorization").First();</span></span>
     
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
                       // Attach the new principal object to the current HttpContext object
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
       <span data-ttu-id="148fb-142">}</span><span class="sxs-lookup"><span data-stu-id="148fb-142">}</span></span>
     
     > [!NOTE]
     > <span data-ttu-id="148fb-143">**Uwaga dotycząca zabezpieczeń**: Klasa `AuthenticationTestHandler` nie zapewnia rzeczywistego uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="148fb-143">**Security Note**: The `AuthenticationTestHandler` class does not provide true authentication.</span></span> <span data-ttu-id="148fb-144">Jest ona używana tylko do naśladowania uwierzytelniania podstawowego i nie jest bezpieczna.</span><span class="sxs-lookup"><span data-stu-id="148fb-144">It is used only to mimic basic authentication and is not secure.</span></span> <span data-ttu-id="148fb-145">W swoich aplikacjach i usługach produkcyjnych musisz zaimplementować mechanizm bezpiecznego uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="148fb-145">You must implement a secure authentication mechanism in your production applications and services.</span></span>                
     > 
     > 
4. <span data-ttu-id="148fb-146">Dodaj następujący kod na końcu metody `Register` w klasie **App_Start/WebApiConfig.cs**, aby zarejestrować procedurę obsługi komunikatów:</span><span class="sxs-lookup"><span data-stu-id="148fb-146">Add the following code at the end of the `Register` method in the **App_Start/WebApiConfig.cs** class to register the message handler:</span></span>
   
        config.MessageHandlers.Add(new AuthenticationTestHandler());
5. <span data-ttu-id="148fb-147">Zapisz zmiany.</span><span class="sxs-lookup"><span data-stu-id="148fb-147">Save your changes.</span></span>

## <a name="registering-for-notifications-using-the-webapi-backend"></a><span data-ttu-id="148fb-148">Rejestrowanie na potrzeby powiadomień za pomocą zaplecza interfejsu WebAPI</span><span class="sxs-lookup"><span data-stu-id="148fb-148">Registering for Notifications using the WebAPI Backend</span></span>
<span data-ttu-id="148fb-149">W tej sekcji dodamy nowy kontroler do zaplecza interfejsu WebAPI w celu obsługi żądań rejestracji użytkownika i urządzenia do otrzymywania powiadomień przy użyciu biblioteki klienta dla centrów powiadomień.</span><span class="sxs-lookup"><span data-stu-id="148fb-149">In this section, we will add a new controller to the WebAPI backend to handle requests to register a user and device for notifications using the client library for notification hubs.</span></span> <span data-ttu-id="148fb-150">Kontroler doda tag użytkownika, który został uwierzytelniony i dołączony do obiektu HttpContext przez klasę `AuthenticationTestHandler`.</span><span class="sxs-lookup"><span data-stu-id="148fb-150">The controller will add a user tag for the user that was authenticated and attached to the HttpContext by the `AuthenticationTestHandler`.</span></span> <span data-ttu-id="148fb-151">Tag będzie miał format ciągu `"username:<actual username>"`.</span><span class="sxs-lookup"><span data-stu-id="148fb-151">The tag will have the string format, `"username:<actual username>"`.</span></span>

1. <span data-ttu-id="148fb-152">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy projekt **AppBackend**, a następnie kliknij polecenie **Zarządzaj pakietami NuGet**.</span><span class="sxs-lookup"><span data-stu-id="148fb-152">In Solution Explorer, right-click the **AppBackend** project and then click **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="148fb-153">Po lewej stronie kliknij pozycję **Online** i wyszukaj ciąg **Microsoft.Azure.NotificationHubs** w polu **Wyszukaj**.</span><span class="sxs-lookup"><span data-stu-id="148fb-153">On the left-hand side, click **Online**, and search for **Microsoft.Azure.NotificationHubs** in the **Search** box.</span></span>
3. <span data-ttu-id="148fb-154">Na liście wyników kliknij pozycję **Microsoft Azure Notification Hubs**, a następnie kliknij pozycję **Instaluj**.</span><span class="sxs-lookup"><span data-stu-id="148fb-154">In the results list, click **Microsoft Azure Notification Hubs**, and then click **Install**.</span></span> <span data-ttu-id="148fb-155">Zakończ instalację, a następnie zamknij okno menedżera pakietów NuGet.</span><span class="sxs-lookup"><span data-stu-id="148fb-155">Complete the installation, then close the NuGet package manager window.</span></span>
   
    <span data-ttu-id="148fb-156">Spowoduje to dodanie odwołania do zestawu SDK usługi Azure Notification Hubs z użyciem <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">pakietu NuGet Microsoft.Azure.Notification Hubs</a>.</span><span class="sxs-lookup"><span data-stu-id="148fb-156">This adds a reference to the Azure Notification Hubs SDK using the <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet package</a>.</span></span>
4. <span data-ttu-id="148fb-157">Teraz utworzymy plik nowej klasy, która reprezentuje połączenie z centrum powiadomień używane do wysyłania powiadomień.</span><span class="sxs-lookup"><span data-stu-id="148fb-157">We will now create a new class file that represents the connection with notification hub used to send notifications.</span></span> <span data-ttu-id="148fb-158">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy folder **Modele**, kliknij polecenie **Dodaj**, a następnie kliknij pozycję **Klasa**.</span><span class="sxs-lookup"><span data-stu-id="148fb-158">In the Solution Explorer, right-click the **Models** folder, click **Add**, then click **Class**.</span></span> <span data-ttu-id="148fb-159">Nadaj nowej klasie nazwę **Notifications.cs**, a następnie kliknij przycisk **Dodaj**, aby wygenerować klasę.</span><span class="sxs-lookup"><span data-stu-id="148fb-159">Name the new class **Notifications.cs**, then click **Add** to generate the class.</span></span> 
   
    ![][B6]
5. <span data-ttu-id="148fb-160">W klasie Notifications.cs dodaj następującą instrukcję `using` na początku pliku:</span><span class="sxs-lookup"><span data-stu-id="148fb-160">In Notifications.cs, add the following `using` statement at the top of the file:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
6. <span data-ttu-id="148fb-161">Zastąp definicję klasy `Notifications` poniższą definicją i pamiętaj o zastąpieniu dwóch symboli zastępczych parametrami połączenia (z pełnym dostępem) dla Twojego centrum powiadomień i nazwą centrum (dostępną w [klasycznej witrynie Azure Portal](http://manage.windowsazure.com)):</span><span class="sxs-lookup"><span data-stu-id="148fb-161">Replace the `Notifications` class definition with the following and make sure to replace the two placeholders with the connection string (with full access) for your notification hub, and the hub name (available at [Azure Classic Portal](http://manage.windowsazure.com)):</span></span>
   
        public class Notifications
        {
            public static Notifications Instance = new Notifications();
   
            public NotificationHubClient Hub { get; set; }
   
            private Notifications() {
                Hub = NotificationHubClient.CreateClientFromConnectionString("<your hub's DefaultFullSharedAccessSignature>", 
                                                                             "<hub name>");
            }
        }
7. <span data-ttu-id="148fb-162">Następnie utworzymy nowy kontroler o nazwie **RegisterController**.</span><span class="sxs-lookup"><span data-stu-id="148fb-162">Next we will create a new controller named **RegisterController**.</span></span> <span data-ttu-id="148fb-163">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy folder **Kontrolery**, po czym kliknij polecenie **Dodaj**, a następnie kliknij pozycję **Kontroler**.</span><span class="sxs-lookup"><span data-stu-id="148fb-163">In Solution Explorer, right-click the **Controllers** folder, then click **Add**, then click **Controller**.</span></span> <span data-ttu-id="148fb-164">Kliknij pozycję **Kontroler internetowego interfejsu API 2 — pusty**, a następnie kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="148fb-164">Click the **Web API 2 Controller -- Empty** item, and then click **Add**.</span></span> <span data-ttu-id="148fb-165">Nadaj nowej klasie nazwę **RegisterController**, a następnie ponownie kliknij przycisk **Dodaj**, aby wygenerować kontroler.</span><span class="sxs-lookup"><span data-stu-id="148fb-165">Name the new class **RegisterController**, and then click **Add** again to generate the controller.</span></span>
   
    ![][B7]
   
    ![][B8]
8. <span data-ttu-id="148fb-166">W pliku RegisterController.cs dodaj następujące instrukcje `using`:</span><span class="sxs-lookup"><span data-stu-id="148fb-166">In RegisterController.cs, add the following `using` statements:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
        using Microsoft.Azure.NotificationHubs.Messaging;
        using AppBackend.Models;
        using System.Threading.Tasks;
        using System.Web;
9. <span data-ttu-id="148fb-167">Dodaj następujący kod wewnątrz definicji klasy `RegisterController`.</span><span class="sxs-lookup"><span data-stu-id="148fb-167">Add the following code inside the `RegisterController` class definition.</span></span> <span data-ttu-id="148fb-168">Pamiętaj, że w tym kodzie dodajemy tag użytkownika, który jest dołączony do obiektu HttpContext.</span><span class="sxs-lookup"><span data-stu-id="148fb-168">Note that in this code, we add a user tag for the user this is attached to the HttpContext.</span></span> <span data-ttu-id="148fb-169">Użytkownik został uwierzytelniony i dołączony do obiektu HttpContext przez dodany przez nas filtr komunikatów, `AuthenticationTestHandler`.</span><span class="sxs-lookup"><span data-stu-id="148fb-169">The user was authenticated and attached to the HttpContext by the message filter we added, `AuthenticationTestHandler`.</span></span> <span data-ttu-id="148fb-170">Można również dodać opcjonalne sprawdzenia w celu weryfikacji, czy użytkownik ma uprawnienia do rejestrowania żądanych tagów.</span><span class="sxs-lookup"><span data-stu-id="148fb-170">You can also add optional checks to verify that the user has rights to register for the requested tags.</span></span>
   
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
        // This creates or updates a registration (with provided channelURI) at the specified id
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
   
            // add check if user is allowed to add these tags
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
10. <span data-ttu-id="148fb-171">Zapisz zmiany.</span><span class="sxs-lookup"><span data-stu-id="148fb-171">Save your changes.</span></span>

## <a name="sending-notifications-from-the-webapi-backend"></a><span data-ttu-id="148fb-172">Wysyłanie powiadomień z zaplecza interfejsu WebAPI</span><span class="sxs-lookup"><span data-stu-id="148fb-172">Sending Notifications from the WebAPI Backend</span></span>
<span data-ttu-id="148fb-173">W tej sekcji dodasz nowy kontroler, który uwidacznia sposób wysyłania powiadomień przez urządzenia klienckie w oparciu o tag nazwy użytkownika przy użyciu biblioteki zarządzania usługi Azure Notification Hubs w zapleczu interfejsu WebAPI ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="148fb-173">In this section you add a new controller that exposes a way for client devices to send a notification based on the username tag using Azure Notification Hubs Service Management Library in the ASP.NET WebAPI backend.</span></span>

1. <span data-ttu-id="148fb-174">Utwórz kolejny nowy kontroler o nazwie **NotificationsController**.</span><span class="sxs-lookup"><span data-stu-id="148fb-174">Create another new controller named **NotificationsController**.</span></span> <span data-ttu-id="148fb-175">Utwórz go w taki sam sposób, jak kontroler **RegisterController** w poprzedniej sekcji.</span><span class="sxs-lookup"><span data-stu-id="148fb-175">Create it the same way you created the **RegisterController** in the previous section.</span></span>
2. <span data-ttu-id="148fb-176">W pliku NotificationsController.cs dodaj następujące instrukcje `using`:</span><span class="sxs-lookup"><span data-stu-id="148fb-176">In NotificationsController.cs, add the following `using` statements:</span></span>
   
        using AppBackend.Models;
        using System.Threading.Tasks;
        using System.Web;
3. <span data-ttu-id="148fb-177">Dodaj następującą metodę do klasy **NotificationsController**.</span><span class="sxs-lookup"><span data-stu-id="148fb-177">Add the following method to the **NotificationsController** class.</span></span>
   
    <span data-ttu-id="148fb-178">Ten kod wysyła typ powiadomienia na podstawie parametru `pns` usługi powiadomień platformy (PNS, Platform Notification Service).</span><span class="sxs-lookup"><span data-stu-id="148fb-178">This code send a notification type based on the Platform Notification Service (PNS) `pns` parameter.</span></span> <span data-ttu-id="148fb-179">Wartość `to_tag` służy do ustawiania tagu *username* w komunikacie.</span><span class="sxs-lookup"><span data-stu-id="148fb-179">The value of `to_tag` is used to set the *username* tag on the message.</span></span> <span data-ttu-id="148fb-180">Ten tag musi być zgodny z tagiem username aktywnej rejestracji centrum powiadomień.</span><span class="sxs-lookup"><span data-stu-id="148fb-180">This tag must match a username tag of an active notification hub registration.</span></span> <span data-ttu-id="148fb-181">Komunikat powiadomienia jest pobierany z treści żądania POST i formatowany dla docelowej usługi PNS.</span><span class="sxs-lookup"><span data-stu-id="148fb-181">The notification message is pulled from the body of the POST request and formatted for the target PNS.</span></span> 
   
    <span data-ttu-id="148fb-182">W zależności od usługi PNS, używanej do odbierania powiadomień przez obsługiwane urządzenia, różne powiadomienia są obsługiwane przy użyciu różnych formatów.</span><span class="sxs-lookup"><span data-stu-id="148fb-182">Depending on the Platform Notification Service (PNS) that your supported devices use to receive notifications, different notifications are supported using different formats.</span></span> <span data-ttu-id="148fb-183">Na przykład w przypadku urządzeń z systemem Windows możesz użyć [wyskakujących powiadomień za pomocą usługi WNS](https://msdn.microsoft.com/library/windows/apps/br230849.aspx), które nie są bezpośrednio obsługiwane przez inną usługę PNS.</span><span class="sxs-lookup"><span data-stu-id="148fb-183">For example on Windows devices, you could use a [toast notification with WNS](https://msdn.microsoft.com/library/windows/apps/br230849.aspx) that isn't directly supported by another PNS.</span></span> <span data-ttu-id="148fb-184">Dlatego zaplecze musi sformatować powiadomienie jako obsługiwane powiadomienie w przypadku usługi PNS urządzeń, które planujesz obsługiwać.</span><span class="sxs-lookup"><span data-stu-id="148fb-184">So your backend would need to format the notification into a supported notification for the PNS of devices you plan to support.</span></span> <span data-ttu-id="148fb-185">Następnie użyj odpowiedniego interfejsu API wysyłania w klasie [NotificationHubClient](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.notificationhubclient_methods.aspx)</span><span class="sxs-lookup"><span data-stu-id="148fb-185">Then use the appropriate send API on the [NotificationHubClient class](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.notificationhubclient_methods.aspx)</span></span>
   
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
4. <span data-ttu-id="148fb-186">Naciśnij klawisz **F5**, aby uruchomić aplikację i sprawdzić dokładność pracy wykonanej do tej pory.</span><span class="sxs-lookup"><span data-stu-id="148fb-186">Press **F5** to run the application and to ensure the accuracy of your work so far.</span></span> <span data-ttu-id="148fb-187">Aplikacja powinna uruchomić przeglądarkę internetową i wyświetlić stronę główną struktury ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="148fb-187">The app should launch a web browser and display the ASP.NET home page.</span></span> 

## <a name="publish-the-new-webapi-backend"></a><span data-ttu-id="148fb-188">Publikowanie nowego zaplecza interfejsu WebAPI</span><span class="sxs-lookup"><span data-stu-id="148fb-188">Publish the new WebAPI Backend</span></span>
1. <span data-ttu-id="148fb-189">Teraz wdrożymy tę aplikację w witrynie internetowej platformy Azure, aby udostępnić ją wszystkim urządzeniom.</span><span class="sxs-lookup"><span data-stu-id="148fb-189">Now we will deploy this app to an Azure Website in order to make it accessible from all devices.</span></span> <span data-ttu-id="148fb-190">Kliknij prawym przyciskiem myszy projekt **AppBackend** i wybierz polecenie **Publikuj**.</span><span class="sxs-lookup"><span data-stu-id="148fb-190">Right-click on the **AppBackend** project and select **Publish**.</span></span>
2. <span data-ttu-id="148fb-191">Wybierz pozycję **Microsoft Azure App Service** jako docelową lokalizację publikacji, a następnie kliknij przycisk **Publikuj**.</span><span class="sxs-lookup"><span data-stu-id="148fb-191">Select **Microsoft Azure App Service** as your publish target and click **Publish**.</span></span> <span data-ttu-id="148fb-192">Spowoduje to otwarcie okna dialogowego Tworzenie usługi App Service, które ułatwi Ci utworzenie wszystkich zasobów platformy Azure niezbędnych do uruchomienia aplikacji internetowej ASP.NET na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="148fb-192">This opens the Create App Service dialog, which helps you create all the necessary Azure resources to run the ASP.NET web app in Azure.</span></span>

    ![][B15]
3. <span data-ttu-id="148fb-193">W oknie dialogowym **Tworzenie usługi App Service** wybierz swoje konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="148fb-193">In the **Create App Service** dialog, select your Azure account.</span></span> <span data-ttu-id="148fb-194">Kliknij pozycję **Zmień typ** i wybierz pozycję **Aplikacja sieci Web**.</span><span class="sxs-lookup"><span data-stu-id="148fb-194">Click **Change Type** and select **Web App**.</span></span> <span data-ttu-id="148fb-195">Zachowaj wartość w polu **Nazwa aplikacji sieci Web** i wybierz wartości w polach **Subskrypcja**, **Grupa zasobów** i **Plan usługi App Service**.</span><span class="sxs-lookup"><span data-stu-id="148fb-195">Keep the **Web App Name** given and select the **Subscription**, **Resource Group**, and **App Service Plan**.</span></span>  <span data-ttu-id="148fb-196">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="148fb-196">Click **Create**.</span></span>

4. <span data-ttu-id="148fb-197">Zanotuj wartość właściwości **Adres URL witryny** w sekcji **Podsumowanie**.</span><span class="sxs-lookup"><span data-stu-id="148fb-197">Make a note of the **Site URL** property in the **Summary** section.</span></span> <span data-ttu-id="148fb-198">W dalszej części tego samouczka będziemy nazywać ten adres URL *punktem końcowym zaplecza*.</span><span class="sxs-lookup"><span data-stu-id="148fb-198">We will refer to this URL as your *backend endpoint* later in this tutorial.</span></span> <span data-ttu-id="148fb-199">Kliknij przycisk **Opublikuj**.</span><span class="sxs-lookup"><span data-stu-id="148fb-199">Click **Publish**.</span></span>

5. <span data-ttu-id="148fb-200">Po zakończeniu działania kreatora aplikacja internetowa ASP.NET zostanie opublikowana na platformie Azure, a następnie uruchomiona w domyślnej przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="148fb-200">Once the wizard completes, it publishes the ASP.NET web app to Azure, and then launches the app in the default browser.</span></span>  <span data-ttu-id="148fb-201">Twoja aplikacja będzie widoczna w usłudze Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="148fb-201">Your application will be viewable in Azure App Services.</span></span>

<span data-ttu-id="148fb-202">Adres URL używa określonej wcześniej nazwy aplikacji internetowej w formacie http://<nazwa_aplikacji>.azurewebsites.net.</span><span class="sxs-lookup"><span data-stu-id="148fb-202">The URL uses the web app name that you specified earlier, with the format http://<app_name>.azurewebsites.net.</span></span>

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
