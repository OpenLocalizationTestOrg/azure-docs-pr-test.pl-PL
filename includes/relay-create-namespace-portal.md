1. <span data-ttu-id="68f2b-101">Zaloguj się w witrynie [Azure Portal][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="68f2b-101">Log on to the [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="68f2b-102">W lewym okienku nawigacji portalu kliknij kolejno pozycje **Nowy**, **Integracja w przedsiębiorstwie** i **Relay**.</span><span class="sxs-lookup"><span data-stu-id="68f2b-102">In the left navigation pane of the portal, click **New**, then click **Enterprise Integration**, and then click **Relay**.</span></span>
3. <span data-ttu-id="68f2b-103">W oknie dialogowym **Tworzenie przestrzeni nazw** wprowadź nazwę przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="68f2b-103">In the **Create namespace** dialog, enter a namespace name.</span></span> <span data-ttu-id="68f2b-104">System od razu sprawdza, czy nazwa jest dostępna.</span><span class="sxs-lookup"><span data-stu-id="68f2b-104">The system immediately checks to see if the name is available.</span></span>
4. <span data-ttu-id="68f2b-105">W polu **Subskrypcja** wybierz subskrypcję platformy Azure, w której ma zostać utworzona przestrzeń nazw.</span><span class="sxs-lookup"><span data-stu-id="68f2b-105">In the **Subscription** field, choose an Azure subscription in which to create the namespace.</span></span>
5. <span data-ttu-id="68f2b-106">W polu **[Grupa zasobów](../articles/azure-resource-manager/resource-group-portal.md)** wybierz istniejącą grupę zasobów, w której znajdzie się przestrzeń nazw, lub utwórz nową.</span><span class="sxs-lookup"><span data-stu-id="68f2b-106">In the **[Resource group](../articles/azure-resource-manager/resource-group-portal.md)** field, choose an existing resource group in which the namespace will live, or create a new one.</span></span>      
6. <span data-ttu-id="68f2b-107">W polu **Lokalizacja** wybierz kraj lub region, w którym powinna być hostowana przestrzeń nazw.</span><span class="sxs-lookup"><span data-stu-id="68f2b-107">In **Location**, choose the country or region in which your namespace should be hosted.</span></span>
   
    ![Create namespace][create-namespace]
7. <span data-ttu-id="68f2b-109">Kliknij pozycję **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="68f2b-109">Click **Create**.</span></span> <span data-ttu-id="68f2b-110">W systemie zostanie utworzona i włączona przestrzeń nazw.</span><span class="sxs-lookup"><span data-stu-id="68f2b-110">The system now creates your namespace and enables it.</span></span> <span data-ttu-id="68f2b-111">Po kilku minutach system aprowizuje zasoby dla Twojego konta.</span><span class="sxs-lookup"><span data-stu-id="68f2b-111">After a few minutes, the system provisions resources for your account.</span></span>

### <a name="obtain-the-management-credentials"></a><span data-ttu-id="68f2b-112">Uzyskiwanie poświadczeń zarządzania</span><span class="sxs-lookup"><span data-stu-id="68f2b-112">Obtain the management credentials</span></span>
1. <span data-ttu-id="68f2b-113">Na liście przestrzeni nazw kliknij nowo utworzoną nazwę przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="68f2b-113">In the list of namespaces, click the newly created namespace name.</span></span>
2. <span data-ttu-id="68f2b-114">W bloku przestrzeni nazw usługi Service Bus kliknij pozycję **Zasady dostępu współdzielonego**.</span><span class="sxs-lookup"><span data-stu-id="68f2b-114">In the namespace blade, click **Shared access policies**.</span></span>
3. <span data-ttu-id="68f2b-115">W bloku **Zasady dostępu współdzielonego** kliknij pozycję **RootManageSharedAccessKey**.</span><span class="sxs-lookup"><span data-stu-id="68f2b-115">In the **Shared access policies** blade, click **RootManageSharedAccessKey**.</span></span>
   
    ![connection-info][connection-info]
4. <span data-ttu-id="68f2b-117">W bloku **Zasady: RootManageSharedAccessKey** kliknij przycisk kopiowania obok pozycji **Parametry połączenia — klucz podstawowy**, aby skopiować parametry połączenia do schowka w celu późniejszego użycia.</span><span class="sxs-lookup"><span data-stu-id="68f2b-117">In the **Policy: RootManageSharedAccessKey** blade, click the copy button next to **Connection string–primary key**, to copy the connection string to your clipboard for later use.</span></span> <span data-ttu-id="68f2b-118">Wklej tę wartość do Notatnika lub innej tymczasowej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="68f2b-118">Paste this value into Notepad or some other temporary location.</span></span>
   
    ![connection-string][connection-string]

5. <span data-ttu-id="68f2b-120">Powtórz poprzedni krok, kopiując i wklejając wartość pozycji **Klucz podstawowy** w lokalizacji tymczasowej do późniejszego użycia.</span><span class="sxs-lookup"><span data-stu-id="68f2b-120">Repeat the previous step, copying and pasting the value of **Primary key** to a temporary location for later use.</span></span>  

<!--Image references-->

[create-namespace]: ./media/relay-create-namespace-portal/create-namespace.png
[connection-info]: ./media/relay-create-namespace-portal/connection-info.png
[connection-string]: ./media/relay-create-namespace-portal/connection-string.png
[Azure portal]: https://portal.azure.com
