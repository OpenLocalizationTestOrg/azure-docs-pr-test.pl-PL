## <a name="prepare-tooauthenticate-azure-resource-manager-requests"></a><span data-ttu-id="47423-101">Przygotowanie tooauthenticate żądań usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="47423-101">Prepare tooauthenticate Azure Resource Manager requests</span></span>
<span data-ttu-id="47423-102">Musi uwierzytelniać wszystkie operacje hello, które należy wykonać na zasobów przy użyciu hello [usługi Azure Resource Manager] [ lnk-authenticate-arm] z usługi Azure Active Directory (AD).</span><span class="sxs-lookup"><span data-stu-id="47423-102">You must authenticate all hello operations that you perform on resources using hello [Azure Resource Manager][lnk-authenticate-arm] with Azure Active Directory (AD).</span></span> <span data-ttu-id="47423-103">Najprostszym sposobem tooconfigure Hello jest toouse programu PowerShell lub interfejsu wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="47423-103">hello easiest way tooconfigure this is toouse PowerShell or Azure CLI.</span></span>

<span data-ttu-id="47423-104">Zainstaluj hello [poleceń cmdlet programu Azure PowerShell] [ lnk-powershell-install] przed kontynuowaniem.</span><span class="sxs-lookup"><span data-stu-id="47423-104">Install hello [Azure PowerShell cmdlets][lnk-powershell-install] before you continue.</span></span>

<span data-ttu-id="47423-105">Witaj, jak po Pokaż kroki tooset się uwierzytelniania hasła dla aplikacji usługi AD przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="47423-105">hello following steps show how tooset up password authentication for an AD application using PowerShell.</span></span> <span data-ttu-id="47423-106">Te polecenia można wykonać w standardowej sesji programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="47423-106">You can run these commands in a standard PowerShell session.</span></span>

1. <span data-ttu-id="47423-107">Zaloguj się tooyour subskrypcji platformy Azure przy użyciu hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="47423-107">Log in tooyour Azure subscription using hello following command:</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

