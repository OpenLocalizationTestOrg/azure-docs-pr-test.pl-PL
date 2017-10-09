## <a name="route-tables"></a><span data-ttu-id="5d6a5-101">Tabele tras</span><span class="sxs-lookup"><span data-stu-id="5d6a5-101">Route tables</span></span>
<span data-ttu-id="5d6a5-102">Zasoby tabeli tras zawiera toodefine tras jak przepływa ruch w ramach infrastruktury platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="5d6a5-102">Route table resources contains routes used toodefine how traffic flows within your Azure infrastructure.</span></span> <span data-ttu-id="5d6a5-103">Można użyć zdefiniowanych przez użytkownika tras (przez) toosend cały ruch z jednej podsieci tooa urządzenie wirtualne, takie jak system wykrywania zapory lub nieautoryzowanego dostępu (ID).</span><span class="sxs-lookup"><span data-stu-id="5d6a5-103">You can use user defined routes (UDR) toosend all traffic from a given subnet tooa virtual appliance, such as a firewall or intrusion detection system (IDS).</span></span> <span data-ttu-id="5d6a5-104">Możesz skojarzyć toosubnets tabeli tras.</span><span class="sxs-lookup"><span data-stu-id="5d6a5-104">You can associate a route table toosubnets.</span></span> 

<span data-ttu-id="5d6a5-105">Tabele tras zawierają hello następujące właściwości.</span><span class="sxs-lookup"><span data-stu-id="5d6a5-105">Route tables contain hello following properties.</span></span>

