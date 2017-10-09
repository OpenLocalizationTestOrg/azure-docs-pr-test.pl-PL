## <a name="set-up-azure-cli-for-azure-dns"></a><span data-ttu-id="46e88-101">Konfigurowanie interfejsu wiersza polecenia platformy Azure dla usługi Azure DNS</span><span class="sxs-lookup"><span data-stu-id="46e88-101">Set up Azure CLI for Azure DNS</span></span>

### <a name="before-you-begin"></a><span data-ttu-id="46e88-102">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="46e88-102">Before you begin</span></span>

<span data-ttu-id="46e88-103">Sprawdź, czy masz hello poniższych elementach przed rozpoczęciem konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="46e88-103">Verify that you have hello following items before beginning your configuration.</span></span>

* <span data-ttu-id="46e88-104">Subskrypcja platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="46e88-104">An Azure subscription.</span></span> <span data-ttu-id="46e88-105">Jeśli nie masz jeszcze subskrypcji platformy Azure, możesz aktywować [korzyści dla subskrybentów MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) lub utworzyć [bezpłatne konto](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="46e88-105">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="46e88-106">Zainstaluj najnowszą wersję hello hello Azure CLI, dostępne dla systemu Windows, Linux lub MAC.</span><span class="sxs-lookup"><span data-stu-id="46e88-106">Install hello latest version of hello Azure CLI, available for Windows, Linux, or MAC.</span></span> <span data-ttu-id="46e88-107">Więcej informacji znajduje się w temacie [hello instalowanie interfejsu wiersza polecenia Azure](../articles/cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="46e88-107">More information is available at [Install hello Azure CLI](../articles/cli-install-nodejs.md).</span></span>

### <a name="sign-in-tooyour-azure-account"></a><span data-ttu-id="46e88-108">Zaloguj się tooyour konto platformy Azure</span><span class="sxs-lookup"><span data-stu-id="46e88-108">Sign in tooyour Azure account</span></span>

<span data-ttu-id="46e88-109">Otwórz okno konsoli i uwierzytelnij się przy użyciu swoich poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="46e88-109">Open a console window and authenticate with your credentials.</span></span> <span data-ttu-id="46e88-110">Aby uzyskać więcej informacji, zobacz [Zaloguj tooAzure z hello wiersza polecenia platformy Azure](../articles/xplat-cli-connect.md)</span><span class="sxs-lookup"><span data-stu-id="46e88-110">For more information, see [Log in tooAzure from hello Azure CLI](../articles/xplat-cli-connect.md)</span></span>

```azurecli
azure login
```

### <a name="switch-cli-mode"></a><span data-ttu-id="46e88-111">Przełącz tryb interfejsu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="46e88-111">Switch CLI mode</span></span>

<span data-ttu-id="46e88-112">Usługa Azure DNS korzysta z usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="46e88-112">Azure DNS uses Azure Resource Manager.</span></span> <span data-ttu-id="46e88-113">Upewnij się, że przełącznik polecenia usługi Azure Resource Manager toouse tryb interfejsu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="46e88-113">Make sure you switch CLI mode toouse Azure Resource Manager commands.</span></span>

```azurecli
azure config mode arm
```

### <a name="select-hello-subscription"></a><span data-ttu-id="46e88-114">Wybierz subskrypcję hello</span><span class="sxs-lookup"><span data-stu-id="46e88-114">Select hello subscription</span></span>

<span data-ttu-id="46e88-115">Sprawdź subskrypcje hello hello konta.</span><span class="sxs-lookup"><span data-stu-id="46e88-115">Check hello subscriptions for hello account.</span></span>

```azurecli
azure account list
```

<span data-ttu-id="46e88-116">Wybierz z toouse Twojej subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="46e88-116">Choose which of your Azure subscriptions toouse.</span></span>

```azurecli
azure account set "subscription name"
```

### <a name="create-a-resource-group"></a><span data-ttu-id="46e88-117">Tworzenie grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="46e88-117">Create a resource group</span></span>

<span data-ttu-id="46e88-118">Usługa Azure Resource Manager wymaga, aby wszystkie grupy zasobów określały lokalizację.</span><span class="sxs-lookup"><span data-stu-id="46e88-118">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="46e88-119">Służy to jako hello domyślna lokalizacja dla zasobów w danej grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="46e88-119">This is used as hello default location for resources in that resource group.</span></span> <span data-ttu-id="46e88-120">Jednak ponieważ wszystkie zasoby DNS są globalne, a nie regionalne, wybór hello lokalizacja grupy zasobów nie ma wpływu na usługi Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="46e88-120">However, because all DNS resources are global, not regional, hello choice of resource group location has no impact on Azure DNS.</span></span>

<span data-ttu-id="46e88-121">Ten krok można pominąć, jeśli używasz istniejącej grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="46e88-121">You can skip this step if you are using an existing resource group.</span></span>

```azurecli
azure group create -n myresourcegroup --location "West US"
```

### <a name="register-resource-provider"></a><span data-ttu-id="46e88-122">Rejestrowanie dostawcy zasobów</span><span class="sxs-lookup"><span data-stu-id="46e88-122">Register resource provider</span></span>

<span data-ttu-id="46e88-123">Usługa Azure DNS Hello jest zarządzana przez dostawcę zasobów Microsoft.Network hello.</span><span class="sxs-lookup"><span data-stu-id="46e88-123">hello Azure DNS service is managed by hello Microsoft.Network resource provider.</span></span> <span data-ttu-id="46e88-124">Twoja subskrypcja platformy Azure musi być zarejestrowany toouse tego dostawcy zasobów przed użyciem usługi Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="46e88-124">Your Azure subscription must be registered toouse this resource provider before you can use Azure DNS.</span></span> <span data-ttu-id="46e88-125">Jest to jednorazowa operacja dla każdej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="46e88-125">This is a one-time operation for each subscription.</span></span>

```azurecli
azure provider register --namespace Microsoft.Network
```

