1. <span data-ttu-id="7cb32-101">Zaloguj się na toohello [portalu Azure][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="7cb32-101">Log on toohello [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="7cb32-102">W okienku nawigacji po lewej stronie powitania hello portalu kliknij **nowy**, następnie kliknij przycisk **integracji przedsiębiorstwa**, a następnie kliknij przycisk **przekazywania**.</span><span class="sxs-lookup"><span data-stu-id="7cb32-102">In hello left navigation pane of hello portal, click **New**, then click **Enterprise Integration**, and then click **Relay**.</span></span>
3. <span data-ttu-id="7cb32-103">W hello **tworzenie przestrzeni nazw** okna dialogowego, wprowadź nazwę przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="7cb32-103">In hello **Create namespace** dialog, enter a namespace name.</span></span> <span data-ttu-id="7cb32-104">system powitania od razu sprawdza toosee, jeśli nazwa hello jest dostępna.</span><span class="sxs-lookup"><span data-stu-id="7cb32-104">hello system immediately checks toosee if hello name is available.</span></span>
4. <span data-ttu-id="7cb32-105">W hello **subskrypcji** pola, wybierz subskrypcję platformy Azure, w których toocreate hello nazw.</span><span class="sxs-lookup"><span data-stu-id="7cb32-105">In hello **Subscription** field, choose an Azure subscription in which toocreate hello namespace.</span></span>
5. <span data-ttu-id="7cb32-106">W hello  **[grupy zasobów](../articles/azure-resource-manager/resource-group-portal.md)**  wybierz istniejącą grupę zasobów, w których hello przestrzeni nazw zostanie na żywo lub Utwórz nową.</span><span class="sxs-lookup"><span data-stu-id="7cb32-106">In hello **[Resource group](../articles/azure-resource-manager/resource-group-portal.md)** field, choose an existing resource group in which hello namespace will live, or create a new one.</span></span>      
6. <span data-ttu-id="7cb32-107">W **lokalizacji**, wybierz hello kraj lub region, w którym ma być hostowana przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="7cb32-107">In **Location**, choose hello country or region in which your namespace should be hosted.</span></span>
   
    ![Create namespace][create-namespace]
7. <span data-ttu-id="7cb32-109">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="7cb32-109">Click **Create**.</span></span> <span data-ttu-id="7cb32-110">teraz Hello system utworzy przestrzeń nazw i włączy ją.</span><span class="sxs-lookup"><span data-stu-id="7cb32-110">hello system now creates your namespace and enables it.</span></span> <span data-ttu-id="7cb32-111">Po kilku minutach hello systemu inicjowania obsługi administracyjnej zasobów dla Twojego konta.</span><span class="sxs-lookup"><span data-stu-id="7cb32-111">After a few minutes, hello system provisions resources for your account.</span></span>

### <a name="obtain-hello-management-credentials"></a><span data-ttu-id="7cb32-112">Uzyskiwanie poświadczeń zarządzania hello</span><span class="sxs-lookup"><span data-stu-id="7cb32-112">Obtain hello management credentials</span></span>
1. <span data-ttu-id="7cb32-113">Kliknij hello nowo utworzona nazwa przestrzeni nazw na liście hello przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="7cb32-113">In hello list of namespaces, click hello newly created namespace name.</span></span>
2. <span data-ttu-id="7cb32-114">W bloku przestrzeni nazw powitania kliknij **zasady dostępu współużytkowanego**.</span><span class="sxs-lookup"><span data-stu-id="7cb32-114">In hello namespace blade, click **Shared access policies**.</span></span>
3. <span data-ttu-id="7cb32-115">W hello **zasady dostępu współużytkowanego** bloku, kliknij przycisk **RootManageSharedAccessKey**.</span><span class="sxs-lookup"><span data-stu-id="7cb32-115">In hello **Shared access policies** blade, click **RootManageSharedAccessKey**.</span></span>
   
    ![connection-info][connection-info]
4. <span data-ttu-id="7cb32-117">W hello **zasad: RootManageSharedAccessKey** bloku, kliknij przycisk Kopiuj hello obok zbyt**połączenia ciąg — podstawowy klucz**, toocopy hello połączenia ciąg tooyour Schowka do późniejszego użycia.</span><span class="sxs-lookup"><span data-stu-id="7cb32-117">In hello **Policy: RootManageSharedAccessKey** blade, click hello copy button next too**Connection string–primary key**, toocopy hello connection string tooyour clipboard for later use.</span></span> <span data-ttu-id="7cb32-118">Wklej tę wartość do Notatnika lub innej tymczasowej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="7cb32-118">Paste this value into Notepad or some other temporary location.</span></span>
   
    ![connection-string][connection-string]

5. <span data-ttu-id="7cb32-120">Hello powtórzeń poprzedniego kroku, kopiowanie i wklejanie wartość hello **klucza podstawowego** tooa lokalizacji tymczasowej na potrzeby późniejszego użycia.</span><span class="sxs-lookup"><span data-stu-id="7cb32-120">Repeat hello previous step, copying and pasting hello value of **Primary key** tooa temporary location for later use.</span></span>  

<!--Image references-->

[create-namespace]: ./media/relay-create-namespace-portal/create-namespace.png
[connection-info]: ./media/relay-create-namespace-portal/connection-info.png
[connection-string]: ./media/relay-create-namespace-portal/connection-string.png
[Azure portal]: https://portal.azure.com
