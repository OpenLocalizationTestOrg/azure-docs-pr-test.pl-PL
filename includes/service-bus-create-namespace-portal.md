<span data-ttu-id="910f3-101">kolejkuje toobegin przy użyciu usługi Service Bus na platformie Azure, musisz najpierw utworzyć przestrzeń nazw o nazwie, która jest unikatowa w obrębie platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="910f3-101">toobegin using Service Bus queues in Azure, you must first create a namespace with a name that is unique across Azure.</span></span> <span data-ttu-id="910f3-102">Przestrzeń nazw zapewnia kontener określania zakresu na potrzeby adresowania zasobów usługi Service Bus w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="910f3-102">A namespace provides a scoping container for addressing Service Bus resources within your application.</span></span>

<span data-ttu-id="910f3-103">toocreate przestrzeni nazw:</span><span class="sxs-lookup"><span data-stu-id="910f3-103">toocreate a namespace:</span></span>

1. <span data-ttu-id="910f3-104">Zaloguj się na toohello [portalu Azure][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="910f3-104">Log on toohello [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="910f3-105">W okienku nawigacji po lewej stronie powitania hello portalu kliknij **nowy**, następnie kliknij przycisk **integracji przedsiębiorstwa**, a następnie kliknij przycisk **usługi Service Bus**.</span><span class="sxs-lookup"><span data-stu-id="910f3-105">In hello left navigation pane of hello portal, click **New**, then click **Enterprise Integration**, and then click **Service Bus**.</span></span>
3. <span data-ttu-id="910f3-106">W hello **tworzenie przestrzeni nazw** okna dialogowego, wprowadź nazwę przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="910f3-106">In hello **Create namespace** dialog, enter a namespace name.</span></span> <span data-ttu-id="910f3-107">system powitania od razu sprawdza toosee, jeśli nazwa hello jest dostępna.</span><span class="sxs-lookup"><span data-stu-id="910f3-107">hello system immediately checks toosee if hello name is available.</span></span>
4. <span data-ttu-id="910f3-108">Po co czy hello przestrzeni nazw jest dostępna, należy wybrać hello cenowym (podstawowa, standardowa lub Premium).</span><span class="sxs-lookup"><span data-stu-id="910f3-108">After making sure hello namespace name is available, choose hello pricing tier (Basic, Standard, or Premium).</span></span>
5. <span data-ttu-id="910f3-109">W hello **subskrypcji** pola, wybierz subskrypcję platformy Azure, w których toocreate hello nazw.</span><span class="sxs-lookup"><span data-stu-id="910f3-109">In hello **Subscription** field, choose an Azure subscription in which toocreate hello namespace.</span></span>
6. <span data-ttu-id="910f3-110">W hello **grupy zasobów** wybierz istniejącą grupę zasobów, w których hello przestrzeni nazw zostanie na żywo lub Utwórz nową.</span><span class="sxs-lookup"><span data-stu-id="910f3-110">In hello **Resource group** field, choose an existing resource group in which hello namespace will live, or create a new one.</span></span>      
7. <span data-ttu-id="910f3-111">W **lokalizacji**, wybierz hello kraj lub region, w którym ma być hostowana przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="910f3-111">In **Location**, choose hello country or region in which your namespace should be hosted.</span></span>
   
    ![Create namespace][create-namespace]
8. <span data-ttu-id="910f3-113">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="910f3-113">Click **Create**.</span></span> <span data-ttu-id="910f3-114">teraz Hello system utworzy przestrzeń nazw i włączy ją.</span><span class="sxs-lookup"><span data-stu-id="910f3-114">hello system now creates your namespace and enables it.</span></span> <span data-ttu-id="910f3-115">Toowait może mieć kilka minut hello systemu inicjowania obsługi administracyjnej zasobów dla Twojego konta.</span><span class="sxs-lookup"><span data-stu-id="910f3-115">You might have toowait several minutes as hello system provisions resources for your account.</span></span>

### <a name="obtain-hello-management-credentials"></a><span data-ttu-id="910f3-116">Uzyskiwanie poświadczeń zarządzania hello</span><span class="sxs-lookup"><span data-stu-id="910f3-116">Obtain hello management credentials</span></span>

1. <span data-ttu-id="910f3-117">Kliknij hello nowo utworzona nazwa przestrzeni nazw na liście hello przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="910f3-117">In hello list of namespaces, click hello newly created namespace name.</span></span>
2. <span data-ttu-id="910f3-118">W bloku przestrzeni nazw powitania kliknij **zasady dostępu współużytkowanego**.</span><span class="sxs-lookup"><span data-stu-id="910f3-118">In hello namespace blade, click **Shared access policies**.</span></span>
3. <span data-ttu-id="910f3-119">W hello **zasady dostępu współużytkowanego** bloku, kliknij przycisk **RootManageSharedAccessKey**.</span><span class="sxs-lookup"><span data-stu-id="910f3-119">In hello **Shared access policies** blade, click **RootManageSharedAccessKey**.</span></span>
   
    ![connection-info][connection-info]
4. <span data-ttu-id="910f3-121">W hello **zasad: RootManageSharedAccessKey** bloku, kliknij przycisk Kopiuj hello obok zbyt**połączenia ciąg — podstawowy klucz**, toocopy hello połączenia ciąg tooyour Schowka do późniejszego użycia.</span><span class="sxs-lookup"><span data-stu-id="910f3-121">In hello **Policy: RootManageSharedAccessKey** blade, click hello copy button next too**Connection string–primary key**, toocopy hello connection string tooyour clipboard for later use.</span></span> <span data-ttu-id="910f3-122">Wklej tę wartość do Notatnika lub innej tymczasowej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="910f3-122">Paste this value into Notepad or some other temporary location.</span></span>
   
    ![connection-string][connection-string]

5. <span data-ttu-id="910f3-124">Hello powtórzeń poprzedniego kroku, kopiowanie i wklejanie wartość hello **klucza podstawowego** tooa lokalizacji tymczasowej na potrzeby późniejszego użycia.</span><span class="sxs-lookup"><span data-stu-id="910f3-124">Repeat hello previous step, copying and pasting hello value of **Primary key** tooa temporary location for later use.</span></span>

<!--Image references-->

[create-namespace]: ./media/service-bus-create-namespace-portal/create-namespace.png
[connection-info]: ./media/service-bus-create-namespace-portal/connection-info.png
[connection-string]: ./media/service-bus-create-namespace-portal/connection-string.png
[Azure portal]: https://portal.azure.com
