
1. <span data-ttu-id="006d7-101">Kliknij przycisk hello **usługi aplikacji** przycisk Wybierz użytkownika zaplecza aplikacji mobilnej, wybierz **szybkiego startu**, a następnie wybierz platformę klienta (systemy iOS, Android, Xamarin, Cordova).</span><span class="sxs-lookup"><span data-stu-id="006d7-101">Click hello **App Services** button, select your Mobile Apps back end, select **Quickstart**, and then select your client platform (iOS, Android, Xamarin, Cordova).</span></span>

    ![Witryna Azure Portal z wyróżnioną pozycją Mobile Apps — szybki start][quickstart]

2. <span data-ttu-id="006d7-103">Jeśli nie skonfigurowano połączenia z bazą danych, utwórz go, wykonując następujące hello:</span><span class="sxs-lookup"><span data-stu-id="006d7-103">If a database connection is not configured, create one by doing hello following:</span></span>

    ![Portal Azure Mobile Apps Connect toodatabase][connect]

    <span data-ttu-id="006d7-105">a.</span><span class="sxs-lookup"><span data-stu-id="006d7-105">a.</span></span> <span data-ttu-id="006d7-106">Utwórz nową bazę danych SQL i serwer.</span><span class="sxs-lookup"><span data-stu-id="006d7-106">Create a new SQL database and server.</span></span>

    ![Witryna Azure Portal z opcją tworzenia nowej bazy danych i serwera funkcji Mobile Apps][server]

    <span data-ttu-id="006d7-108">b.</span><span class="sxs-lookup"><span data-stu-id="006d7-108">b.</span></span> <span data-ttu-id="006d7-109">Poczekaj, aż hello połączenie danych został utworzony pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="006d7-109">Wait until hello data connection is successfully created.</span></span>

    ![Powiadomienie witryny Azure Portal o pomyślnym utworzeniu połączenia danych][notification]

    <span data-ttu-id="006d7-111">c.</span><span class="sxs-lookup"><span data-stu-id="006d7-111">c.</span></span> <span data-ttu-id="006d7-112">Połączenie danych musi się powieść.</span><span class="sxs-lookup"><span data-stu-id="006d7-112">Data connection must be successful.</span></span>

    ![Powiadomienie witryny Azure Portal „Masz już połączenie danych”][already-connection]

3. <span data-ttu-id="006d7-114">W obszarze **2. Utwórz tabelę interfejsu API** wybierz dla języka Node.js opcję **Język zaplecza**.</span><span class="sxs-lookup"><span data-stu-id="006d7-114">Under **2. Create a table API**, select Node.js for **Backend language**.</span></span> 
 
4. <span data-ttu-id="006d7-115">Zaakceptuj potwierdzenie hello, a następnie wybierz **Utwórz tabelę TodoItem**.</span><span class="sxs-lookup"><span data-stu-id="006d7-115">Accept hello acknowledgment, and then select **Create TodoItem table**.</span></span>  
    <span data-ttu-id="006d7-116">Ta akcja spowoduje utworzenie nowej tabeli elementów do wykonania w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="006d7-116">This action creates a new to-do item table in your database.</span></span> 

    >[!IMPORTANT]
    > <span data-ttu-id="006d7-117">Przełączenie istniejącej tooNode.js zaplecza spowoduje zastąpienie całej zawartości.</span><span class="sxs-lookup"><span data-stu-id="006d7-117">Switching an existing back end tooNode.js overwrites all contents.</span></span> <span data-ttu-id="006d7-118">Zamiast tego zobacz zaplecze .NET toocreate [działać z serwerem hello zaplecza .NET SDK dla aplikacji mobilnych][instructions].</span><span class="sxs-lookup"><span data-stu-id="006d7-118">toocreate a .NET back end instead, see [Work with hello .NET back-end server SDK for Mobile Apps][instructions].</span></span>

<!-- Images. -->
[quickstart]: ./media/app-service-mobile-configure-new-backend/quickstart.png
[connect]: ./media/app-service-mobile-configure-new-backend/connect-to-bd.png
[notification]: ./media/app-service-mobile-configure-new-backend/notification-data-connection-create.png
[server]: ./media/app-service-mobile-configure-new-backend/create-new-server.png
[already-connection]: ./media/app-service-mobile-configure-new-backend/already-connection.png

<!-- URLs -->
[instructions]: ../articles/app-service-mobile/app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#create-app
