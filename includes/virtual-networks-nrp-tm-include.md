## <a name="traffic-manager-profile"></a><span data-ttu-id="a06c9-101">Profil Menedżera ruchu</span><span class="sxs-lookup"><span data-stu-id="a06c9-101">Traffic Manager Profile</span></span>
<span data-ttu-id="a06c9-102">Menedżera ruchu i jego zasobu punktu końcowego podrzędne umożliwiają DNS tooendpoints routingu na platformie Azure i poza platformą Azure.</span><span class="sxs-lookup"><span data-stu-id="a06c9-102">Traffic manager and its child endpoint resource enable DNS routing tooendpoints in Azure and outside of Azure.</span></span> <span data-ttu-id="a06c9-103">Taki podział ruchu podlega metody zasad routingu.</span><span class="sxs-lookup"><span data-stu-id="a06c9-103">Such traffic distribution is governed by routing  policy methods.</span></span> <span data-ttu-id="a06c9-104">Menedżer ruchu umożliwia także monitorowane toobe kondycji punktu końcowego, a ruch odpowiednio kierowane oparty na powitania kondycji punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="a06c9-104">Traffic manager also allows endpoint health toobe monitored, and traffic diverted appropriately based on hello health of an endpoint.</span></span> 

| <span data-ttu-id="a06c9-105">Właściwość</span><span class="sxs-lookup"><span data-stu-id="a06c9-105">Property</span></span> | <span data-ttu-id="a06c9-106">Opis</span><span class="sxs-lookup"><span data-stu-id="a06c9-106">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a06c9-107">**trafficRoutingMethod**</span><span class="sxs-lookup"><span data-stu-id="a06c9-107">**trafficRoutingMethod**</span></span> |<span data-ttu-id="a06c9-108">Możliwe wartości to *wydajności*, *ważone*, i *priorytet*</span><span class="sxs-lookup"><span data-stu-id="a06c9-108">possible values are *Performance*, *Weighted*, and *Priority*</span></span> |
| <span data-ttu-id="a06c9-109">**dnsConfig**</span><span class="sxs-lookup"><span data-stu-id="a06c9-109">**dnsConfig**</span></span> |<span data-ttu-id="a06c9-110">Nazwa FQDN hello profilu</span><span class="sxs-lookup"><span data-stu-id="a06c9-110">FQDN for hello profile</span></span> |
| <span data-ttu-id="a06c9-111">**Protokół**</span><span class="sxs-lookup"><span data-stu-id="a06c9-111">**Protocol**</span></span> |<span data-ttu-id="a06c9-112">Protokół monitorowania, możliwe wartości to *HTTP* i *protokołu HTTPS*</span><span class="sxs-lookup"><span data-stu-id="a06c9-112">monitoring protocol, possible values are *HTTP* and *HTTPS*</span></span> |
| <span data-ttu-id="a06c9-113">**Port**</span><span class="sxs-lookup"><span data-stu-id="a06c9-113">**Port**</span></span> |<span data-ttu-id="a06c9-114">monitorowanie portu</span><span class="sxs-lookup"><span data-stu-id="a06c9-114">monitoring port</span></span> |
| <span data-ttu-id="a06c9-115">**Ścieżka**</span><span class="sxs-lookup"><span data-stu-id="a06c9-115">**Path**</span></span> |<span data-ttu-id="a06c9-116">Ścieżka monitorowania</span><span class="sxs-lookup"><span data-stu-id="a06c9-116">monitoring path</span></span> |
| <span data-ttu-id="a06c9-117">**Punkty końcowe**</span><span class="sxs-lookup"><span data-stu-id="a06c9-117">**Endpoints**</span></span> |<span data-ttu-id="a06c9-118">kontener dla punktu końcowego zasobów</span><span class="sxs-lookup"><span data-stu-id="a06c9-118">container for endpoint resources</span></span> |

### <a name="endpoint"></a><span data-ttu-id="a06c9-119">Endpoint</span><span class="sxs-lookup"><span data-stu-id="a06c9-119">Endpoint</span></span>
<span data-ttu-id="a06c9-120">Punkt końcowy jest zasobem podrzędne profil Menedżera ruchu.</span><span class="sxs-lookup"><span data-stu-id="a06c9-120">An endpoint is a child resource of a Traffic Manager Profile.</span></span> <span data-ttu-id="a06c9-121">Reprezentuje usługę lub ruchu użytkowników toowhich punktu końcowego sieci web jest dystrybuowany na podstawie zasad hello skonfigurowane w hello zasobów profilu usługi Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="a06c9-121">It represents a service or web endpoint toowhich user traffic is distributed based on hello configured policy in hello Traffic Manager Profile resource.</span></span> 

