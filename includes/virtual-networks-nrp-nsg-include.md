## <a name="network-security-group"></a><span data-ttu-id="31cda-101">Grupy zabezpieczeń sieci</span><span class="sxs-lookup"><span data-stu-id="31cda-101">Network Security Group</span></span>
<span data-ttu-id="31cda-102">Zasób NSG umożliwia tworzenie hello granicy zabezpieczeń obciążeń, implementując zezwalania i odmowy reguły.</span><span class="sxs-lookup"><span data-stu-id="31cda-102">An NSG resource enables hello creation of security boundary for workloads, by implementing allow and deny rules.</span></span> <span data-ttu-id="31cda-103">Te zasady mogą być stosowane tooa maszyny Wirtualnej karty Sieciowej i podsieci.</span><span class="sxs-lookup"><span data-stu-id="31cda-103">Such rules can be applied tooa VM, a NIC, or a subnet.</span></span>

| <span data-ttu-id="31cda-104">Właściwość</span><span class="sxs-lookup"><span data-stu-id="31cda-104">Property</span></span> | <span data-ttu-id="31cda-105">Opis</span><span class="sxs-lookup"><span data-stu-id="31cda-105">Description</span></span> | <span data-ttu-id="31cda-106">Przykładowe wartości</span><span class="sxs-lookup"><span data-stu-id="31cda-106">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="31cda-107">**podsieci**</span><span class="sxs-lookup"><span data-stu-id="31cda-107">**subnets**</span></span> |<span data-ttu-id="31cda-108">Lista hello identyfikatorów podsieci grupa NSG jest stosowana do.</span><span class="sxs-lookup"><span data-stu-id="31cda-108">List of subnet ids hello NSG is applied to.</span></span> |<span data-ttu-id="31cda-109">/Subscriptions/XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX/resourceGroups/TestRG/Providers/Microsoft.Network/virtualNetworks/TestVNet/Subnets/FrontEnd</span><span class="sxs-lookup"><span data-stu-id="31cda-109">/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd</span></span> |
| <span data-ttu-id="31cda-110">**securityRules**</span><span class="sxs-lookup"><span data-stu-id="31cda-110">**securityRules**</span></span> |<span data-ttu-id="31cda-111">Lista reguł zabezpieczeń, które tworzą hello NSG</span><span class="sxs-lookup"><span data-stu-id="31cda-111">List of security rules that make up hello NSG</span></span> |<span data-ttu-id="31cda-112">Zobacz [reguły zabezpieczeń](#Security-rule) poniżej</span><span class="sxs-lookup"><span data-stu-id="31cda-112">See [Security rule](#Security-rule) below</span></span> |
| <span data-ttu-id="31cda-113">**defaultSecurityRules**</span><span class="sxs-lookup"><span data-stu-id="31cda-113">**defaultSecurityRules**</span></span> |<span data-ttu-id="31cda-114">Lista domyślnych reguł zabezpieczeń w każdej grupy NSG</span><span class="sxs-lookup"><span data-stu-id="31cda-114">List of default security rules present in every NSG</span></span> |<span data-ttu-id="31cda-115">Zobacz [domyślne reguły zabezpieczeń](#Default-security-rules) poniżej</span><span class="sxs-lookup"><span data-stu-id="31cda-115">See [Default security rules](#Default-security-rules) below</span></span> |

* <span data-ttu-id="31cda-116">**Reguła zabezpieczeń** -grupa NSG może mieć zdefiniowano wiele reguł zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="31cda-116">**Security rule** - An NSG can have multiple security rules defined.</span></span> <span data-ttu-id="31cda-117">Każda reguła może akceptować lub odrzucać różnego rodzaju ruchu.</span><span class="sxs-lookup"><span data-stu-id="31cda-117">Each rule can allow or deny different types of traffic.</span></span>

### <a name="security-rule"></a><span data-ttu-id="31cda-118">Reguły zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="31cda-118">Security rule</span></span>
<span data-ttu-id="31cda-119">Reguła zabezpieczeń jest zasobem podrzędne grupy NSG zawierający właściwości hello poniżej.</span><span class="sxs-lookup"><span data-stu-id="31cda-119">A security rule is a child resource of an NSG containing hello properties below.</span></span>

| <span data-ttu-id="31cda-120">Właściwość</span><span class="sxs-lookup"><span data-stu-id="31cda-120">Property</span></span> | <span data-ttu-id="31cda-121">Opis</span><span class="sxs-lookup"><span data-stu-id="31cda-121">Description</span></span> | <span data-ttu-id="31cda-122">Przykładowe wartości</span><span class="sxs-lookup"><span data-stu-id="31cda-122">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="31cda-123">**Opis elementu**</span><span class="sxs-lookup"><span data-stu-id="31cda-123">**description**</span></span> |<span data-ttu-id="31cda-124">Opis reguły hello</span><span class="sxs-lookup"><span data-stu-id="31cda-124">Description for hello rule</span></span> |<span data-ttu-id="31cda-125">Zezwalaj na ruch przychodzący dla wszystkich maszyn wirtualnych w podsieci X</span><span class="sxs-lookup"><span data-stu-id="31cda-125">Allow inbound traffic for all VMs in subnet X</span></span> |
| <span data-ttu-id="31cda-126">**Protokół**</span><span class="sxs-lookup"><span data-stu-id="31cda-126">**protocol**</span></span> |<span data-ttu-id="31cda-127">Protokół toomatch hello reguły</span><span class="sxs-lookup"><span data-stu-id="31cda-127">Protocol toomatch for hello rule</span></span> |<span data-ttu-id="31cda-128">TCP, UDP lub *</span><span class="sxs-lookup"><span data-stu-id="31cda-128">TCP, UDP, or *</span></span> |
| <span data-ttu-id="31cda-129">**sourcePortRange**</span><span class="sxs-lookup"><span data-stu-id="31cda-129">**sourcePortRange**</span></span> |<span data-ttu-id="31cda-130">Toomatch zakres portu źródłowego hello reguły</span><span class="sxs-lookup"><span data-stu-id="31cda-130">Source port range toomatch for hello rule</span></span> |<span data-ttu-id="31cda-131">80, 100-200, *</span><span class="sxs-lookup"><span data-stu-id="31cda-131">80, 100-200, *</span></span> |
| <span data-ttu-id="31cda-132">**destinationPortRange**</span><span class="sxs-lookup"><span data-stu-id="31cda-132">**destinationPortRange**</span></span> |<span data-ttu-id="31cda-133">Docelowy port zakresu toomatch hello reguły</span><span class="sxs-lookup"><span data-stu-id="31cda-133">Destination port range toomatch for hello rule</span></span> |<span data-ttu-id="31cda-134">80, 100-200, *</span><span class="sxs-lookup"><span data-stu-id="31cda-134">80, 100-200, *</span></span> |
| <span data-ttu-id="31cda-135">**sourceAddressPrefix**</span><span class="sxs-lookup"><span data-stu-id="31cda-135">**sourceAddressPrefix**</span></span> |<span data-ttu-id="31cda-136">Toomatch prefiks adresu źródłowego dla reguły hello</span><span class="sxs-lookup"><span data-stu-id="31cda-136">Source address prefix toomatch for hello rule</span></span> |<span data-ttu-id="31cda-137">10.10.10.1, 10.10.10.0/24, sieć wirtualną</span><span class="sxs-lookup"><span data-stu-id="31cda-137">10.10.10.1, 10.10.10.0/24, VirtualNetwork</span></span> |
| <span data-ttu-id="31cda-138">**destinationAddressPrefix**</span><span class="sxs-lookup"><span data-stu-id="31cda-138">**destinationAddressPrefix**</span></span> |<span data-ttu-id="31cda-139">Toomatch prefiks adresu docelowego hello reguły</span><span class="sxs-lookup"><span data-stu-id="31cda-139">Destination address prefix toomatch for hello rule</span></span> |<span data-ttu-id="31cda-140">10.10.10.1, 10.10.10.0/24, sieć wirtualną</span><span class="sxs-lookup"><span data-stu-id="31cda-140">10.10.10.1, 10.10.10.0/24, VirtualNetwork</span></span> |
| <span data-ttu-id="31cda-141">**Kierunek**</span><span class="sxs-lookup"><span data-stu-id="31cda-141">**direction**</span></span> |<span data-ttu-id="31cda-142">Kierunek ruchu toomatch hello reguły</span><span class="sxs-lookup"><span data-stu-id="31cda-142">Direction of traffic toomatch for hello rule</span></span> |<span data-ttu-id="31cda-143">ruch przychodzący lub wychodzący</span><span class="sxs-lookup"><span data-stu-id="31cda-143">inbound or outbound</span></span> |
| <span data-ttu-id="31cda-144">**priorytet**</span><span class="sxs-lookup"><span data-stu-id="31cda-144">**priority**</span></span> |<span data-ttu-id="31cda-145">Priorytet reguły hello.</span><span class="sxs-lookup"><span data-stu-id="31cda-145">Priority for hello rule.</span></span> <span data-ttu-id="31cda-146">Reguły są sprawdzane według ważności, gdy reguła ma zastosowanie, żadne inne reguły są sprawdzane pod kątem dopasowania.</span><span class="sxs-lookup"><span data-stu-id="31cda-146">Rules are checked int he order of priority, once a rule applies, no more rules are tested for matching.</span></span> |<span data-ttu-id="31cda-147">10, 100, 65000</span><span class="sxs-lookup"><span data-stu-id="31cda-147">10, 100, 65000</span></span> |
| <span data-ttu-id="31cda-148">**dostęp**</span><span class="sxs-lookup"><span data-stu-id="31cda-148">**access**</span></span> |<span data-ttu-id="31cda-149">Typ tooapply dostęp, czy reguła hello</span><span class="sxs-lookup"><span data-stu-id="31cda-149">Type of access tooapply if hello rule matches</span></span> |<span data-ttu-id="31cda-150">zezwolenie lub zablokowanie</span><span class="sxs-lookup"><span data-stu-id="31cda-150">allow or deny</span></span> |

<span data-ttu-id="31cda-151">Przykład grupy NSG w formacie JSON:</span><span class="sxs-lookup"><span data-stu-id="31cda-151">Sample NSG in JSON format:</span></span>

    {
        "name": "NSG-BackEnd",
        "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-BackEnd",
        "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
        "type": "Microsoft.Network/networkSecurityGroups",
        "location": "westus",
        "tags": {
            "displayName": "NSG - Front End"
        },
        "properties": {
            "provisioningState": "Succeeded",
            "resourceGuid": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
            "securityRules": [
                {
                    "name": "rdp-rule",
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-BackEnd/securityRules/rdp-rule",
                    "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
                    "properties": {
                        "provisioningState": "Succeeded",
                        "description": "Allow RDP",
                        "protocol": "Tcp",
                        "sourcePortRange": "*",
                        "destinationPortRange": "3389",
                        "sourceAddressPrefix": "Internet",
                        "destinationAddressPrefix": "*",
                        "access": "Allow",
                        "priority": 100,
                        "direction": "Inbound"
                    }
                }
            ],
            "defaultSecurityRules": [
                { [...],
            "subnets": [
                {
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd"
                }
            ]
        }
    }

### <a name="default-security-rules"></a><span data-ttu-id="31cda-152">Domyślne reguły zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="31cda-152">Default security rules</span></span>

<span data-ttu-id="31cda-153">Reguły domyślne zabezpieczenia mają hello takie same właściwości dostępne w zasadach zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="31cda-153">Default security rules have hello same properties available in security rules.</span></span> <span data-ttu-id="31cda-154">Istnieją one tooprovide podstawowej łączności między zasoby, które mają toothem zastosować grupy NSG.</span><span class="sxs-lookup"><span data-stu-id="31cda-154">They exist tooprovide basic connectivity between resources that have NSGs applied toothem.</span></span> <span data-ttu-id="31cda-155">Upewnij się, że wiesz, jakiego [domyślne reguły zabezpieczeń](../articles/virtual-network/virtual-networks-nsg.md#default-rules) istnieje.</span><span class="sxs-lookup"><span data-stu-id="31cda-155">Make sure you know which [default security rules](../articles/virtual-network/virtual-networks-nsg.md#default-rules) exist.</span></span>

### <a name="additional-resources"></a><span data-ttu-id="31cda-156">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="31cda-156">Additional resources</span></span>
* <span data-ttu-id="31cda-157">Uzyskaj więcej informacji [grup NSG](../articles/virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="31cda-157">Get more information about [NSGs](../articles/virtual-network/virtual-networks-nsg.md).</span></span>
* <span data-ttu-id="31cda-158">Witaj odczytu [dokumentacji interfejsu API REST](https://msdn.microsoft.com/library/azure/mt163615.aspx) dla grup NSG.</span><span class="sxs-lookup"><span data-stu-id="31cda-158">Read hello [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt163615.aspx) for NSGs.</span></span>
* <span data-ttu-id="31cda-159">Witaj odczytu [dokumentacji interfejsu API REST](https://msdn.microsoft.com/library/azure/mt163580.aspx) dla reguł zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="31cda-159">Read hello [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt163580.aspx) for security rules.</span></span>
