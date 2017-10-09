## <a name="virtual-network"></a><span data-ttu-id="7c91f-101">Virtual Network</span><span class="sxs-lookup"><span data-stu-id="7c91f-101">Virtual Network</span></span>
<span data-ttu-id="7c91f-102">Zasoby sieci (VNET) i podsieci wirtualne pomoc w określeniu granicy zabezpieczeń dla obciążeń działających na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="7c91f-102">Virtual Networks (VNET) and subnets resources help define a security boundary for workloads running in Azure.</span></span> <span data-ttu-id="7c91f-103">Kolekcja przestrzeni adresów, zdefiniowany jako bloków CIDR charakteryzuje się sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="7c91f-103">A VNet is characterized by a collection of address spaces, defined as CIDR blocks.</span></span> 

> [!NOTE]
> <span data-ttu-id="7c91f-104">Administratorzy sieci znają notacji CIDR.</span><span class="sxs-lookup"><span data-stu-id="7c91f-104">Network administrators are familiar with CIDR notation.</span></span> <span data-ttu-id="7c91f-105">Jeśli nie znasz CIDR, [Dowiedz się więcej o](http://whatismyipaddress.com/cidr).</span><span class="sxs-lookup"><span data-stu-id="7c91f-105">If you are not familiar with CIDR, [learn more about it](http://whatismyipaddress.com/cidr).</span></span>
> 
> 

![Sieć wirtualną z wieloma podsieciami](./media/resource-groups-networking/Figure4.png)

<span data-ttu-id="7c91f-107">Sieci wirtualne zawierają hello następujące właściwości.</span><span class="sxs-lookup"><span data-stu-id="7c91f-107">VNets contain hello following properties.</span></span>

| <span data-ttu-id="7c91f-108">Właściwość</span><span class="sxs-lookup"><span data-stu-id="7c91f-108">Property</span></span> | <span data-ttu-id="7c91f-109">Opis</span><span class="sxs-lookup"><span data-stu-id="7c91f-109">Description</span></span> | <span data-ttu-id="7c91f-110">Przykładowe wartości</span><span class="sxs-lookup"><span data-stu-id="7c91f-110">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7c91f-111">**Element addressSpace**</span><span class="sxs-lookup"><span data-stu-id="7c91f-111">**addressSpace**</span></span> |<span data-ttu-id="7c91f-112">Kolekcja prefiksów adresów, które tworzą hello sieci wirtualnej w notacji CIDR</span><span class="sxs-lookup"><span data-stu-id="7c91f-112">Collection of address prefixes that make up hello VNet in CIDR notation</span></span> |<span data-ttu-id="7c91f-113">192.168.0.0/16</span><span class="sxs-lookup"><span data-stu-id="7c91f-113">192.168.0.0/16</span></span> |
| <span data-ttu-id="7c91f-114">**podsieci**</span><span class="sxs-lookup"><span data-stu-id="7c91f-114">**subnets**</span></span> |<span data-ttu-id="7c91f-115">Kolekcja podsieci, które tworzą hello sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="7c91f-115">Collection of subnets that make up hello VNet</span></span> |<span data-ttu-id="7c91f-116">zobacz [podsieci](#Subnets) poniżej.</span><span class="sxs-lookup"><span data-stu-id="7c91f-116">see [subnets](#Subnets) below.</span></span> |
| <span data-ttu-id="7c91f-117">**adres IP**</span><span class="sxs-lookup"><span data-stu-id="7c91f-117">**ipAddress**</span></span> |<span data-ttu-id="7c91f-118">Tooobject przypisany adres IP.</span><span class="sxs-lookup"><span data-stu-id="7c91f-118">IP address assigned tooobject.</span></span> <span data-ttu-id="7c91f-119">Jest to właściwość tylko do odczytu.</span><span class="sxs-lookup"><span data-stu-id="7c91f-119">This is a read-only property.</span></span> |<span data-ttu-id="7c91f-120">104.42.233.77</span><span class="sxs-lookup"><span data-stu-id="7c91f-120">104.42.233.77</span></span> |

### <a name="subnets"></a><span data-ttu-id="7c91f-121">Podsieci</span><span class="sxs-lookup"><span data-stu-id="7c91f-121">Subnets</span></span>
<span data-ttu-id="7c91f-122">Podsieć jest zasobem podrzędnych sieci wirtualnej i pomaga zdefiniować segmenty przestrzeni adresów w obrębie blok CIDR, przy użyciu prefiksów adresów IP.</span><span class="sxs-lookup"><span data-stu-id="7c91f-122">A subnet is a child resource of a VNet, and helps define segments of address spaces within a CIDR block, using IP address prefixes.</span></span> <span data-ttu-id="7c91f-123">Karty sieciowe mogą być dodawane toosubnets i tooVMs połączone, zapewniają łączność dla różnych obciążeń.</span><span class="sxs-lookup"><span data-stu-id="7c91f-123">NICs can be added toosubnets, and connected tooVMs, providing connectivity for various workloads.</span></span>

<span data-ttu-id="7c91f-124">Podsieci zawierają hello następujące właściwości.</span><span class="sxs-lookup"><span data-stu-id="7c91f-124">Subnets contain hello following properties.</span></span> 

| <span data-ttu-id="7c91f-125">Właściwość</span><span class="sxs-lookup"><span data-stu-id="7c91f-125">Property</span></span> | <span data-ttu-id="7c91f-126">Opis</span><span class="sxs-lookup"><span data-stu-id="7c91f-126">Description</span></span> | <span data-ttu-id="7c91f-127">Przykładowe wartości</span><span class="sxs-lookup"><span data-stu-id="7c91f-127">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7c91f-128">**addressPrefix**</span><span class="sxs-lookup"><span data-stu-id="7c91f-128">**addressPrefix**</span></span> |<span data-ttu-id="7c91f-129">Prefiks pojedynczy adres, który tworzą hello podsieci w notacji CIDR</span><span class="sxs-lookup"><span data-stu-id="7c91f-129">Single address prefix that make up hello subnet in CIDR notation</span></span> |<span data-ttu-id="7c91f-130">192.168.1.0/24</span><span class="sxs-lookup"><span data-stu-id="7c91f-130">192.168.1.0/24</span></span> |
| <span data-ttu-id="7c91f-131">**grupy networkSecurityGroup**</span><span class="sxs-lookup"><span data-stu-id="7c91f-131">**networkSecurityGroup**</span></span> |<span data-ttu-id="7c91f-132">Grupa NSG stosowana toohello podsieci</span><span class="sxs-lookup"><span data-stu-id="7c91f-132">NSG applied toohello subnet</span></span> |<span data-ttu-id="7c91f-133">zobacz [grupy NSG](#Network-Security-Group)</span><span class="sxs-lookup"><span data-stu-id="7c91f-133">see [NSGs](#Network-Security-Group)</span></span> |
| <span data-ttu-id="7c91f-134">**Stan**</span><span class="sxs-lookup"><span data-stu-id="7c91f-134">**routeTable**</span></span> |<span data-ttu-id="7c91f-135">Tabela tras stosowane toohello podsieci</span><span class="sxs-lookup"><span data-stu-id="7c91f-135">Route table applied toohello subnet</span></span> |<span data-ttu-id="7c91f-136">zobacz [przez](#Route-table)</span><span class="sxs-lookup"><span data-stu-id="7c91f-136">see [UDR](#Route-table)</span></span> |
| <span data-ttu-id="7c91f-137">**elementy Ipconfiguration**</span><span class="sxs-lookup"><span data-stu-id="7c91f-137">**ipConfigurations**</span></span> |<span data-ttu-id="7c91f-138">Kolekcja obiektów configruation IP używane przez karty sieciowe połączone toohello podsieci</span><span class="sxs-lookup"><span data-stu-id="7c91f-138">Collection of IP configruation objects used by NICs connected toohello subnet</span></span> |<span data-ttu-id="7c91f-139">zobacz [przez](#Route-table)</span><span class="sxs-lookup"><span data-stu-id="7c91f-139">see [UDR](#Route-table)</span></span> |

<span data-ttu-id="7c91f-140">Przykład sieci wirtualnej w formacie JSON:</span><span class="sxs-lookup"><span data-stu-id="7c91f-140">Sample VNet in JSON format:</span></span>

    {
        "name": "TestVNet",
        "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet",
        "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
        "type": "Microsoft.Network/virtualNetworks",
        "location": "westus",
        "tags": {
            "displayName": "VNet"
        },
        "properties": {
            "provisioningState": "Succeeded",
            "resourceGuid": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
            "addressSpace": {
                "addressPrefixes": [
                    "192.168.0.0/16"
                ]
            },
            "subnets": [
                {
                    "name": "FrontEnd",
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                    "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
                    "properties": {
                        "provisioningState": "Succeeded",
                        "addressPrefix": "192.168.1.0/24",
                        "networkSecurityGroup": {
                            "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-BackEnd"
                        },
                        "routeTable": {
                            "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/routeTables/UDR-FrontEnd"
                        },
                        "ipConfigurations": [
                            {
                                "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/NICWEB1/ipConfigurations/ipconfig1"
                            },
                            ...]
                    }
                },
                ...]
        }
    }

### <a name="additional-resources"></a><span data-ttu-id="7c91f-141">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="7c91f-141">Additional resources</span></span>
* <span data-ttu-id="7c91f-142">Uzyskaj więcej informacji [sieci wirtualnej](../articles/virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="7c91f-142">Get more information about [VNet](../articles/virtual-network/virtual-networks-overview.md).</span></span>
* <span data-ttu-id="7c91f-143">Witaj odczytu [dokumentacji interfejsu API REST](https://msdn.microsoft.com/library/azure/mt163650.aspx) dla sieci wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="7c91f-143">Read hello [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt163650.aspx) for VNets.</span></span>
* <span data-ttu-id="7c91f-144">Witaj odczytu [dokumentacji interfejsu API REST](https://msdn.microsoft.com/library/azure/mt163618.aspx) podsieci.</span><span class="sxs-lookup"><span data-stu-id="7c91f-144">Read hello [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt163618.aspx) for Subnets.</span></span>