| <span data-ttu-id="a06c9-122">Właściwość</span><span class="sxs-lookup"><span data-stu-id="a06c9-122">Property</span></span> | <span data-ttu-id="a06c9-123">Opis</span><span class="sxs-lookup"><span data-stu-id="a06c9-123">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a06c9-124">**Typ**</span><span class="sxs-lookup"><span data-stu-id="a06c9-124">**Type**</span></span> |<span data-ttu-id="a06c9-125">Witaj typ punktu końcowego hello, możliwe wartości to *punktu końcowego usługi Azure*, *zewnętrznego punktu końcowego*, i *zagnieżdżone punktu końcowego*</span><span class="sxs-lookup"><span data-stu-id="a06c9-125">hello type of hello endpoint, possible values are *Azure End point*, *External Endpoint*, and  *Nested Endpoint*</span></span> |
| <span data-ttu-id="a06c9-126">**Element targetResourceId**</span><span class="sxs-lookup"><span data-stu-id="a06c9-126">**targetResourceId**</span></span> |<span data-ttu-id="a06c9-127">publiczny adres IP punktu końcowego usługi lub sieci web.</span><span class="sxs-lookup"><span data-stu-id="a06c9-127">public IP address of a service or web endpoint.</span></span> <span data-ttu-id="a06c9-128">Może to być platformy Azure lub zewnętrznego punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="a06c9-128">This can be an Azure or external endpoint.</span></span> |
| <span data-ttu-id="a06c9-129">**Waga**</span><span class="sxs-lookup"><span data-stu-id="a06c9-129">**Weight**</span></span> |<span data-ttu-id="a06c9-130">Waga punktu końcowego używane w ruchu zarządzania.</span><span class="sxs-lookup"><span data-stu-id="a06c9-130">endpoint weight used in traffic management.</span></span> |
| <span data-ttu-id="a06c9-131">**Priorytet**</span><span class="sxs-lookup"><span data-stu-id="a06c9-131">**Priority**</span></span> |<span data-ttu-id="a06c9-132">priorytet punktu końcowego hello, używane toodefine działania trybu failover</span><span class="sxs-lookup"><span data-stu-id="a06c9-132">priority of hello endpoint, used toodefine a failover action</span></span> |

<span data-ttu-id="a06c9-133">Przykład Traffic Manager w formacie Json:</span><span class="sxs-lookup"><span data-stu-id="a06c9-133">Sample of Traffic Manager in Json format:</span></span> 

        {
            "apiVersion": "[variables('tmApiVersion')]",
            "type": "Microsoft.Network/trafficManagerProfiles",
            "name": "VMEndpointExample",
            "location": "global",
            "dependsOn": [
                "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIPAddressName'), '0')]",
                "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIPAddressName'), '1')]",
                "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIPAddressName'), '2')]",
            ],
            "properties": {
                "profileStatus": "Enabled",
                "trafficRoutingMethod": "Weighted",
                "dnsConfig": {
                    "relativeName": "[parameters('dnsname')]",
                    "ttl": 30
                },
                "monitorConfig": {
                    "protocol": "http",
                    "port": 80,
                    "path": "/"
                },
                "endpoints": [
                    {
                        "name": "endpoint0",
                        "type": "Microsoft.Network/trafficManagerProfiles/azureEndpoints",
                        "properties": {
                            "targetResourceId": "[resourceId('Microsoft.Network/publicIPAddresses',concat(variables('publicIPAddressName'), 0))]",
                            "endpointStatus": "Enabled",
                            "weight": 1
                        }
                    },
                    {
                        "name": "endpoint1",
                        "type": "Microsoft.Network/trafficManagerProfiles/azureEndpoints",
                        "properties": {
                            "targetResourceId": "[resourceId('Microsoft.Network/publicIPAddresses',concat(variables('publicIPAddressName'), 1))]",
                            "endpointStatus": "Enabled",
                            "weight": 1
                        }
                    },
                    {
                        "name": "endpoint2",
                        "type": "Microsoft.Network/trafficManagerProfiles/azureEndpoints",
                        "properties": {
                            "targetResourceId": "[resourceId('Microsoft.Network/publicIPAddresses',concat(variables('publicIPAddressName'), 2))]",
                            "endpointStatus": "Enabled",
                            "weight": 1
                        }
                    }
                ]
            }
        }


## <a name="additional-resources"></a><span data-ttu-id="a06c9-134">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="a06c9-134">Additional resources</span></span>
<span data-ttu-id="a06c9-135">Odczyt [dokumentacja interfejsu API REST dla Menedżera ruchu](https://msdn.microsoft.com/library/azure/mt163664.aspx) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="a06c9-135">Read [REST API documentation for Traffic Manager](https://msdn.microsoft.com/library/azure/mt163664.aspx) for more information.</span></span>

