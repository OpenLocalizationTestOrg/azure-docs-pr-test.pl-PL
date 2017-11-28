## <a name="virtual-network"></a><span data-ttu-id="ca0c2-101">Virtual Network</span><span class="sxs-lookup"><span data-stu-id="ca0c2-101">Virtual Network</span></span>
<span data-ttu-id="ca0c2-102">Zasoby sieci (VNET) i podsieci wirtualne pomoc w określeniu granicy zabezpieczeń dla obciążeń działających na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="ca0c2-102">Virtual Networks (VNET) and subnets resources help define a security boundary for workloads running in Azure.</span></span> <span data-ttu-id="ca0c2-103">Kolekcja przestrzeni adresów, zdefiniowany jako bloków CIDR charakteryzuje się sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ca0c2-103">A VNet is characterized by a collection of address spaces, defined as CIDR blocks.</span></span> 

> [!NOTE]
> <span data-ttu-id="ca0c2-104">Administratorzy sieci znają notacji CIDR.</span><span class="sxs-lookup"><span data-stu-id="ca0c2-104">Network administrators are familiar with CIDR notation.</span></span> <span data-ttu-id="ca0c2-105">Jeśli nie znasz CIDR, [Dowiedz się więcej o](http://whatismyipaddress.com/cidr).</span><span class="sxs-lookup"><span data-stu-id="ca0c2-105">If you are not familiar with CIDR, [learn more about it](http://whatismyipaddress.com/cidr).</span></span>
> 
> 

![Sieć wirtualną z wieloma podsieciami](./media/resource-groups-networking/Figure4.png)

<span data-ttu-id="ca0c2-107">Sieci wirtualne obejmują następujące właściwości.</span><span class="sxs-lookup"><span data-stu-id="ca0c2-107">VNets contain the following properties.</span></span>

| <span data-ttu-id="ca0c2-108">Właściwość</span><span class="sxs-lookup"><span data-stu-id="ca0c2-108">Property</span></span> | <span data-ttu-id="ca0c2-109">Opis</span><span class="sxs-lookup"><span data-stu-id="ca0c2-109">Description</span></span> | <span data-ttu-id="ca0c2-110">Przykładowe wartości</span><span class="sxs-lookup"><span data-stu-id="ca0c2-110">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ca0c2-111">**Element addressSpace**</span><span class="sxs-lookup"><span data-stu-id="ca0c2-111">**addressSpace**</span></span> |<span data-ttu-id="ca0c2-112">Kolekcja prefiksów adresów, które tworzą sieci wirtualnej w notacji CIDR</span><span class="sxs-lookup"><span data-stu-id="ca0c2-112">Collection of address prefixes that make up the VNet in CIDR notation</span></span> |<span data-ttu-id="ca0c2-113">192.168.0.0/16</span><span class="sxs-lookup"><span data-stu-id="ca0c2-113">192.168.0.0/16</span></span> |
| <span data-ttu-id="ca0c2-114">**podsieci**</span><span class="sxs-lookup"><span data-stu-id="ca0c2-114">**subnets**</span></span> |<span data-ttu-id="ca0c2-115">Kolekcja podsieci, które tworzą sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="ca0c2-115">Collection of subnets that make up the VNet</span></span> |<span data-ttu-id="ca0c2-116">zobacz [podsieci](#Subnets) poniżej.</span><span class="sxs-lookup"><span data-stu-id="ca0c2-116">see [subnets](#Subnets) below.</span></span> |
| <span data-ttu-id="ca0c2-117">**adres IP**</span><span class="sxs-lookup"><span data-stu-id="ca0c2-117">**ipAddress**</span></span> |<span data-ttu-id="ca0c2-118">Adres IP przypisany do obiektu.</span><span class="sxs-lookup"><span data-stu-id="ca0c2-118">IP address assigned to object.</span></span> <span data-ttu-id="ca0c2-119">Jest to właściwość tylko do odczytu.</span><span class="sxs-lookup"><span data-stu-id="ca0c2-119">This is a read-only property.</span></span> |<span data-ttu-id="ca0c2-120">104.42.233.77</span><span class="sxs-lookup"><span data-stu-id="ca0c2-120">104.42.233.77</span></span> |

### <a name="subnets"></a><span data-ttu-id="ca0c2-121">Podsieci</span><span class="sxs-lookup"><span data-stu-id="ca0c2-121">Subnets</span></span>
<span data-ttu-id="ca0c2-122">Podsieć jest zasobem podrzędnych sieci wirtualnej i pomaga zdefiniować segmenty przestrzeni adresów w obrębie blok CIDR, przy użyciu prefiksów adresów IP.</span><span class="sxs-lookup"><span data-stu-id="ca0c2-122">A subnet is a child resource of a VNet, and helps define segments of address spaces within a CIDR block, using IP address prefixes.</span></span> <span data-ttu-id="ca0c2-123">Karty sieciowe mogą być dodawane do podsieci lub podłączone do maszyn wirtualnych, zapewniają łączność dla różnych obciążeń.</span><span class="sxs-lookup"><span data-stu-id="ca0c2-123">NICs can be added to subnets, and connected to VMs, providing connectivity for various workloads.</span></span>

<span data-ttu-id="ca0c2-124">Podsieci obejmują następujące właściwości.</span><span class="sxs-lookup"><span data-stu-id="ca0c2-124">Subnets contain the following properties.</span></span> 

| <span data-ttu-id="ca0c2-125">Właściwość</span><span class="sxs-lookup"><span data-stu-id="ca0c2-125">Property</span></span> | <span data-ttu-id="ca0c2-126">Opis</span><span class="sxs-lookup"><span data-stu-id="ca0c2-126">Description</span></span> | <span data-ttu-id="ca0c2-127">Przykładowe wartości</span><span class="sxs-lookup"><span data-stu-id="ca0c2-127">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ca0c2-128">**addressPrefix**</span><span class="sxs-lookup"><span data-stu-id="ca0c2-128">**addressPrefix**</span></span> |<span data-ttu-id="ca0c2-129">Prefiks pojedynczy adres, który tworzą podsieci w notacji CIDR</span><span class="sxs-lookup"><span data-stu-id="ca0c2-129">Single address prefix that make up the subnet in CIDR notation</span></span> |<span data-ttu-id="ca0c2-130">192.168.1.0/24</span><span class="sxs-lookup"><span data-stu-id="ca0c2-130">192.168.1.0/24</span></span> |
| <span data-ttu-id="ca0c2-131">**grupy networkSecurityGroup**</span><span class="sxs-lookup"><span data-stu-id="ca0c2-131">**networkSecurityGroup**</span></span> |<span data-ttu-id="ca0c2-132">Grupa NSG stosowana do podsieci</span><span class="sxs-lookup"><span data-stu-id="ca0c2-132">NSG applied to the subnet</span></span> |<span data-ttu-id="ca0c2-133">zobacz [grupy NSG](#Network-Security-Group)</span><span class="sxs-lookup"><span data-stu-id="ca0c2-133">see [NSGs](#Network-Security-Group)</span></span> |
| <span data-ttu-id="ca0c2-134">**Stan**</span><span class="sxs-lookup"><span data-stu-id="ca0c2-134">**routeTable**</span></span> |<span data-ttu-id="ca0c2-135">Tabela tras stosowane do podsieci</span><span class="sxs-lookup"><span data-stu-id="ca0c2-135">Route table applied to the subnet</span></span> |<span data-ttu-id="ca0c2-136">zobacz [przez](#Route-table)</span><span class="sxs-lookup"><span data-stu-id="ca0c2-136">see [UDR](#Route-table)</span></span> |
| <span data-ttu-id="ca0c2-137">**elementy Ipconfiguration**</span><span class="sxs-lookup"><span data-stu-id="ca0c2-137">**ipConfigurations**</span></span> |<span data-ttu-id="ca0c2-138">Kolekcja obiektów configruation IP używane przez karty sieciowe podłączone do podsieci</span><span class="sxs-lookup"><span data-stu-id="ca0c2-138">Collection of IP configruation objects used by NICs connected to the subnet</span></span> |<span data-ttu-id="ca0c2-139">zobacz [przez](#Route-table)</span><span class="sxs-lookup"><span data-stu-id="ca0c2-139">see [UDR](#Route-table)</span></span> |

<span data-ttu-id="ca0c2-140">Przykład sieci wirtualnej w formacie JSON:</span><span class="sxs-lookup"><span data-stu-id="ca0c2-140">Sample VNet in JSON format:</span></span>

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

### <a name="additional-resources"></a><span data-ttu-id="ca0c2-141">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="ca0c2-141">Additional resources</span></span>
* <span data-ttu-id="ca0c2-142">Uzyskaj więcej informacji [sieci wirtualnej](../articles/virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ca0c2-142">Get more information about [VNet](../articles/virtual-network/virtual-networks-overview.md).</span></span>
* <span data-ttu-id="ca0c2-143">Odczyt [dokumentacji interfejsu API REST](https://msdn.microsoft.com/library/azure/mt163650.aspx) dla sieci wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="ca0c2-143">Read the [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt163650.aspx) for VNets.</span></span>
* <span data-ttu-id="ca0c2-144">Odczyt [dokumentacji interfejsu API REST](https://msdn.microsoft.com/library/azure/mt163618.aspx) podsieci.</span><span class="sxs-lookup"><span data-stu-id="ca0c2-144">Read the [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt163618.aspx) for Subnets.</span></span>