| <span data-ttu-id="5d6a5-106">Właściwość</span><span class="sxs-lookup"><span data-stu-id="5d6a5-106">Property</span></span> | <span data-ttu-id="5d6a5-107">Opis</span><span class="sxs-lookup"><span data-stu-id="5d6a5-107">Description</span></span> | <span data-ttu-id="5d6a5-108">Przykładowe wartości</span><span class="sxs-lookup"><span data-stu-id="5d6a5-108">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5d6a5-109">**trasy**</span><span class="sxs-lookup"><span data-stu-id="5d6a5-109">**routes**</span></span> |<span data-ttu-id="5d6a5-110">Trasy definiowane przez kolekcję użytkownika w tabeli tras hello</span><span class="sxs-lookup"><span data-stu-id="5d6a5-110">Collection of user defined routes in hello route table</span></span> |<span data-ttu-id="5d6a5-111">zobacz [trasy zdefiniowane przez użytkownika](#User-defined-routes)</span><span class="sxs-lookup"><span data-stu-id="5d6a5-111">see [user defined routes](#User-defined-routes)</span></span> |
| <span data-ttu-id="5d6a5-112">**podsieci**</span><span class="sxs-lookup"><span data-stu-id="5d6a5-112">**subnets**</span></span> |<span data-ttu-id="5d6a5-113">Kolekcja tabeli tras podsieci hello jest stosowany zbyt</span><span class="sxs-lookup"><span data-stu-id="5d6a5-113">Collection of subnets hello route table is applied too</span></span>|<span data-ttu-id="5d6a5-114">zobacz [podsieci](#Subnets)</span><span class="sxs-lookup"><span data-stu-id="5d6a5-114">see [subnets](#Subnets)</span></span> |

### <a name="user-defined-routes"></a><span data-ttu-id="5d6a5-115">Trasy zdefiniowane przez użytkownika</span><span class="sxs-lookup"><span data-stu-id="5d6a5-115">User defined routes</span></span>
<span data-ttu-id="5d6a5-116">Toospecify Udr wysyłania ruchu sieciowego, można utworzyć na podstawie jego adresu docelowego.</span><span class="sxs-lookup"><span data-stu-id="5d6a5-116">You can create UDRs toospecify where traffic should be sent to, based on its destination address.</span></span> <span data-ttu-id="5d6a5-117">Trasa można traktować jako definicji bramy domyślnej hello na podstawie adresu docelowego hello pakietów sieciowych.</span><span class="sxs-lookup"><span data-stu-id="5d6a5-117">You can think of a route as hello default gateway definition based on hello destination address of a network packet.</span></span>

<span data-ttu-id="5d6a5-118">Udr zawierają hello następujące właściwości.</span><span class="sxs-lookup"><span data-stu-id="5d6a5-118">UDRs contain hello following properties.</span></span> 

| <span data-ttu-id="5d6a5-119">Właściwość</span><span class="sxs-lookup"><span data-stu-id="5d6a5-119">Property</span></span> | <span data-ttu-id="5d6a5-120">Opis</span><span class="sxs-lookup"><span data-stu-id="5d6a5-120">Description</span></span> | <span data-ttu-id="5d6a5-121">Przykładowe wartości</span><span class="sxs-lookup"><span data-stu-id="5d6a5-121">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5d6a5-122">**addressPrefix**</span><span class="sxs-lookup"><span data-stu-id="5d6a5-122">**addressPrefix**</span></span> |<span data-ttu-id="5d6a5-123">Prefiks adresu lub pełny adres IP dla miejsca docelowego hello</span><span class="sxs-lookup"><span data-stu-id="5d6a5-123">Address prefix, or full IP address for hello destination</span></span> |<span data-ttu-id="5d6a5-124">192.168.1.0/24, 192.168.1.101</span><span class="sxs-lookup"><span data-stu-id="5d6a5-124">192.168.1.0/24, 192.168.1.101</span></span> |
| <span data-ttu-id="5d6a5-125">**Typ następnego przeskoku**</span><span class="sxs-lookup"><span data-stu-id="5d6a5-125">**nextHopType**</span></span> |<span data-ttu-id="5d6a5-126">Typu ruchu hello urządzenie zostanie wysłany</span><span class="sxs-lookup"><span data-stu-id="5d6a5-126">Type of device hello traffic will be sent too</span></span>|<span data-ttu-id="5d6a5-127">Internet VirtualAppliance, Brama sieci VPN</span><span class="sxs-lookup"><span data-stu-id="5d6a5-127">VirtualAppliance, VPN Gateway, Internet</span></span> |
| <span data-ttu-id="5d6a5-128">**adres IP następnego przeskoku**</span><span class="sxs-lookup"><span data-stu-id="5d6a5-128">**nextHopIpAddress**</span></span> |<span data-ttu-id="5d6a5-129">Adres IP następnego przeskoku hello</span><span class="sxs-lookup"><span data-stu-id="5d6a5-129">IP address for hello next hop</span></span> |<span data-ttu-id="5d6a5-130">192.168.1.4</span><span class="sxs-lookup"><span data-stu-id="5d6a5-130">192.168.1.4</span></span> |

<span data-ttu-id="5d6a5-131">Przykładowa tabela tras w formacie JSON:</span><span class="sxs-lookup"><span data-stu-id="5d6a5-131">Sample route table in JSON format:</span></span>

    {
        "name": "UDR-BackEnd",
        "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/routeTables/UDR-BackEnd",
        "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
        "type": "Microsoft.Network/routeTables",
        "location": "westus",
        "properties": {
            "provisioningState": "Succeeded",
            "routes": [
                {
                    "name": "RouteToFrontEnd",
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/routeTables/UDR-BackEnd/routes/RouteToFrontEnd",
                    "etag": "W/\"v\"",
                    "properties": {
                        "provisioningState": "Succeeded",
                        "addressPrefix": "192.168.1.0/24",
                        "nextHopType": "VirtualAppliance",
                        "nextHopIpAddress": "192.168.0.4"
                    }
                }
            ],
            "subnets": [
                {
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/BackEnd"
                }
            ]
        }
    }

### <a name="additional-resources"></a><span data-ttu-id="5d6a5-132">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="5d6a5-132">Additional resources</span></span>
* <span data-ttu-id="5d6a5-133">Uzyskaj więcej informacji [Udr](../articles/virtual-network/virtual-networks-udr-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5d6a5-133">Get more information about [UDRs](../articles/virtual-network/virtual-networks-udr-overview.md).</span></span>
* <span data-ttu-id="5d6a5-134">Witaj odczytu [dokumentacji interfejsu API REST](https://msdn.microsoft.com/library/azure/mt502549.aspx) dla tabel tras.</span><span class="sxs-lookup"><span data-stu-id="5d6a5-134">Read hello [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt502549.aspx) for route tables.</span></span>
* <span data-ttu-id="5d6a5-135">Witaj odczytu [dokumentacji interfejsu API REST](https://msdn.microsoft.com/library/azure/mt502539.aspx) dla użytkownika zdefiniowanych tras (Udr).</span><span class="sxs-lookup"><span data-stu-id="5d6a5-135">Read hello [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt502539.aspx) for user defined routes (UDRs).</span></span>