1. <span data-ttu-id="47423-108">Jeśli masz wiele subskrypcji Azure, logowanie tooAzure umożliwiają dostęp tooall hello subskrypcji platformy Azure skojarzonych z poświadczeniami użytkownika.</span><span class="sxs-lookup"><span data-stu-id="47423-108">If you have multiple Azure subscriptions, signing in tooAzure grants you access tooall hello Azure subscriptions associated with your credentials.</span></span> <span data-ttu-id="47423-109">Użyj następującego polecenia toolist hello subskrypcji platformy Azure, dostępne dla Ciebie toouse hello:</span><span class="sxs-lookup"><span data-stu-id="47423-109">Use hello following command toolist hello Azure subscriptions available for you toouse:</span></span>

    ```powershell
    Get-AzureRMSubscription
    ```

    <span data-ttu-id="47423-110">Użyj następującego polecenia tooselect subskrypcji ma się, że toouse toorun hello polecenia toomanage Centrum IoT hello.</span><span class="sxs-lookup"><span data-stu-id="47423-110">Use hello following command tooselect subscription that you want toouse toorun hello commands toomanage your IoT hub.</span></span> <span data-ttu-id="47423-111">Identyfikator lub Nazwa subskrypcji hello można użyć z danych wyjściowych hello hello poprzednie polecenie:</span><span class="sxs-lookup"><span data-stu-id="47423-111">You can use either hello subscription name or ID from hello output of hello previous command:</span></span>

    ```powershell
    Select-AzureRMSubscription `
        -SubscriptionName "{your subscription name}"
    ```

2. <span data-ttu-id="47423-112">Zanotuj Twojej **TenantId** i **SubscriptionId**.</span><span class="sxs-lookup"><span data-stu-id="47423-112">Make a note of your **TenantId** and **SubscriptionId**.</span></span> <span data-ttu-id="47423-113">Należy je później.</span><span class="sxs-lookup"><span data-stu-id="47423-113">You need them later.</span></span>
3. <span data-ttu-id="47423-114">Utwórz nową aplikację usługi Azure Active Directory przy użyciu hello następujące polecenie, zastępując symbole zastępcze hello:</span><span class="sxs-lookup"><span data-stu-id="47423-114">Create a new Azure Active Directory application using hello following command, replacing hello place holders:</span></span>
   
   * <span data-ttu-id="47423-115">**{Nazwa wyświetlana}:** nazwę wyświetlaną dla aplikacji, takich jak **MySampleApp**</span><span class="sxs-lookup"><span data-stu-id="47423-115">**{Display name}:** a display name for your application such as **MySampleApp**</span></span>
   * <span data-ttu-id="47423-116">**{Adres URL strony głównej}:** hello adres URL strony głównej hello aplikacji, takich jak **http://mysampleapp/home**.</span><span class="sxs-lookup"><span data-stu-id="47423-116">**{Home page URL}:** hello URL of hello home page of your app such as **http://mysampleapp/home**.</span></span> <span data-ttu-id="47423-117">Ten adres URL nie jest konieczne toopoint tooa rzeczywistej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="47423-117">This URL does not need toopoint tooa real application.</span></span>
   * <span data-ttu-id="47423-118">**{Identyfikator aplikacji}:** Unikatowy identyfikator **http://mysampleapp**.</span><span class="sxs-lookup"><span data-stu-id="47423-118">**{Application identifier}:** A unique identifier such as **http://mysampleapp**.</span></span> <span data-ttu-id="47423-119">Ten adres URL nie jest konieczne toopoint tooa rzeczywistej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="47423-119">This URL does not need toopoint tooa real application.</span></span>
   * <span data-ttu-id="47423-120">**{Hasło}:** hasła, użyj tooauthenticate z aplikacją.</span><span class="sxs-lookup"><span data-stu-id="47423-120">**{Password}:** A password that you use tooauthenticate with your app.</span></span>
     
     ```powershell
     New-AzureRmADApplication -DisplayName {Display name} -HomePage {Home page URL} -IdentifierUris {Application identifier} -Password {Password}
     ```
4. <span data-ttu-id="47423-121">Zanotuj hello **ApplicationId** aplikacji hello został utworzony.</span><span class="sxs-lookup"><span data-stu-id="47423-121">Make a note of hello **ApplicationId** of hello application you created.</span></span> <span data-ttu-id="47423-122">Należy to później.</span><span class="sxs-lookup"><span data-stu-id="47423-122">You need this later.</span></span>
5. <span data-ttu-id="47423-123">Utwórz nową główną nazwę usługi przy użyciu hello następujące polecenie, zastępując **{MyApplicationId}** z hello **ApplicationId** hello w poprzednim kroku:</span><span class="sxs-lookup"><span data-stu-id="47423-123">Create a new service principal using hello following command, replacing **{MyApplicationId}** with hello **ApplicationId** from hello previous step:</span></span>
   
    ```powershell
    New-AzureRmADServicePrincipal -ApplicationId {MyApplicationId}
    ```
6. <span data-ttu-id="47423-124">Konfigurowanie przypisania roli przy użyciu hello następujące polecenie, zastępując **{MyApplicationId}** z Twojej **ApplicationId**.</span><span class="sxs-lookup"><span data-stu-id="47423-124">Set up a role assignment using hello following command, replacing **{MyApplicationId}** with your **ApplicationId**.</span></span>
   
    ```powershell
    New-AzureRmRoleAssignment -RoleDefinitionName Owner -ServicePrincipalName {MyApplicationId}
    ```

<span data-ttu-id="47423-125">Tworzenie aplikacji hello Azure AD, która umożliwia tooauthenticate z niestandardowych aplikacji C# zostało zakończone.</span><span class="sxs-lookup"><span data-stu-id="47423-125">You have now finished creating hello Azure AD application that enables you tooauthenticate from your custom C# application.</span></span> <span data-ttu-id="47423-126">Potrzebne są następujące wartości w dalszej części tego samouczka hello:</span><span class="sxs-lookup"><span data-stu-id="47423-126">You need hello following values later in this tutorial:</span></span>

* <span data-ttu-id="47423-127">Dla identyfikatora dzierżawcy</span><span class="sxs-lookup"><span data-stu-id="47423-127">TenantId</span></span>
* <span data-ttu-id="47423-128">SubscriptionId</span><span class="sxs-lookup"><span data-stu-id="47423-128">SubscriptionId</span></span>
* <span data-ttu-id="47423-129">Identyfikator aplikacji</span><span class="sxs-lookup"><span data-stu-id="47423-129">ApplicationId</span></span>
* <span data-ttu-id="47423-130">Hasło</span><span class="sxs-lookup"><span data-stu-id="47423-130">Password</span></span>

[lnk-authenticate-arm]: https://msdn.microsoft.com/library/azure/dn790557.aspx
[lnk-powershell-install]: https://docs.microsoft.com/powershell/azure/install-azurerm-ps
