## <a name="incremental-and-complete-deployments"></a><span data-ttu-id="79cd5-101">Przyrostowe i pełne wdrożenia</span><span class="sxs-lookup"><span data-stu-id="79cd5-101">Incremental and complete deployments</span></span>
<span data-ttu-id="79cd5-102">W przypadku wdrażania zasobów, należy określić hello wdrożenia aktualizacji przyrostowej i pełnej aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="79cd5-102">When deploying your resources, you specify that hello deployment is either an incremental update or a complete update.</span></span> <span data-ttu-id="79cd5-103">Witaj podstawowa różnica między tych dwóch trybów jest jak Resource Manager obsługuje istniejących zasobów w grupie zasobów hello, które nie są w szablonie hello:</span><span class="sxs-lookup"><span data-stu-id="79cd5-103">hello primary difference between these two modes is how Resource Manager handles existing resources in hello resource group that are not in hello template:</span></span>

* <span data-ttu-id="79cd5-104">W trybie pełnej, Menedżer zasobów **usuwa** zasobów, które istnieją w grupie zasobów hello, ale nie są określone w szablonie hello.</span><span class="sxs-lookup"><span data-stu-id="79cd5-104">In complete mode, Resource Manager **deletes** resources that exist in hello resource group but are not specified in hello template.</span></span> 
* <span data-ttu-id="79cd5-105">W trybie przyrostowych, Menedżer zasobów **pozostawia niezmienione** zasobów, które istnieją w grupie zasobów hello, ale nie są określone w szablonie hello.</span><span class="sxs-lookup"><span data-stu-id="79cd5-105">In incremental mode, Resource Manager **leaves unchanged** resources that exist in hello resource group but are not specified in hello template.</span></span>

<span data-ttu-id="79cd5-106">Dla obu trybów Resource Manager podejmie tooprovision wszystkich zasobów określonej w szablonie hello.</span><span class="sxs-lookup"><span data-stu-id="79cd5-106">For both modes, Resource Manager attempts tooprovision all resources specified in hello template.</span></span> <span data-ttu-id="79cd5-107">Jeśli hello zasób już istnieje w grupie zasobów hello, jego ustawienia są takie same jak hello wynikiem operacji bez zmian.</span><span class="sxs-lookup"><span data-stu-id="79cd5-107">If hello resource already exists in hello resource group and its settings are unchanged, hello operation results in no change.</span></span> <span data-ttu-id="79cd5-108">Jeśli zmienisz ustawienia hello zasobu zasobów hello jest udostępniane z te nowe ustawienia.</span><span class="sxs-lookup"><span data-stu-id="79cd5-108">If you change hello settings for a resource, hello resource is provisioned with those new settings.</span></span> <span data-ttu-id="79cd5-109">Jeśli tooupdate hello lokalizację i typ istniejącego zasobu, hello wdrożenie zakończy się niepowodzeniem z powodu błędu.</span><span class="sxs-lookup"><span data-stu-id="79cd5-109">If you attempt tooupdate hello location or type of an existing resource, hello deployment fails with an error.</span></span> <span data-ttu-id="79cd5-110">Zamiast tego należy wdrożyć nowy zasób z lokalizacją hello lub wpisz, że należy.</span><span class="sxs-lookup"><span data-stu-id="79cd5-110">Instead, deploy a new resource with hello location or type that you need.</span></span>

<span data-ttu-id="79cd5-111">Domyślnie usługi Resource Manager tryb hello przyrostowe.</span><span class="sxs-lookup"><span data-stu-id="79cd5-111">By default, Resource Manager uses hello incremental mode.</span></span>

<span data-ttu-id="79cd5-112">tooillustrate hello różnica między trybami przyrostowe i pełne, należy wziąć pod uwagę powitania od scenariusza.</span><span class="sxs-lookup"><span data-stu-id="79cd5-112">tooillustrate hello difference between incremental and complete modes, consider hello following scenario.</span></span>

<span data-ttu-id="79cd5-113">**Istniejąca grupa zasobów** zawiera:</span><span class="sxs-lookup"><span data-stu-id="79cd5-113">**Existing Resource Group** contains:</span></span>

* <span data-ttu-id="79cd5-114">Zasobów A</span><span class="sxs-lookup"><span data-stu-id="79cd5-114">Resource A</span></span>
* <span data-ttu-id="79cd5-115">Zasób B</span><span class="sxs-lookup"><span data-stu-id="79cd5-115">Resource B</span></span>
* <span data-ttu-id="79cd5-116">Zasób C</span><span class="sxs-lookup"><span data-stu-id="79cd5-116">Resource C</span></span>

<span data-ttu-id="79cd5-117">**Szablon** definiuje:</span><span class="sxs-lookup"><span data-stu-id="79cd5-117">**Template** defines:</span></span>

* <span data-ttu-id="79cd5-118">Zasobów A</span><span class="sxs-lookup"><span data-stu-id="79cd5-118">Resource A</span></span>
* <span data-ttu-id="79cd5-119">Zasób B</span><span class="sxs-lookup"><span data-stu-id="79cd5-119">Resource B</span></span>
* <span data-ttu-id="79cd5-120">Zasób D</span><span class="sxs-lookup"><span data-stu-id="79cd5-120">Resource D</span></span>

<span data-ttu-id="79cd5-121">Po wdrożeniu w **przyrostowe** trybie hello grupa zasobów zawiera:</span><span class="sxs-lookup"><span data-stu-id="79cd5-121">When deployed in **incremental** mode, hello resource group contains:</span></span>

* <span data-ttu-id="79cd5-122">Zasobów A</span><span class="sxs-lookup"><span data-stu-id="79cd5-122">Resource A</span></span>
* <span data-ttu-id="79cd5-123">Zasób B</span><span class="sxs-lookup"><span data-stu-id="79cd5-123">Resource B</span></span>
* <span data-ttu-id="79cd5-124">Zasób C</span><span class="sxs-lookup"><span data-stu-id="79cd5-124">Resource C</span></span>
* <span data-ttu-id="79cd5-125">Zasób D</span><span class="sxs-lookup"><span data-stu-id="79cd5-125">Resource D</span></span>

<span data-ttu-id="79cd5-126">Po wdrożeniu w **pełną** trybie C zasób zostanie usunięty.</span><span class="sxs-lookup"><span data-stu-id="79cd5-126">When deployed in **complete** mode, Resource C is deleted.</span></span> <span data-ttu-id="79cd5-127">Grupa zasobów Hello zawiera:</span><span class="sxs-lookup"><span data-stu-id="79cd5-127">hello resource group contains:</span></span>

* <span data-ttu-id="79cd5-128">Zasobów A</span><span class="sxs-lookup"><span data-stu-id="79cd5-128">Resource A</span></span>
* <span data-ttu-id="79cd5-129">Zasób B</span><span class="sxs-lookup"><span data-stu-id="79cd5-129">Resource B</span></span>
* <span data-ttu-id="79cd5-130">Zasób D</span><span class="sxs-lookup"><span data-stu-id="79cd5-130">Resource D</span></span>
