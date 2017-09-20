## <a name="prepare-to-authenticate-azure-resource-manager-requests"></a><span data-ttu-id="bcce9-101">Przygotowanie do uwierzytelniania żądań usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="bcce9-101">Prepare to authenticate Azure Resource Manager requests</span></span>
<span data-ttu-id="bcce9-102">Musi uwierzytelniać wszystkie operacje, które należy wykonać na zasobów przy użyciu [usługi Azure Resource Manager] [ lnk-authenticate-arm] z usługi Azure Active Directory (AD).</span><span class="sxs-lookup"><span data-stu-id="bcce9-102">You must authenticate all the operations that you perform on resources using the [Azure Resource Manager][lnk-authenticate-arm] with Azure Active Directory (AD).</span></span> <span data-ttu-id="bcce9-103">Najprostszym sposobem skonfigurowania tego jest za pomocą programu PowerShell lub wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="bcce9-103">The easiest way to configure this is to use PowerShell or Azure CLI.</span></span>

<span data-ttu-id="bcce9-104">Zainstaluj [poleceń cmdlet programu Azure PowerShell] [ lnk-powershell-install] przed kontynuowaniem.</span><span class="sxs-lookup"><span data-stu-id="bcce9-104">Install the [Azure PowerShell cmdlets][lnk-powershell-install] before you continue.</span></span>

<span data-ttu-id="bcce9-105">Poniższe kroki pokazują, jak skonfigurować uwierzytelnianie hasła dla aplikacji usługi AD przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bcce9-105">The following steps show how to set up password authentication for an AD application using PowerShell.</span></span> <span data-ttu-id="bcce9-106">Te polecenia można wykonać w standardowej sesji programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bcce9-106">You can run these commands in a standard PowerShell session.</span></span>

1. <span data-ttu-id="bcce9-107">Zaloguj się do subskrypcji platformy Azure przy użyciu następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="bcce9-107">Log in to your Azure subscription using the following command:</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

