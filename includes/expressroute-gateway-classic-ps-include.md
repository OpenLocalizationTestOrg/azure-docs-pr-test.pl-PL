<span data-ttu-id="ae84d-101">Należy utworzyć sieć wirtualną i podsieć bramy, przed rozpoczęciem pracy hello następujące zadania.</span><span class="sxs-lookup"><span data-stu-id="ae84d-101">You must create a VNet and a gateway subnet first, before working on hello following tasks.</span></span> <span data-ttu-id="ae84d-102">Zobacz artykuł hello [skonfigurować sieć wirtualną przy użyciu klasycznego portalu hello](../articles/expressroute/expressroute-howto-vnet-portal-classic.md) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="ae84d-102">See hello article [Configure a Virtual Network using hello classic portal](../articles/expressroute/expressroute-howto-vnet-portal-classic.md) for more information.</span></span>   

## <a name="add-a-gateway"></a><span data-ttu-id="ae84d-103">Dodaj bramę</span><span class="sxs-lookup"><span data-stu-id="ae84d-103">Add a gateway</span></span>
<span data-ttu-id="ae84d-104">Polecenie hello poniżej toocreate bramy.</span><span class="sxs-lookup"><span data-stu-id="ae84d-104">Use hello command below toocreate a gateway.</span></span> <span data-ttu-id="ae84d-105">Można toosubstitute się, że wszystkie własne wartości.</span><span class="sxs-lookup"><span data-stu-id="ae84d-105">Be sure toosubstitute any values for your own.</span></span>

    New-AzureVirtualNetworkGateway -VNetName "MyAzureVNET" -GatewayName "ERGateway" -GatewayType Dedicated -GatewaySKU  Standard

## <a name="verify-hello-gateway-was-created"></a><span data-ttu-id="ae84d-106">Sprawdź, czy utworzono bramę hello</span><span class="sxs-lookup"><span data-stu-id="ae84d-106">Verify hello gateway was created</span></span>
<span data-ttu-id="ae84d-107">Użyj polecenia hello poniżej tooverify, który hello bramy został utworzony.</span><span class="sxs-lookup"><span data-stu-id="ae84d-107">Use hello command below tooverify that hello gateway has been created.</span></span> <span data-ttu-id="ae84d-108">To polecenie pobiera również hello identyfikator bramy, który należy innych operacji.</span><span class="sxs-lookup"><span data-stu-id="ae84d-108">This command also retrieves hello gateway ID, which you need for other operations.</span></span>

    Get-AzureVirtualNetworkGateway

## <a name="resize-a-gateway"></a><span data-ttu-id="ae84d-109">Zmień rozmiar bramy</span><span class="sxs-lookup"><span data-stu-id="ae84d-109">Resize a gateway</span></span>
<span data-ttu-id="ae84d-110">Istnieje szereg [jednostki SKU bramy](../articles/expressroute/expressroute-about-virtual-network-gateways.md).</span><span class="sxs-lookup"><span data-stu-id="ae84d-110">There are a number of [Gateway SKUs](../articles/expressroute/expressroute-about-virtual-network-gateways.md).</span></span> <span data-ttu-id="ae84d-111">Możesz użyć hello następujące polecenia toochange hello jednostka SKU bramy w dowolnym momencie.</span><span class="sxs-lookup"><span data-stu-id="ae84d-111">You can use hello following command toochange hello Gateway SKU at any time.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ae84d-112">To polecenie nie działa dla UltraPerformance bramy.</span><span class="sxs-lookup"><span data-stu-id="ae84d-112">This command doesn't work for UltraPerformance gateway.</span></span> <span data-ttu-id="ae84d-113">toochange bramy UltraPerformance tooan bramy, najpierw usuń hello istniejącą bramę usługi ExpressRoute, a następnie utwórz nową bramę UltraPerformance.</span><span class="sxs-lookup"><span data-stu-id="ae84d-113">toochange your gateway tooan UltraPerformance gateway, first remove hello existing ExpressRoute gateway, and then create a new UltraPerformance gateway.</span></span> <span data-ttu-id="ae84d-114">najpierw usuń toodowngrade bramy sieci z bramy UltraPerformance hello UltraPerformance bramy, a następnie utwórz nową bramę.</span><span class="sxs-lookup"><span data-stu-id="ae84d-114">toodowngrade your gateway from an UltraPerformance gateway, first remove hello UltraPerformance gateway, and then create a new gateway.</span></span> 
> 
> 

    Resize-AzureVirtualNetworkGateway -GatewayId <Gateway ID> -GatewaySKU HighPerformance

## <a name="remove-a-gateway"></a><span data-ttu-id="ae84d-115">Usuń bramę</span><span class="sxs-lookup"><span data-stu-id="ae84d-115">Remove a gateway</span></span>
<span data-ttu-id="ae84d-116">Użyj polecenia hello poniżej tooremove bramy</span><span class="sxs-lookup"><span data-stu-id="ae84d-116">Use hello command below tooremove a gateway</span></span>

    Remove-AzureVirtualNetworkGateway -GatewayId <Gateway ID>