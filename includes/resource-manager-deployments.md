## <a name="incremental-and-complete-deployments"></a><span data-ttu-id="f1671-101">Przyrostowe i pełne wdrożenia</span><span class="sxs-lookup"><span data-stu-id="f1671-101">Incremental and complete deployments</span></span>
<span data-ttu-id="f1671-102">Podczas wdrażania zasobów, należy określić, że wdrożenie jest aktualizacji przyrostowej i pełnej aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="f1671-102">When deploying your resources, you specify that the deployment is either an incremental update or a complete update.</span></span> <span data-ttu-id="f1671-103">Główną różnicą między tych dwóch trybów jest jak Resource Manager obsługuje istniejących zasobów w grupie zasobów, które nie znajdują się w szablonie:</span><span class="sxs-lookup"><span data-stu-id="f1671-103">The primary difference between these two modes is how Resource Manager handles existing resources in the resource group that are not in the template:</span></span>

* <span data-ttu-id="f1671-104">W trybie pełnej, Menedżer zasobów **usuwa** zasobów, które istnieją w grupie zasobów, ale nie są określone w szablonie.</span><span class="sxs-lookup"><span data-stu-id="f1671-104">In complete mode, Resource Manager **deletes** resources that exist in the resource group but are not specified in the template.</span></span> 
* <span data-ttu-id="f1671-105">W trybie przyrostowych, Menedżer zasobów **pozostawia niezmienione** zasobów, które istnieją w grupie zasobów, ale nie są określone w szablonie.</span><span class="sxs-lookup"><span data-stu-id="f1671-105">In incremental mode, Resource Manager **leaves unchanged** resources that exist in the resource group but are not specified in the template.</span></span>

<span data-ttu-id="f1671-106">Dla obu trybów Resource Manager podejmie próbę zapewnić wszystkich zasobów określone w szablonie.</span><span class="sxs-lookup"><span data-stu-id="f1671-106">For both modes, Resource Manager attempts to provision all resources specified in the template.</span></span> <span data-ttu-id="f1671-107">Jeśli zasób już istnieje w grupie zasobów i jego ustawienia są takie same jak, wykonanie tej operacji skutkuje bez zmian.</span><span class="sxs-lookup"><span data-stu-id="f1671-107">If the resource already exists in the resource group and its settings are unchanged, the operation results in no change.</span></span> <span data-ttu-id="f1671-108">Jeśli zmienisz ustawienia zasobu zasobu jest udostępniane z tych nowych ustawień.</span><span class="sxs-lookup"><span data-stu-id="f1671-108">If you change the settings for a resource, the resource is provisioned with those new settings.</span></span> <span data-ttu-id="f1671-109">Jeśli próbujesz zaktualizować lokalizację i typ istniejącego zasobu, wdrożenie zakończy się niepowodzeniem z powodu błędu.</span><span class="sxs-lookup"><span data-stu-id="f1671-109">If you attempt to update the location or type of an existing resource, the deployment fails with an error.</span></span> <span data-ttu-id="f1671-110">Zamiast tego należy wdrożyć nowy zasób z lokalizacją lub wpisz, że należy.</span><span class="sxs-lookup"><span data-stu-id="f1671-110">Instead, deploy a new resource with the location or type that you need.</span></span>

<span data-ttu-id="f1671-111">Domyślnie usługi Resource Manager korzysta z trybu przyrostowe.</span><span class="sxs-lookup"><span data-stu-id="f1671-111">By default, Resource Manager uses the incremental mode.</span></span>

<span data-ttu-id="f1671-112">Aby zilustrować różnica między trybami przyrostowe i pełne, rozważmy następujący scenariusz.</span><span class="sxs-lookup"><span data-stu-id="f1671-112">To illustrate the difference between incremental and complete modes, consider the following scenario.</span></span>

<span data-ttu-id="f1671-113">**Istniejąca grupa zasobów** zawiera:</span><span class="sxs-lookup"><span data-stu-id="f1671-113">**Existing Resource Group** contains:</span></span>

* <span data-ttu-id="f1671-114">Zasobów A</span><span class="sxs-lookup"><span data-stu-id="f1671-114">Resource A</span></span>
* <span data-ttu-id="f1671-115">Zasób B</span><span class="sxs-lookup"><span data-stu-id="f1671-115">Resource B</span></span>
* <span data-ttu-id="f1671-116">Zasób C</span><span class="sxs-lookup"><span data-stu-id="f1671-116">Resource C</span></span>

<span data-ttu-id="f1671-117">**Szablon** definiuje:</span><span class="sxs-lookup"><span data-stu-id="f1671-117">**Template** defines:</span></span>

* <span data-ttu-id="f1671-118">Zasobów A</span><span class="sxs-lookup"><span data-stu-id="f1671-118">Resource A</span></span>
* <span data-ttu-id="f1671-119">Zasób B</span><span class="sxs-lookup"><span data-stu-id="f1671-119">Resource B</span></span>
* <span data-ttu-id="f1671-120">Zasób D</span><span class="sxs-lookup"><span data-stu-id="f1671-120">Resource D</span></span>

<span data-ttu-id="f1671-121">Po wdrożeniu w **przyrostowe** trybie grupa zasobów zawiera:</span><span class="sxs-lookup"><span data-stu-id="f1671-121">When deployed in **incremental** mode, the resource group contains:</span></span>

* <span data-ttu-id="f1671-122">Zasobów A</span><span class="sxs-lookup"><span data-stu-id="f1671-122">Resource A</span></span>
* <span data-ttu-id="f1671-123">Zasób B</span><span class="sxs-lookup"><span data-stu-id="f1671-123">Resource B</span></span>
* <span data-ttu-id="f1671-124">Zasób C</span><span class="sxs-lookup"><span data-stu-id="f1671-124">Resource C</span></span>
* <span data-ttu-id="f1671-125">Zasób D</span><span class="sxs-lookup"><span data-stu-id="f1671-125">Resource D</span></span>

<span data-ttu-id="f1671-126">Po wdrożeniu w **pełną** trybie C zasób zostanie usunięty.</span><span class="sxs-lookup"><span data-stu-id="f1671-126">When deployed in **complete** mode, Resource C is deleted.</span></span> <span data-ttu-id="f1671-127">Grupa zasobów zawiera:</span><span class="sxs-lookup"><span data-stu-id="f1671-127">The resource group contains:</span></span>

* <span data-ttu-id="f1671-128">Zasobów A</span><span class="sxs-lookup"><span data-stu-id="f1671-128">Resource A</span></span>
* <span data-ttu-id="f1671-129">Zasób B</span><span class="sxs-lookup"><span data-stu-id="f1671-129">Resource B</span></span>
* <span data-ttu-id="f1671-130">Zasób D</span><span class="sxs-lookup"><span data-stu-id="f1671-130">Resource D</span></span>
