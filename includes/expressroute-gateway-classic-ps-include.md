<span data-ttu-id="7aadd-101">Należy utworzyć sieć wirtualną i podsieć bramy, przed rozpoczęciem pracy poniższe zadania.</span><span class="sxs-lookup"><span data-stu-id="7aadd-101">You must create a VNet and a gateway subnet first, before working on the following tasks.</span></span> <span data-ttu-id="7aadd-102">Zapoznaj się z artykułem [Skonfiguruj sieć wirtualną przy użyciu klasycznego portalu](../articles/expressroute/expressroute-howto-vnet-portal-classic.md) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="7aadd-102">See the article [Configure a Virtual Network using the classic portal](../articles/expressroute/expressroute-howto-vnet-portal-classic.md) for more information.</span></span>   

## <a name="add-a-gateway"></a><span data-ttu-id="7aadd-103">Dodaj bramę</span><span class="sxs-lookup"><span data-stu-id="7aadd-103">Add a gateway</span></span>
<span data-ttu-id="7aadd-104">Aby utworzyć bramę, należy użyć poniższego polecenia.</span><span class="sxs-lookup"><span data-stu-id="7aadd-104">Use the command below to create a gateway.</span></span> <span data-ttu-id="7aadd-105">Należy zastąpić wszystkie własne wartości.</span><span class="sxs-lookup"><span data-stu-id="7aadd-105">Be sure to substitute any values for your own.</span></span>

    New-AzureVirtualNetworkGateway -VNetName "MyAzureVNET" -GatewayName "ERGateway" -GatewayType Dedicated -GatewaySKU  Standard

## <a name="verify-the-gateway-was-created"></a><span data-ttu-id="7aadd-106">Sprawdź, czy utworzono bramę</span><span class="sxs-lookup"><span data-stu-id="7aadd-106">Verify the gateway was created</span></span>
<span data-ttu-id="7aadd-107">Użyj poniższego polecenia, aby sprawdzić, czy utworzono bramę.</span><span class="sxs-lookup"><span data-stu-id="7aadd-107">Use the command below to verify that the gateway has been created.</span></span> <span data-ttu-id="7aadd-108">To polecenie pobiera również identyfikator bramy, który jest wymagany dla innych operacji.</span><span class="sxs-lookup"><span data-stu-id="7aadd-108">This command also retrieves the gateway ID, which you need for other operations.</span></span>

    Get-AzureVirtualNetworkGateway

## <a name="resize-a-gateway"></a><span data-ttu-id="7aadd-109">Zmień rozmiar bramy</span><span class="sxs-lookup"><span data-stu-id="7aadd-109">Resize a gateway</span></span>
<span data-ttu-id="7aadd-110">Istnieje szereg [jednostki SKU bramy](../articles/expressroute/expressroute-about-virtual-network-gateways.md).</span><span class="sxs-lookup"><span data-stu-id="7aadd-110">There are a number of [Gateway SKUs](../articles/expressroute/expressroute-about-virtual-network-gateways.md).</span></span> <span data-ttu-id="7aadd-111">Następujące polecenie służy do zmiany jednostka SKU bramy w dowolnym momencie.</span><span class="sxs-lookup"><span data-stu-id="7aadd-111">You can use the following command to change the Gateway SKU at any time.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7aadd-112">To polecenie nie działa dla UltraPerformance bramy.</span><span class="sxs-lookup"><span data-stu-id="7aadd-112">This command doesn't work for UltraPerformance gateway.</span></span> <span data-ttu-id="7aadd-113">Aby zmienić bramę do bramy UltraPerformance, najpierw usuń istniejącą bramę usługi ExpressRoute, a następnie utwórz nową bramę UltraPerformance.</span><span class="sxs-lookup"><span data-stu-id="7aadd-113">To change your gateway to an UltraPerformance gateway, first remove the existing ExpressRoute gateway, and then create a new UltraPerformance gateway.</span></span> <span data-ttu-id="7aadd-114">Na starszą wersję bramy sieci z bramy UltraPerformance, najpierw usuń UltraPerformance bramy, a następnie utwórz nową bramę.</span><span class="sxs-lookup"><span data-stu-id="7aadd-114">To downgrade your gateway from an UltraPerformance gateway, first remove the UltraPerformance gateway, and then create a new gateway.</span></span> 
> 
> 

    Resize-AzureVirtualNetworkGateway -GatewayId <Gateway ID> -GatewaySKU HighPerformance

## <a name="remove-a-gateway"></a><span data-ttu-id="7aadd-115">Usuń bramę</span><span class="sxs-lookup"><span data-stu-id="7aadd-115">Remove a gateway</span></span>
<span data-ttu-id="7aadd-116">Użyj poniższego polecenia, aby usunąć bramę</span><span class="sxs-lookup"><span data-stu-id="7aadd-116">Use the command below to remove a gateway</span></span>

    Remove-AzureVirtualNetworkGateway -GatewayId <Gateway ID>