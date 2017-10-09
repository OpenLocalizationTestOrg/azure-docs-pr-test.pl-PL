## <a name="create-hello-webapi-project"></a><span data-ttu-id="b6edc-101">Utwórz hello WebAPI projektu</span><span class="sxs-lookup"><span data-stu-id="b6edc-101">Create hello WebAPI Project</span></span>
<span data-ttu-id="b6edc-102">Nowego zaplecza ASP.NET WebAPI zostaną utworzone w kolejnych sekcjach hello i będzie mieć trzy główne cele:</span><span class="sxs-lookup"><span data-stu-id="b6edc-102">A new ASP.NET WebAPI backend will be created in hello sections that follow and it will have three main purposes:</span></span>

1. <span data-ttu-id="b6edc-103">**Uwierzytelnianie klientów**: program obsługi komunikatów zostanie dodany nowszych żądań klientów tooauthenticate i skojarz hello użytkownika z żądaniem hello.</span><span class="sxs-lookup"><span data-stu-id="b6edc-103">**Authenticating Clients**: A message handler will be added later tooauthenticate client requests and associate hello user with hello request.</span></span>
2. <span data-ttu-id="b6edc-104">**Rejestracje powiadomień klienta**: później, należy dodać kontroler toohandle nowe rejestracje klienta tooreceive powiadomień.</span><span class="sxs-lookup"><span data-stu-id="b6edc-104">**Client Notification Registrations**: Later, you will add a controller toohandle new registrations for a client device tooreceive notifications.</span></span> <span data-ttu-id="b6edc-105">Witaj nazwę uwierzytelnionego użytkownika zostanie automatycznie dodane rejestracji toohello jako [tag](https://msdn.microsoft.com/library/azure/dn530749.aspx).</span><span class="sxs-lookup"><span data-stu-id="b6edc-105">hello authenticated user name will automatically be added toohello registration as a [tag](https://msdn.microsoft.com/library/azure/dn530749.aspx).</span></span>
3. <span data-ttu-id="b6edc-106">**Wysyłanie powiadomień tooClients**: później zostaną dodane również tooprovide kontrolera sposób tootrigger użytkownika toodevices bezpiecznego wypychania i klientów skojarzonych z tagiem hello.</span><span class="sxs-lookup"><span data-stu-id="b6edc-106">**Sending Notifications tooClients**: Later, you will also add a controller tooprovide a way for a user tootrigger a secure push toodevices and clients associated with hello tag.</span></span> 

<span data-ttu-id="b6edc-107">Witaj następujące kroki pokazują, jak toocreate hello nowego zaplecza ASP.NET WebAPI:</span><span class="sxs-lookup"><span data-stu-id="b6edc-107">hello following steps show how toocreate hello new ASP.NET WebAPI backend:</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="b6edc-108">Jeśli używasz programu Visual Studio 2015 lub starszym, przed rozpoczęciem tego samouczka, upewnij się, że zainstalowano najnowszą wersję hello hello Menedżera pakietów NuGet.</span><span class="sxs-lookup"><span data-stu-id="b6edc-108">If you are using Visual Studio 2015 or earlier, before starting this tutorial, please ensure that you have installed hello latest version of hello NuGet Package Manager.</span></span> <span data-ttu-id="b6edc-109">toocheck, uruchamiania programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b6edc-109">toocheck, start Visual Studio.</span></span> <span data-ttu-id="b6edc-110">Z hello **narzędzia** menu, kliknij przycisk **rozszerzenia i aktualizacje**.</span><span class="sxs-lookup"><span data-stu-id="b6edc-110">From hello **Tools** menu, click **Extensions and Updates**.</span></span> <span data-ttu-id="b6edc-111">Wyszukaj **Menedżera pakietów NuGet** dla używanej wersji programu Visual Studio i upewnij się, że masz hello najnowszej wersji.</span><span class="sxs-lookup"><span data-stu-id="b6edc-111">Search for **NuGet Package Manager** for your version of Visual Studio, and make sure you have hello latest version.</span></span> <span data-ttu-id="b6edc-112">Jeśli nie, odinstaluj, a następnie ponownie zainstalować hello Menedżera pakietów NuGet.</span><span class="sxs-lookup"><span data-stu-id="b6edc-112">If not, please uninstall, then reinstall hello NuGet Package Manager.</span></span>
> 
> ![][B4]
> 
> [!NOTE]
> <span data-ttu-id="b6edc-113">Upewnij się, że zainstalowano hello Visual Studio [zestawu Azure SDK](https://azure.microsoft.com/downloads/) wdrożenia witryny sieci Web.</span><span class="sxs-lookup"><span data-stu-id="b6edc-113">Make sure you have installed hello Visual Studio [Azure SDK](https://azure.microsoft.com/downloads/) for website deployment.</span></span>
> 
> 

1. <span data-ttu-id="b6edc-114">Uruchom program Visual Studio lub Visual Studio Express.</span><span class="sxs-lookup"><span data-stu-id="b6edc-114">Start Visual Studio or Visual Studio Express.</span></span> <span data-ttu-id="b6edc-115">Kliknij przycisk **Eksploratora serwera** i zaloguj się na tooyour konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="b6edc-115">Click **Server Explorer** and sign in tooyour Azure account.</span></span> <span data-ttu-id="b6edc-116">Visual Studio będzie konieczne jest podpisany w zasobach witryny sieci web hello toocreate Twojego konta.</span><span class="sxs-lookup"><span data-stu-id="b6edc-116">Visual Studio will need you signed in toocreate hello web site resources on your account.</span></span>
2. <span data-ttu-id="b6edc-117">W programie Visual Studio, kliknij przycisk **pliku**, następnie kliknij przycisk **nowy**, następnie **projektu**, rozwiń węzeł **szablony**, **Visual C#**, następnie kliknij przycisk **sieci Web** i **aplikacji sieci Web ASP.NET**, nazwa typu hello **AppBackend**, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="b6edc-117">In Visual Studio, click **File**, then click **New**, then **Project**, expand **Templates**, **Visual C#**, then click **Web** and **ASP.NET Web Application**, type hello name **AppBackend**, and then click **OK**.</span></span> 
   
    ![][B1]
3. <span data-ttu-id="b6edc-118">W hello **nowy projekt ASP.NET** okna dialogowego, kliknij przycisk **interfejsu API sieci Web**, następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="b6edc-118">In hello **New ASP.NET Project** dialog, click **Web API**, then click **OK**.</span></span>
   
    ![][B2]
4. <span data-ttu-id="b6edc-119">W hello **Konfigurowanie aplikacji sieci Web Microsoft Azure** okno dialogowe, wybierz subskrypcję, a **planu usługi aplikacji** zostały już utworzone.</span><span class="sxs-lookup"><span data-stu-id="b6edc-119">In hello **Configure Microsoft Azure Web App** dialog, choose a subscription, and an **App Service plan** you have already created.</span></span> <span data-ttu-id="b6edc-120">Można również wybrać **Utwórz nowy plan usługi aplikacji** i utwórz je z okna dialogowego hello.</span><span class="sxs-lookup"><span data-stu-id="b6edc-120">You can also choose **Create a new app service plan** and create one from hello dialog.</span></span> <span data-ttu-id="b6edc-121">Ten samouczek nie wymaga bazy danych.</span><span class="sxs-lookup"><span data-stu-id="b6edc-121">You do not need a database for this tutorial.</span></span> <span data-ttu-id="b6edc-122">Po wybraniu planu usługi aplikacji, kliknij przycisk **OK** toocreate hello projektu.</span><span class="sxs-lookup"><span data-stu-id="b6edc-122">Once you have selected your app service plan, click **OK** toocreate hello project.</span></span>
   
    ![][B5]

## <a name="authenticating-clients-toohello-webapi-backend"></a><span data-ttu-id="b6edc-123">Uwierzytelnianie klientów toohello WebAPI wewnętrznej bazy danych</span><span class="sxs-lookup"><span data-stu-id="b6edc-123">Authenticating Clients toohello WebAPI Backend</span></span>
<span data-ttu-id="b6edc-124">W tej sekcji utworzysz nową klasę programu obsługi wiadomości o nazwie **AuthenticationTestHandler** dla hello nowego zaplecza.</span><span class="sxs-lookup"><span data-stu-id="b6edc-124">In this section, you will create a new message handler class named **AuthenticationTestHandler** for hello new backend.</span></span> <span data-ttu-id="b6edc-125">Ta klasa pochodzi od [DelegatingHandler](https://msdn.microsoft.com/library/system.net.http.delegatinghandler.aspx) i dodawane jako program obsługi komunikatów, więc może przetwarzać wszystkie żądania kierowane do hello wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="b6edc-125">This class is derived from [DelegatingHandler](https://msdn.microsoft.com/library/system.net.http.delegatinghandler.aspx) and added as a message handler so it can process all requests coming into hello backend.</span></span> 

1. <span data-ttu-id="b6edc-126">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy hello **AppBackend** projektu, kliknij przycisk **Dodaj**, następnie kliknij przycisk **klasy**.</span><span class="sxs-lookup"><span data-stu-id="b6edc-126">In Solution Explorer, right-click hello **AppBackend** project, click **Add**, then click **Class**.</span></span> <span data-ttu-id="b6edc-127">Nazwa nowej klasy hello **AuthenticationTestHandler.cs**i kliknij przycisk **Dodaj** toogenerate hello klasy.</span><span class="sxs-lookup"><span data-stu-id="b6edc-127">Name hello new class **AuthenticationTestHandler.cs**, and click **Add** toogenerate hello class.</span></span> <span data-ttu-id="b6edc-128">Ta klasa będzie używana tooauthenticate użytkowników przy użyciu *uwierzytelnianie podstawowe* dla uproszczenia.</span><span class="sxs-lookup"><span data-stu-id="b6edc-128">This class will be used tooauthenticate users using *Basic Authentication* for simplicity.</span></span> <span data-ttu-id="b6edc-129">Pamiętaj, że Twoja aplikacja może używać dowolnego schematu uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="b6edc-129">Note that your app can use any authentication scheme.</span></span>
2. <span data-ttu-id="b6edc-130">W AuthenticationTestHandler.cs, Dodaj następujące hello `using` instrukcji:</span><span class="sxs-lookup"><span data-stu-id="b6edc-130">In AuthenticationTestHandler.cs, add hello following `using` statements:</span></span>
   
        using System.Net.Http;
        using System.Threading;
        using System.Security.Principal;
        using System.Net;
        using System.Text;
        using System.Threading.Tasks;

3. <span data-ttu-id="b6edc-131">W AuthenticationTestHandler.cs, zastępując hello `AuthenticationTestHandler` klasy definicji z hello następującego kodu.</span><span class="sxs-lookup"><span data-stu-id="b6edc-131">In AuthenticationTestHandler.cs, replacing hello `AuthenticationTestHandler` class definition with hello following code.</span></span> 
   
    <span data-ttu-id="b6edc-132">Ten program obsługi autoryzacji żądania hello gdy wszystkie spełnione są następujące trzy warunki hello:</span><span class="sxs-lookup"><span data-stu-id="b6edc-132">This handler will authorize hello request when hello following three conditions are all true:</span></span>
   
   * <span data-ttu-id="b6edc-133">Żądanie hello uwzględnione *autoryzacji* nagłówka.</span><span class="sxs-lookup"><span data-stu-id="b6edc-133">hello request included an *Authorization* header.</span></span> 
   * <span data-ttu-id="b6edc-134">Żądanie hello używa *podstawowe* uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="b6edc-134">hello request uses *basic* authentication.</span></span> 
   * <span data-ttu-id="b6edc-135">ciąg nazwy użytkownika Hello i haśle hello są hello tych samych parametrach.</span><span class="sxs-lookup"><span data-stu-id="b6edc-135">hello user name string and hello password string are hello same string.</span></span>
     
     <span data-ttu-id="b6edc-136">W przeciwnym razie hello żądanie zostanie odrzucone.</span><span class="sxs-lookup"><span data-stu-id="b6edc-136">Otherwise, hello request will be rejected.</span></span> <span data-ttu-id="b6edc-137">Nie jest to rzeczywiste podejście do uwierzytelniania i autoryzacji.</span><span class="sxs-lookup"><span data-stu-id="b6edc-137">This is not a true authentication and authorization approach.</span></span> <span data-ttu-id="b6edc-138">Jest to bardzo prosty przykład na potrzeby tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="b6edc-138">It is just a very simple example for this tutorial.</span></span>
     
     <span data-ttu-id="b6edc-139">Jeśli komunikat żądania hello uwierzytelnieniu i autoryzacji przez hello `AuthenticationTestHandler`, hello uwierzytelnianie podstawowe użytkownika zostaną dołączone toohello bieżącego żądania na powitania [element HttpContext](https://msdn.microsoft.com/library/system.web.httpcontext.current.aspx).</span><span class="sxs-lookup"><span data-stu-id="b6edc-139">If hello request message is authenticated and authorized by hello `AuthenticationTestHandler`, then hello basic authentication user will be attached toohello current request on hello [HttpContext](https://msdn.microsoft.com/library/system.web.httpcontext.current.aspx).</span></span> <span data-ttu-id="b6edc-140">Informacje o użytkowniku w hello element HttpContext będzie używany przez inny kontroler (RegisterController) nowszego tooadd [tag](https://msdn.microsoft.com/library/azure/dn530749.aspx) żądanie rejestracji toohello powiadomień.</span><span class="sxs-lookup"><span data-stu-id="b6edc-140">User information in hello HttpContext will be used by another controller (RegisterController) later tooadd a [tag](https://msdn.microsoft.com/library/azure/dn530749.aspx) toohello notification registration request.</span></span>
     
       <span data-ttu-id="b6edc-141">public class AuthenticationTestHandler : DelegatingHandler   {       protected override Task<HttpResponseMessage> SendAsync(       HttpRequestMessage request, CancellationToken cancellationToken)       {           var authorizationHeader = request.Headers.GetValues("Authorization").First();</span><span class="sxs-lookup"><span data-stu-id="b6edc-141">public class AuthenticationTestHandler : DelegatingHandler   {       protected override Task<HttpResponseMessage> SendAsync(       HttpRequestMessage request, CancellationToken cancellationToken)       {           var authorizationHeader = request.Headers.GetValues("Authorization").First();</span></span>
     
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
       <span data-ttu-id="b6edc-142">}</span><span class="sxs-lookup"><span data-stu-id="b6edc-142">}</span></span>
     
     > [!NOTE]
     > <span data-ttu-id="b6edc-143">**Uwaga dotycząca zabezpieczeń**: hello `AuthenticationTestHandler` klasa nie zapewnia uwierzytelniania wartość true.</span><span class="sxs-lookup"><span data-stu-id="b6edc-143">**Security Note**: hello `AuthenticationTestHandler` class does not provide true authentication.</span></span> <span data-ttu-id="b6edc-144">Jest używane tylko toomimic uwierzytelniania podstawowego i nie jest bezpieczna.</span><span class="sxs-lookup"><span data-stu-id="b6edc-144">It is used only toomimic basic authentication and is not secure.</span></span> <span data-ttu-id="b6edc-145">W swoich aplikacjach i usługach produkcyjnych musisz zaimplementować mechanizm bezpiecznego uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="b6edc-145">You must implement a secure authentication mechanism in your production applications and services.</span></span>                
     > 
     > 
4. <span data-ttu-id="b6edc-146">Dodaj następującego kodu na końcu hello hello hello `Register` metoda hello **App_Start/WebApiConfig.cs** obsługi wiadomości powitania tooregister klasy:</span><span class="sxs-lookup"><span data-stu-id="b6edc-146">Add hello following code at hello end of hello `Register` method in hello **App_Start/WebApiConfig.cs** class tooregister hello message handler:</span></span>
   
        config.MessageHandlers.Add(new AuthenticationTestHandler());
5. <span data-ttu-id="b6edc-147">Zapisz zmiany.</span><span class="sxs-lookup"><span data-stu-id="b6edc-147">Save your changes.</span></span>

## <a name="registering-for-notifications-using-hello-webapi-backend"></a><span data-ttu-id="b6edc-148">Rejestrowanie na potrzeby powiadomień za pomocą hello WebAPI wewnętrznej bazy danych</span><span class="sxs-lookup"><span data-stu-id="b6edc-148">Registering for Notifications using hello WebAPI Backend</span></span>
<span data-ttu-id="b6edc-149">W tej sekcji dodamy nowe toohandle zaplecza WebAPI toohello kontrolera żądań tooregister użytkownika i urządzenie na potrzeby powiadomień dotyczących usługi notification hubs przy użyciu powitania klienta biblioteki.</span><span class="sxs-lookup"><span data-stu-id="b6edc-149">In this section, we will add a new controller toohello WebAPI backend toohandle requests tooregister a user and device for notifications using hello client library for notification hubs.</span></span> <span data-ttu-id="b6edc-150">Kontroler Hello doda tag użytkownika dla użytkownika hello, który został uwierzytelniony i dołączyć toohello element HttpContext przez hello `AuthenticationTestHandler`.</span><span class="sxs-lookup"><span data-stu-id="b6edc-150">hello controller will add a user tag for hello user that was authenticated and attached toohello HttpContext by hello `AuthenticationTestHandler`.</span></span> <span data-ttu-id="b6edc-151">Hello tag będzie mieć format ciągu hello, `"username:<actual username>"`.</span><span class="sxs-lookup"><span data-stu-id="b6edc-151">hello tag will have hello string format, `"username:<actual username>"`.</span></span>

1. <span data-ttu-id="b6edc-152">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy hello **AppBackend** projektu, a następnie kliknij przycisk **Zarządzaj pakietami NuGet**.</span><span class="sxs-lookup"><span data-stu-id="b6edc-152">In Solution Explorer, right-click hello **AppBackend** project and then click **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="b6edc-153">Na powitania po lewej stronie, kliknij przycisk **Online**i wyszukaj **Microsoft.Azure.NotificationHubs** w hello **wyszukiwania** pole.</span><span class="sxs-lookup"><span data-stu-id="b6edc-153">On hello left-hand side, click **Online**, and search for **Microsoft.Azure.NotificationHubs** in hello **Search** box.</span></span>
3. <span data-ttu-id="b6edc-154">Kliknij na liście wyników hello **centra powiadomień Microsoft Azure**, a następnie kliknij przycisk **zainstalować**.</span><span class="sxs-lookup"><span data-stu-id="b6edc-154">In hello results list, click **Microsoft Azure Notification Hubs**, and then click **Install**.</span></span> <span data-ttu-id="b6edc-155">Ukończenie instalacji hello, a następnie zamknij okno Menedżera pakietów NuGet hello.</span><span class="sxs-lookup"><span data-stu-id="b6edc-155">Complete hello installation, then close hello NuGet package manager window.</span></span>
   
    <span data-ttu-id="b6edc-156">Spowoduje to dodanie toohello odwołanie do zestawu SDK usługi Azure Notification Hubs za pomocą hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">pakietu Microsoft.Azure.Notification Hubs NuGet</a>.</span><span class="sxs-lookup"><span data-stu-id="b6edc-156">This adds a reference toohello Azure Notification Hubs SDK using hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet package</a>.</span></span>
4. <span data-ttu-id="b6edc-157">Teraz utworzymy nowy plik klasy reprezentujące hello połączenia z powiadomieniami toosend używane Centrum powiadomień.</span><span class="sxs-lookup"><span data-stu-id="b6edc-157">We will now create a new class file that represents hello connection with notification hub used toosend notifications.</span></span> <span data-ttu-id="b6edc-158">W Eksploratorze rozwiązań hello, kliknij prawym przyciskiem myszy hello **modele** folderu, kliknij przycisk **Dodaj**, następnie kliknij przycisk **klasy**.</span><span class="sxs-lookup"><span data-stu-id="b6edc-158">In hello Solution Explorer, right-click hello **Models** folder, click **Add**, then click **Class**.</span></span> <span data-ttu-id="b6edc-159">Nazwa nowej klasy hello **Notifications.cs**, następnie kliknij przycisk **Dodaj** toogenerate hello klasy.</span><span class="sxs-lookup"><span data-stu-id="b6edc-159">Name hello new class **Notifications.cs**, then click **Add** toogenerate hello class.</span></span> 
   
    ![][B6]
5. <span data-ttu-id="b6edc-160">W Notifications.cs, Dodaj następujące hello `using` instrukcji u góry pliku hello hello:</span><span class="sxs-lookup"><span data-stu-id="b6edc-160">In Notifications.cs, add hello following `using` statement at hello top of hello file:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
6. <span data-ttu-id="b6edc-161">Zastąp hello `Notifications` klasy definicji hello następujący i wprowadzić symbole zastępcze hello dwa tooreplace się przy użyciu parametrów połączenia hello (z pełnym dostępem) dla Centrum powiadomień, a hello nazwy Centrum (dostępne pod adresem [klasycznego portalu Azure ](http://manage.windowsazure.com)):</span><span class="sxs-lookup"><span data-stu-id="b6edc-161">Replace hello `Notifications` class definition with hello following and make sure tooreplace hello two placeholders with hello connection string (with full access) for your notification hub, and hello hub name (available at [Azure Classic Portal](http://manage.windowsazure.com)):</span></span>
   
        public class Notifications
        {
            public static Notifications Instance = new Notifications();
   
            public NotificationHubClient Hub { get; set; }
   
            private Notifications() {
                Hub = NotificationHubClient.CreateClientFromConnectionString("<your hub's DefaultFullSharedAccessSignature>", 
                                                                             "<hub name>");
            }
        }
7. <span data-ttu-id="b6edc-162">Następnie utworzymy nowy kontroler o nazwie **RegisterController**.</span><span class="sxs-lookup"><span data-stu-id="b6edc-162">Next we will create a new controller named **RegisterController**.</span></span> <span data-ttu-id="b6edc-163">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy hello **kontrolerów** folderu, następnie kliknij przycisk **Dodaj**, następnie kliknij przycisk **kontrolera**.</span><span class="sxs-lookup"><span data-stu-id="b6edc-163">In Solution Explorer, right-click hello **Controllers** folder, then click **Add**, then click **Controller**.</span></span> <span data-ttu-id="b6edc-164">Kliknij przycisk hello **kontroler 2 interfejsu API sieci Web — pusty** elementu, a następnie kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="b6edc-164">Click hello **Web API 2 Controller -- Empty** item, and then click **Add**.</span></span> <span data-ttu-id="b6edc-165">Nazwa nowej klasy hello **RegisterController**, a następnie kliknij przycisk **Dodaj** ponownie toogenerate hello kontrolera.</span><span class="sxs-lookup"><span data-stu-id="b6edc-165">Name hello new class **RegisterController**, and then click **Add** again toogenerate hello controller.</span></span>
   
    ![][B7]
   
    ![][B8]
8. <span data-ttu-id="b6edc-166">W RegisterController.cs, Dodaj następujące hello `using` instrukcji:</span><span class="sxs-lookup"><span data-stu-id="b6edc-166">In RegisterController.cs, add hello following `using` statements:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
        using Microsoft.Azure.NotificationHubs.Messaging;
        using AppBackend.Models;
        using System.Threading.Tasks;
        using System.Web;
9. <span data-ttu-id="b6edc-167">Dodaj następujące kodu wewnątrz hello hello `RegisterController` definicji klasy.</span><span class="sxs-lookup"><span data-stu-id="b6edc-167">Add hello following code inside hello `RegisterController` class definition.</span></span> <span data-ttu-id="b6edc-168">Należy pamiętać, że w tym kodzie, możemy dodać tag użytkownika dla użytkownika hello, który jest dołączony toohello element HttpContext.</span><span class="sxs-lookup"><span data-stu-id="b6edc-168">Note that in this code, we add a user tag for hello user this is attached toohello HttpContext.</span></span> <span data-ttu-id="b6edc-169">Hello użytkownik został uwierzytelniony i dołączony toohello element HttpContext przez filtr wiadomość hello dodaliśmy, `AuthenticationTestHandler`.</span><span class="sxs-lookup"><span data-stu-id="b6edc-169">hello user was authenticated and attached toohello HttpContext by hello message filter we added, `AuthenticationTestHandler`.</span></span> <span data-ttu-id="b6edc-170">Można również dodać tooverify kontroli opcjonalne, które hello użytkownika ma uprawnienia tooregister dla hello wymagane tagi.</span><span class="sxs-lookup"><span data-stu-id="b6edc-170">You can also add optional checks tooverify that hello user has rights tooregister for hello requested tags.</span></span>
   
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
10. <span data-ttu-id="b6edc-171">Zapisz zmiany.</span><span class="sxs-lookup"><span data-stu-id="b6edc-171">Save your changes.</span></span>

## <a name="sending-notifications-from-hello-webapi-backend"></a><span data-ttu-id="b6edc-172">Wysyłanie powiadomień z zaplecza WebAPI hello</span><span class="sxs-lookup"><span data-stu-id="b6edc-172">Sending Notifications from hello WebAPI Backend</span></span>
<span data-ttu-id="b6edc-173">W tej sekcji możesz dodać nowego kontrolera, który opisuje sposób dla klienta urządzenia toosend powiadomienie oparte na powitania username tag przy użyciu Biblioteka zarządzania usługi centra powiadomień Azure w hello zaplecza ASP.NET WebAPI.</span><span class="sxs-lookup"><span data-stu-id="b6edc-173">In this section you add a new controller that exposes a way for client devices toosend a notification based on hello username tag using Azure Notification Hubs Service Management Library in hello ASP.NET WebAPI backend.</span></span>

1. <span data-ttu-id="b6edc-174">Utwórz kolejny nowy kontroler o nazwie **NotificationsController**.</span><span class="sxs-lookup"><span data-stu-id="b6edc-174">Create another new controller named **NotificationsController**.</span></span> <span data-ttu-id="b6edc-175">Utwórz go hello taki sam sposób utworzyć hello **RegisterController** w poprzedniej sekcji hello.</span><span class="sxs-lookup"><span data-stu-id="b6edc-175">Create it hello same way you created hello **RegisterController** in hello previous section.</span></span>
2. <span data-ttu-id="b6edc-176">W NotificationsController.cs, Dodaj następujące hello `using` instrukcji:</span><span class="sxs-lookup"><span data-stu-id="b6edc-176">In NotificationsController.cs, add hello following `using` statements:</span></span>
   
        using AppBackend.Models;
        using System.Threading.Tasks;
        using System.Web;
3. <span data-ttu-id="b6edc-177">Dodaj następujące metody toohello hello **NotificationsController** klasy.</span><span class="sxs-lookup"><span data-stu-id="b6edc-177">Add hello following method toohello **NotificationsController** class.</span></span>
   
    <span data-ttu-id="b6edc-178">Ten kod wysyłania typ powiadomienia, oparte na powitania usługi powiadomień platformy (PNS) `pns` parametru.</span><span class="sxs-lookup"><span data-stu-id="b6edc-178">This code send a notification type based on hello Platform Notification Service (PNS) `pns` parameter.</span></span> <span data-ttu-id="b6edc-179">Witaj wartość `to_tag` jest używane tooset hello *username* tagu na wiadomość powitania.</span><span class="sxs-lookup"><span data-stu-id="b6edc-179">hello value of `to_tag` is used tooset hello *username* tag on hello message.</span></span> <span data-ttu-id="b6edc-180">Ten tag musi być zgodny z tagiem username aktywnej rejestracji centrum powiadomień.</span><span class="sxs-lookup"><span data-stu-id="b6edc-180">This tag must match a username tag of an active notification hub registration.</span></span> <span data-ttu-id="b6edc-181">komunikat z powiadomieniem Hello jest pobierane z hello treści żądania POST hello i sformatowany dla elementu docelowego hello systemu powiadomień platformy.</span><span class="sxs-lookup"><span data-stu-id="b6edc-181">hello notification message is pulled from hello body of hello POST request and formatted for hello target PNS.</span></span> 
   
    <span data-ttu-id="b6edc-182">W zależności od hello czy obsługiwanych urządzeń, użyj tooreceive powiadomień platformy powiadomień usługi (PNS) różnych powiadomienia są obsługiwane przy użyciu różnych formatach.</span><span class="sxs-lookup"><span data-stu-id="b6edc-182">Depending on hello Platform Notification Service (PNS) that your supported devices use tooreceive notifications, different notifications are supported using different formats.</span></span> <span data-ttu-id="b6edc-183">Na przykład w przypadku urządzeń z systemem Windows możesz użyć [wyskakujących powiadomień za pomocą usługi WNS](https://msdn.microsoft.com/library/windows/apps/br230849.aspx), które nie są bezpośrednio obsługiwane przez inną usługę PNS.</span><span class="sxs-lookup"><span data-stu-id="b6edc-183">For example on Windows devices, you could use a [toast notification with WNS](https://msdn.microsoft.com/library/windows/apps/br230849.aspx) that isn't directly supported by another PNS.</span></span> <span data-ttu-id="b6edc-184">Dzięki zaplecza musi tooformat hello powiadomień do obsługiwanych powiadomień dla hello systemu powiadomień platformy urządzeń, który planujesz toosupport.</span><span class="sxs-lookup"><span data-stu-id="b6edc-184">So your backend would need tooformat hello notification into a supported notification for hello PNS of devices you plan toosupport.</span></span> <span data-ttu-id="b6edc-185">Następnie użyj interfejsu API wysyłania odpowiednie hello na powitania [NotificationHubClient — klasa](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.notificationhubclient_methods.aspx)</span><span class="sxs-lookup"><span data-stu-id="b6edc-185">Then use hello appropriate send API on hello [NotificationHubClient class](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.notificationhubclient_methods.aspx)</span></span>
   
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
4. <span data-ttu-id="b6edc-186">Naciśnij klawisz **F5** toorun hello aplikacji i tooensure hello dokładność pracy wykonanej do tej pory.</span><span class="sxs-lookup"><span data-stu-id="b6edc-186">Press **F5** toorun hello application and tooensure hello accuracy of your work so far.</span></span> <span data-ttu-id="b6edc-187">Aplikacja Hello powinno uruchomić przeglądarki sieci web i wyświetlenie strony głównej hello ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="b6edc-187">hello app should launch a web browser and display hello ASP.NET home page.</span></span> 

## <a name="publish-hello-new-webapi-backend"></a><span data-ttu-id="b6edc-188">Publikowanie hello nowego zaplecza WebAPI</span><span class="sxs-lookup"><span data-stu-id="b6edc-188">Publish hello new WebAPI Backend</span></span>
1. <span data-ttu-id="b6edc-189">Teraz wdrożymy ten tooan aplikacji witryny sieci Web Azure w kolejności toomake go ze wszystkich urządzeń.</span><span class="sxs-lookup"><span data-stu-id="b6edc-189">Now we will deploy this app tooan Azure Website in order toomake it accessible from all devices.</span></span> <span data-ttu-id="b6edc-190">Kliknij prawym przyciskiem myszy na powitania **AppBackend** projekt i wybierz **publikowania**.</span><span class="sxs-lookup"><span data-stu-id="b6edc-190">Right-click on hello **AppBackend** project and select **Publish**.</span></span>
2. <span data-ttu-id="b6edc-191">Wybierz pozycję **Microsoft Azure App Service** jako docelową lokalizację publikacji, a następnie kliknij przycisk **Publikuj**.</span><span class="sxs-lookup"><span data-stu-id="b6edc-191">Select **Microsoft Azure App Service** as your publish target and click **Publish**.</span></span> <span data-ttu-id="b6edc-192">Zostanie otwarte okno dialogowe Tworzenie usługi App Service hello, które pomaga w utworzeniu wszystkich aplikacji sieci web serwera hello niezbędnych zasobów Azure toorun hello ASP.NET na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="b6edc-192">This opens hello Create App Service dialog, which helps you create all hello necessary Azure resources toorun hello ASP.NET web app in Azure.</span></span>

    ![][B15]
3. <span data-ttu-id="b6edc-193">W hello **Tworzenie usługi App Service** okno dialogowe, wybierz konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="b6edc-193">In hello **Create App Service** dialog, select your Azure account.</span></span> <span data-ttu-id="b6edc-194">Kliknij pozycję **Zmień typ** i wybierz pozycję **Aplikacja sieci Web**.</span><span class="sxs-lookup"><span data-stu-id="b6edc-194">Click **Change Type** and select **Web App**.</span></span> <span data-ttu-id="b6edc-195">Zachowaj hello **Nazwa aplikacji sieci Web** hello danego i wybierz pozycję **subskrypcji**, **grupy zasobów**, i **planu usługi App Service**.</span><span class="sxs-lookup"><span data-stu-id="b6edc-195">Keep hello **Web App Name** given and select hello **Subscription**, **Resource Group**, and **App Service Plan**.</span></span>  <span data-ttu-id="b6edc-196">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="b6edc-196">Click **Create**.</span></span>

4. <span data-ttu-id="b6edc-197">Zanotuj hello **adres URL witryny** właściwości w hello **Podsumowanie** sekcji.</span><span class="sxs-lookup"><span data-stu-id="b6edc-197">Make a note of hello **Site URL** property in hello **Summary** section.</span></span> <span data-ttu-id="b6edc-198">Odnoszą się adres URL toothis Twojego *wewnętrznej bazy danych punktu końcowego* dalszej części tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="b6edc-198">We will refer toothis URL as your *backend endpoint* later in this tutorial.</span></span> <span data-ttu-id="b6edc-199">Kliknij przycisk **Opublikuj**.</span><span class="sxs-lookup"><span data-stu-id="b6edc-199">Click **Publish**.</span></span>

5. <span data-ttu-id="b6edc-200">Po zakończeniu pracy Kreatora hello, powoduje ona publikowanie tooAzure aplikacji sieci web ASP.NET hello, a następnie spowoduje uruchomienie hello aplikacji hello domyślnej przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="b6edc-200">Once hello wizard completes, it publishes hello ASP.NET web app tooAzure, and then launches hello app in hello default browser.</span></span>  <span data-ttu-id="b6edc-201">Twoja aplikacja będzie widoczna w usłudze Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="b6edc-201">Your application will be viewable in Azure App Services.</span></span>

<span data-ttu-id="b6edc-202">adres URL Hello używa hello Nazwa aplikacji sieci web, określony wcześniej, z hello format http://<app_name>.azurewebsites.net.</span><span class="sxs-lookup"><span data-stu-id="b6edc-202">hello URL uses hello web app name that you specified earlier, with hello format http://<app_name>.azurewebsites.net.</span></span>

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