1. <span data-ttu-id="bcce9-108">Jeśli masz wiele subskrypcji Azure, logowanie do platformy Azure udziela dostępu do subskrypcji platformy Azure skojarzone z poświadczeniami użytkownika.</span><span class="sxs-lookup"><span data-stu-id="bcce9-108">If you have multiple Azure subscriptions, signing in to Azure grants you access to all the Azure subscriptions associated with your credentials.</span></span> <span data-ttu-id="bcce9-109">Aby wyświetlić listę dostępnych przy użyciu subskrypcji platformy Azure, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="bcce9-109">Use the following command to list the Azure subscriptions available for you to use:</span></span>

    ```powershell
    Get-AzureRMSubscription
    ```

    <span data-ttu-id="bcce9-110">Użyj następującego polecenia, aby wybrać subskrypcję, która ma być używany do uruchamiania polecenia do zarządzania Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="bcce9-110">Use the following command to select subscription that you want to use to run the commands to manage your IoT hub.</span></span> <span data-ttu-id="bcce9-111">Przy użyciu subskrypcji nazwa lub identyfikator z danych wyjściowych poprzednie polecenie:</span><span class="sxs-lookup"><span data-stu-id="bcce9-111">You can use either the subscription name or ID from the output of the previous command:</span></span>

    ```powershell
    Select-AzureRMSubscription `
        -SubscriptionName "{your subscription name}"
    ```

2. <span data-ttu-id="bcce9-112">Zanotuj Twojej **TenantId** i **SubscriptionId**.</span><span class="sxs-lookup"><span data-stu-id="bcce9-112">Make a note of your **TenantId** and **SubscriptionId**.</span></span> <span data-ttu-id="bcce9-113">Należy je później.</span><span class="sxs-lookup"><span data-stu-id="bcce9-113">You need them later.</span></span>
3. <span data-ttu-id="bcce9-114">Utwórz nową aplikację usługi Azure Active Directory przy użyciu następujące polecenie, zastępując symbole zastępcze:</span><span class="sxs-lookup"><span data-stu-id="bcce9-114">Create a new Azure Active Directory application using the following command, replacing the place holders:</span></span>
   
   * <span data-ttu-id="bcce9-115">**{Nazwa wyświetlana}:** nazwę wyświetlaną dla aplikacji, takich jak **MySampleApp**</span><span class="sxs-lookup"><span data-stu-id="bcce9-115">**{Display name}:** a display name for your application such as **MySampleApp**</span></span>
   * <span data-ttu-id="bcce9-116">**{Adres URL strony głównej}:** adres URL strony głównej aplikacji takich jak **http://mysampleapp/home**.</span><span class="sxs-lookup"><span data-stu-id="bcce9-116">**{Home page URL}:** the URL of the home page of your app such as **http://mysampleapp/home**.</span></span> <span data-ttu-id="bcce9-117">Ten adres URL nie musi wskazywać rzeczywistych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="bcce9-117">This URL does not need to point to a real application.</span></span>
   * <span data-ttu-id="bcce9-118">**{Identyfikator aplikacji}:** Unikatowy identyfikator **http://mysampleapp**.</span><span class="sxs-lookup"><span data-stu-id="bcce9-118">**{Application identifier}:** A unique identifier such as **http://mysampleapp**.</span></span> <span data-ttu-id="bcce9-119">Ten adres URL nie musi wskazywać rzeczywistych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="bcce9-119">This URL does not need to point to a real application.</span></span>
   * <span data-ttu-id="bcce9-120">**{Hasło}:** hasła używanego do uwierzytelniania z aplikacji.</span><span class="sxs-lookup"><span data-stu-id="bcce9-120">**{Password}:** A password that you use to authenticate with your app.</span></span>
     
     ```powershell
     New-AzureRmADApplication -DisplayName {Display name} -HomePage {Home page URL} -IdentifierUris {Application identifier} -Password {Password}
     ```
4. <span data-ttu-id="bcce9-121">Zanotuj **ApplicationId** aplikacji został utworzony.</span><span class="sxs-lookup"><span data-stu-id="bcce9-121">Make a note of the **ApplicationId** of the application you created.</span></span> <span data-ttu-id="bcce9-122">Należy to później.</span><span class="sxs-lookup"><span data-stu-id="bcce9-122">You need this later.</span></span>
5. <span data-ttu-id="bcce9-123">Utwórz nową główną nazwę usługi, za pomocą następującego polecenia, zastępując **{MyApplicationId}** z **ApplicationId** w poprzednim kroku:</span><span class="sxs-lookup"><span data-stu-id="bcce9-123">Create a new service principal using the following command, replacing **{MyApplicationId}** with the **ApplicationId** from the previous step:</span></span>
   
    ```powershell
    New-AzureRmADServicePrincipal -ApplicationId {MyApplicationId}
    ```
6. <span data-ttu-id="bcce9-124">Konfigurowanie przypisania roli za pomocą następującego polecenia, zastępując **{MyApplicationId}** z Twojej **ApplicationId**.</span><span class="sxs-lookup"><span data-stu-id="bcce9-124">Set up a role assignment using the following command, replacing **{MyApplicationId}** with your **ApplicationId**.</span></span>
   
    ```powershell
    New-AzureRmRoleAssignment -RoleDefinitionName Owner -ServicePrincipalName {MyApplicationId}
    ```

<span data-ttu-id="bcce9-125">Tworzenie aplikacji usługi Azure AD, która pozwala na uwierzytelnianie z niestandardowych aplikacji C# zostało zakończone.</span><span class="sxs-lookup"><span data-stu-id="bcce9-125">You have now finished creating the Azure AD application that enables you to authenticate from your custom C# application.</span></span> <span data-ttu-id="bcce9-126">W dalszej części tego samouczka niezbędne są następujące wartości:</span><span class="sxs-lookup"><span data-stu-id="bcce9-126">You need the following values later in this tutorial:</span></span>

* <span data-ttu-id="bcce9-127">Dla identyfikatora dzierżawcy</span><span class="sxs-lookup"><span data-stu-id="bcce9-127">TenantId</span></span>
* <span data-ttu-id="bcce9-128">SubscriptionId</span><span class="sxs-lookup"><span data-stu-id="bcce9-128">SubscriptionId</span></span>
* <span data-ttu-id="bcce9-129">Identyfikator aplikacji</span><span class="sxs-lookup"><span data-stu-id="bcce9-129">ApplicationId</span></span>
* <span data-ttu-id="bcce9-130">Hasło</span><span class="sxs-lookup"><span data-stu-id="bcce9-130">Password</span></span>

[lnk-authenticate-arm]: https://msdn.microsoft.com/library/azure/dn790557.aspx
[lnk-powershell-install]: https://docs.microsoft.com/powershell/azure/install-azurerm-ps
