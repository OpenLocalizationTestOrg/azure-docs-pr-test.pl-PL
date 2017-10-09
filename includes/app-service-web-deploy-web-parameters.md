<span data-ttu-id="87469-101">Usługi Azure Resource Manager Zdefiniuj parametry dla wartości ma toospecify po wdrożeniu hello szablonu.</span><span class="sxs-lookup"><span data-stu-id="87469-101">With Azure Resource Manager, you define parameters for values you want toospecify when hello template is deployed.</span></span> <span data-ttu-id="87469-102">Szablon Hello zawiera sekcji parametrów zawierający wszystkie hello wartości parametrów.</span><span class="sxs-lookup"><span data-stu-id="87469-102">hello template includes a section called Parameters that contains all of hello parameter values.</span></span>
<span data-ttu-id="87469-103">Należy zdefiniować parametr dla tych wartości, które będą się różnić na podstawie hello projektu, który jest wdrażany lub opartych na środowisku hello, który jest wdrażany z.</span><span class="sxs-lookup"><span data-stu-id="87469-103">You should define a parameter for those values that will vary based on hello project you are deploying or based on hello environment you are deploying to.</span></span> <span data-ttu-id="87469-104">Definiuje parametry dla wartości, które będą zawsze hello takie same.</span><span class="sxs-lookup"><span data-stu-id="87469-104">Do not define parameters for values that will always stay hello same.</span></span> <span data-ttu-id="87469-105">Każda wartość parametru jest używany w hello szablonu toodefine hello zasoby, które zostały wdrożone.</span><span class="sxs-lookup"><span data-stu-id="87469-105">Each parameter value is used in hello template toodefine hello resources that are deployed.</span></span> 

<span data-ttu-id="87469-106">Określając parametry, użyj hello **allowedValues** toospecify pola, które wartości użytkownika można podać podczas wdrażania.</span><span class="sxs-lookup"><span data-stu-id="87469-106">When defining parameters, use hello **allowedValues** field toospecify which values a user can provide during deployment.</span></span> <span data-ttu-id="87469-107">Użyj hello **defaultValue** tooassign pola parametru toohello wartości, jeśli wartość nie zostanie podana podczas wdrażania.</span><span class="sxs-lookup"><span data-stu-id="87469-107">Use hello **defaultValue** field tooassign a value toohello parameter, if no value is provided during deployment.</span></span>

<span data-ttu-id="87469-108">Firma Microsoft będzie opisywać każdego parametru w szablonie hello.</span><span class="sxs-lookup"><span data-stu-id="87469-108">We will describe each parameter in hello template.</span></span>

### <a name="sitename"></a><span data-ttu-id="87469-109">Nazwa witryny</span><span class="sxs-lookup"><span data-stu-id="87469-109">siteName</span></span>
<span data-ttu-id="87469-110">Nazwa Hello hello aplikacji sieci web, że chcesz toocreate.</span><span class="sxs-lookup"><span data-stu-id="87469-110">hello name of hello web app that you wish toocreate.</span></span>

    "siteName":{
      "type":"string"
    }

### <a name="hostingplanname"></a><span data-ttu-id="87469-111">hostingPlanName</span><span class="sxs-lookup"><span data-stu-id="87469-111">hostingPlanName</span></span>
<span data-ttu-id="87469-112">Nazwa Hello hello usługi aplikacji — planowanie toouse do obsługi aplikacji sieci web hello.</span><span class="sxs-lookup"><span data-stu-id="87469-112">hello name of hello App Service plan toouse for hosting hello web app.</span></span>

    "hostingPlanName":{
      "type":"string"
    }

### <a name="sku"></a><span data-ttu-id="87469-113">Jednostka SKU</span><span class="sxs-lookup"><span data-stu-id="87469-113">sku</span></span>
<span data-ttu-id="87469-114">Witaj warstwę cenową dla planu hostingu hello.</span><span class="sxs-lookup"><span data-stu-id="87469-114">hello pricing tier for hello hosting plan.</span></span>

    "sku": {
      "type": "string",
      "allowedValues": [
        "F1",
        "D1",
        "B1",
        "B2",
        "B3",
        "S1",
        "S2",
        "S3",
        "P1",
        "P2",
        "P3",
        "P4"
      ],
      "defaultValue": "S1",
      "metadata": {
        "description": "hello pricing tier for hello hosting plan."
      }
    }

<span data-ttu-id="87469-115">Szablon Hello definiuje hello wartości, które są dozwolone dla tego parametru, a następnie przypisuje wartość domyślną (S1), jeśli nie określono wartości.</span><span class="sxs-lookup"><span data-stu-id="87469-115">hello template defines hello values that are permitted for this parameter, and assigns a default value (S1) if no value is specified.</span></span>

### <a name="workersize"></a><span data-ttu-id="87469-116">workerSize</span><span class="sxs-lookup"><span data-stu-id="87469-116">workerSize</span></span>
<span data-ttu-id="87469-117">rozmiar wystąpienia Hello hello planu (małych, średnich i dużych) hostingu.</span><span class="sxs-lookup"><span data-stu-id="87469-117">hello instance size of hello hosting plan (small, medium, or large).</span></span>

    "workerSize":{
      "type":"string",
      "allowedValues":[
        "0",
        "1",
        "2"
      ],
      "defaultValue":"0"
    }

<span data-ttu-id="87469-118">Szablon Hello definiuje hello wartości, które są dozwolone dla tego parametru (0, 1 lub 2) i przypisuje wartość domyślną (0), jeśli nie określono wartości.</span><span class="sxs-lookup"><span data-stu-id="87469-118">hello template defines hello values that are permitted for this parameter (0, 1, or 2), and assigns a default value (0) if no value is specified.</span></span> <span data-ttu-id="87469-119">wartości Hello odpowiadają toosmall, średnich i dużych.</span><span class="sxs-lookup"><span data-stu-id="87469-119">hello values correspond toosmall, medium and large.</span></span>

