## <a name="set-up-azure-powershell-for-azure-dns"></a><span data-ttu-id="b0049-101">Konfigurowanie programu Azure PowerShell dla usługi Azure DNS</span><span class="sxs-lookup"><span data-stu-id="b0049-101">Set up Azure PowerShell for Azure DNS</span></span>

### <a name="before-you-begin"></a><span data-ttu-id="b0049-102">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="b0049-102">Before you begin</span></span>

<span data-ttu-id="b0049-103">Sprawdź, czy masz hello poniższych elementach przed rozpoczęciem konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="b0049-103">Verify that you have hello following items before beginning your configuration.</span></span>

* <span data-ttu-id="b0049-104">Subskrypcja platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="b0049-104">An Azure subscription.</span></span> <span data-ttu-id="b0049-105">Jeśli nie masz jeszcze subskrypcji platformy Azure, możesz aktywować [korzyści dla subskrybentów MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) lub utworzyć [bezpłatne konto](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b0049-105">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="b0049-106">Należy tooinstall hello najnowszą wersję hello poleceń cmdlet programu PowerShell usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="b0049-106">You need tooinstall hello latest version of hello Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="b0049-107">Aby uzyskać więcej informacji, zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="b0049-107">For more information, see [How tooinstall and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span>

### <a name="sign-in-tooyour-azure-account"></a><span data-ttu-id="b0049-108">Zaloguj się tooyour konto platformy Azure</span><span class="sxs-lookup"><span data-stu-id="b0049-108">Sign in tooyour Azure account</span></span>

<span data-ttu-id="b0049-109">Otwórz konsolę programu PowerShell i Połącz konto tooyour.</span><span class="sxs-lookup"><span data-stu-id="b0049-109">Open your PowerShell console and connect tooyour account.</span></span> <span data-ttu-id="b0049-110">Aby uzyskać więcej informacji, zobacz [przy użyciu programu PowerShell z usługą Resource Manager](../articles/azure-resource-manager/powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="b0049-110">For more information, see [Using PowerShell with Resource Manager](../articles/azure-resource-manager/powershell-azure-resource-manager.md).</span></span>

```powershell
Login-AzureRmAccount
```

### <a name="select-hello-subscription"></a><span data-ttu-id="b0049-111">Wybierz subskrypcję hello</span><span class="sxs-lookup"><span data-stu-id="b0049-111">Select hello subscription</span></span>
 
<span data-ttu-id="b0049-112">Sprawdź subskrypcje hello hello konta.</span><span class="sxs-lookup"><span data-stu-id="b0049-112">Check hello subscriptions for hello account.</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="b0049-113">Wybierz z toouse Twojej subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="b0049-113">Choose which of your Azure subscriptions toouse.</span></span>

```powershell
Select-AzureRmSubscription -SubscriptionName "your_subscription_name"
```

### <a name="create-a-resource-group"></a><span data-ttu-id="b0049-114">Tworzenie grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="b0049-114">Create a resource group</span></span>

<span data-ttu-id="b0049-115">Usługa Azure Resource Manager wymaga, aby wszystkie grupy zasobów określały lokalizację.</span><span class="sxs-lookup"><span data-stu-id="b0049-115">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="b0049-116">Ta lokalizacja jest używana jako hello domyślna lokalizacja dla zasobów w danej grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="b0049-116">This location is used as hello default location for resources in that resource group.</span></span> <span data-ttu-id="b0049-117">Jednak ponieważ wszystkie zasoby DNS są globalne, a nie regionalne, wybór hello lokalizacja grupy zasobów nie ma wpływu na usługi Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="b0049-117">However, because all DNS resources are global, not regional, hello choice of resource group location has no impact on Azure DNS.</span></span>

<span data-ttu-id="b0049-118">Ten krok można pominąć, jeśli używasz istniejącej grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="b0049-118">You can skip this step if you are using an existing resource group.</span></span>

```powershell
New-AzureRmResourceGroup -Name MyAzureResourceGroup -location "West US"
```

### <a name="register-resource-provider"></a><span data-ttu-id="b0049-119">Rejestrowanie dostawcy zasobów</span><span class="sxs-lookup"><span data-stu-id="b0049-119">Register resource provider</span></span>

<span data-ttu-id="b0049-120">Usługa Azure DNS Hello jest zarządzana przez dostawcę zasobów Microsoft.Network hello.</span><span class="sxs-lookup"><span data-stu-id="b0049-120">hello Azure DNS service is managed by hello Microsoft.Network resource provider.</span></span> <span data-ttu-id="b0049-121">Twoja subskrypcja platformy Azure musi być zarejestrowany toouse tego dostawcy zasobów przed użyciem usługi Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="b0049-121">Your Azure subscription must be registered toouse this resource provider before you can use Azure DNS.</span></span> <span data-ttu-id="b0049-122">Jest to jednorazowa operacja dla każdej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="b0049-122">This is a one-time operation for each subscription.</span></span>

```powershell
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Network
```