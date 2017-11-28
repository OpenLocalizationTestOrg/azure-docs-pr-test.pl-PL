## <a name="set-up-azure-powershell-for-azure-dns"></a><span data-ttu-id="509e1-101">Konfigurowanie programu Azure PowerShell dla usługi Azure DNS</span><span class="sxs-lookup"><span data-stu-id="509e1-101">Set up Azure PowerShell for Azure DNS</span></span>

### <a name="before-you-begin"></a><span data-ttu-id="509e1-102">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="509e1-102">Before you begin</span></span>

<span data-ttu-id="509e1-103">Przed rozpoczęciem konfiguracji sprawdź, czy dysponujesz następującymi elementami:</span><span class="sxs-lookup"><span data-stu-id="509e1-103">Verify that you have the following items before beginning your configuration.</span></span>

* <span data-ttu-id="509e1-104">Subskrypcja platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="509e1-104">An Azure subscription.</span></span> <span data-ttu-id="509e1-105">Jeśli nie masz jeszcze subskrypcji platformy Azure, możesz aktywować [korzyści dla subskrybentów MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) lub utworzyć [bezpłatne konto](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="509e1-105">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="509e1-106">Musisz zainstalować najnowszą wersję poleceń cmdlet programu PowerShell Menedżera zasobów Azure.</span><span class="sxs-lookup"><span data-stu-id="509e1-106">You need to install the latest version of the Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="509e1-107">Aby uzyskać więcej informacji, zobacz [Instalowanie i konfigurowanie programu Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="509e1-107">For more information, see [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span>

### <a name="sign-in-to-your-azure-account"></a><span data-ttu-id="509e1-108">Zaloguj się do swojego konta platformy Azure</span><span class="sxs-lookup"><span data-stu-id="509e1-108">Sign in to your Azure account</span></span>

<span data-ttu-id="509e1-109">Otwórz konsolę programu PowerShell i połącz się ze swoim kontem.</span><span class="sxs-lookup"><span data-stu-id="509e1-109">Open your PowerShell console and connect to your account.</span></span> <span data-ttu-id="509e1-110">Aby uzyskać więcej informacji, zobacz [przy użyciu programu PowerShell z usługą Resource Manager](../articles/azure-resource-manager/powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="509e1-110">For more information, see [Using PowerShell with Resource Manager](../articles/azure-resource-manager/powershell-azure-resource-manager.md).</span></span>

```powershell
Login-AzureRmAccount
```

### <a name="select-the-subscription"></a><span data-ttu-id="509e1-111">Wybierz subskrypcję</span><span class="sxs-lookup"><span data-stu-id="509e1-111">Select the subscription</span></span>
 
<span data-ttu-id="509e1-112">Sprawdź subskrypcje dostępne na koncie.</span><span class="sxs-lookup"><span data-stu-id="509e1-112">Check the subscriptions for the account.</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="509e1-113">Wybierz subskrypcję platformy Azure do użycia.</span><span class="sxs-lookup"><span data-stu-id="509e1-113">Choose which of your Azure subscriptions to use.</span></span>

```powershell
Select-AzureRmSubscription -SubscriptionName "your_subscription_name"
```

### <a name="create-a-resource-group"></a><span data-ttu-id="509e1-114">Tworzenie grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="509e1-114">Create a resource group</span></span>

<span data-ttu-id="509e1-115">Usługa Azure Resource Manager wymaga, aby wszystkie grupy zasobów określały lokalizację.</span><span class="sxs-lookup"><span data-stu-id="509e1-115">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="509e1-116">Ta lokalizacja będzie używana jako domyślna lokalizacja dla zasobów w danej grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="509e1-116">This location is used as the default location for resources in that resource group.</span></span> <span data-ttu-id="509e1-117">Ponieważ jednak wszystkie zasoby DNS są globalne, a nie regionalne, wybór lokalizacji grupy zasobów nie ma wpływu na usługę Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="509e1-117">However, because all DNS resources are global, not regional, the choice of resource group location has no impact on Azure DNS.</span></span>

<span data-ttu-id="509e1-118">Ten krok można pominąć, jeśli używasz istniejącej grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="509e1-118">You can skip this step if you are using an existing resource group.</span></span>

```powershell
New-AzureRmResourceGroup -Name MyAzureResourceGroup -location "West US"
```

### <a name="register-resource-provider"></a><span data-ttu-id="509e1-119">Rejestrowanie dostawcy zasobów</span><span class="sxs-lookup"><span data-stu-id="509e1-119">Register resource provider</span></span>

<span data-ttu-id="509e1-120">Usługa Azure DNS jest zarządzana przez dostawcę zasobów Microsoft.Network.</span><span class="sxs-lookup"><span data-stu-id="509e1-120">The Azure DNS service is managed by the Microsoft.Network resource provider.</span></span> <span data-ttu-id="509e1-121">Aby można było korzystać z usługi Azure DNS, Twoja subskrypcja platformy Azure musi być zarejestrowana do używania tego dostawcy zasobów.</span><span class="sxs-lookup"><span data-stu-id="509e1-121">Your Azure subscription must be registered to use this resource provider before you can use Azure DNS.</span></span> <span data-ttu-id="509e1-122">Jest to jednorazowa operacja dla każdej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="509e1-122">This is a one-time operation for each subscription.</span></span>

```powershell
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Network
```