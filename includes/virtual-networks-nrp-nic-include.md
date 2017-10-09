## <a name="nic"></a><span data-ttu-id="94c37-101">KARTA SIECIOWA</span><span class="sxs-lookup"><span data-stu-id="94c37-101">NIC</span></span>
<span data-ttu-id="94c37-102">Karta sieciowa zasobu interfejsu sieciowego zapewnia istniejącą podsieć tooan łączności sieciowej w zasobie sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="94c37-102">A network interface card (NIC) resource provides network connectivity tooan existing subnet in a VNet resource.</span></span> <span data-ttu-id="94c37-103">Mimo że można tworzyć karty Sieciowej jako obiekt autonomiczny, należy tooassociate go tooactually obiektu tooanother zapewnić łączność.</span><span class="sxs-lookup"><span data-stu-id="94c37-103">Although you can create a NIC as a stand alone object, you need tooassociate it tooanother object tooactually provide connectivity.</span></span> <span data-ttu-id="94c37-104">Karta sieciowa może być używane tooconnect tooa podsieć maszyny Wirtualnej, publiczny adres IP lub równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="94c37-104">A NIC can be used tooconnect a VM tooa subnet, a public IP address, or a load balancer.</span></span>  

| <span data-ttu-id="94c37-105">Właściwość</span><span class="sxs-lookup"><span data-stu-id="94c37-105">Property</span></span> | <span data-ttu-id="94c37-106">Opis</span><span class="sxs-lookup"><span data-stu-id="94c37-106">Description</span></span> | <span data-ttu-id="94c37-107">Przykładowe wartości</span><span class="sxs-lookup"><span data-stu-id="94c37-107">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="94c37-108">**maszyny wirtualnej**</span><span class="sxs-lookup"><span data-stu-id="94c37-108">**virtualMachine**</span></span> |<span data-ttu-id="94c37-109">Witaj wirtualna karta sieciowa jest skojarzony.</span><span class="sxs-lookup"><span data-stu-id="94c37-109">VM hello NIC is associated with.</span></span> |<span data-ttu-id="94c37-110">/Subscriptions/{GUID}/../microsoft.COMPUTE/virtualMachines/vm1</span><span class="sxs-lookup"><span data-stu-id="94c37-110">/subscriptions/{guid}/../Microsoft.Compute/virtualMachines/vm1</span></span> |
| <span data-ttu-id="94c37-111">**macAddress**</span><span class="sxs-lookup"><span data-stu-id="94c37-111">**macAddress**</span></span> |<span data-ttu-id="94c37-112">Adres MAC dla hello karty Sieciowej</span><span class="sxs-lookup"><span data-stu-id="94c37-112">MAC address for hello NIC</span></span> |<span data-ttu-id="94c37-113">dowolna wartość od 4 do 30</span><span class="sxs-lookup"><span data-stu-id="94c37-113">any value between 4 and 30</span></span> |
| <span data-ttu-id="94c37-114">**grupy networkSecurityGroup**</span><span class="sxs-lookup"><span data-stu-id="94c37-114">**networkSecurityGroup**</span></span> |<span data-ttu-id="94c37-115">Grupy NSG skojarzonej toohello karty Sieciowej</span><span class="sxs-lookup"><span data-stu-id="94c37-115">NSG associated toohello NIC</span></span> |<span data-ttu-id="94c37-116">/Subscriptions/{GUID}/../microsoft.Network/networkSecurityGroups/myNSG1</span><span class="sxs-lookup"><span data-stu-id="94c37-116">/subscriptions/{guid}/../Microsoft.Network/networkSecurityGroups/myNSG1</span></span> |
| <span data-ttu-id="94c37-117">**dnsSettings**</span><span class="sxs-lookup"><span data-stu-id="94c37-117">**dnsSettings**</span></span> |<span data-ttu-id="94c37-118">Ustawienia DNS dla hello karty Sieciowej</span><span class="sxs-lookup"><span data-stu-id="94c37-118">DNS settings for hello NIC</span></span> |<span data-ttu-id="94c37-119">zobacz [PIP](#Public-IP-address)</span><span class="sxs-lookup"><span data-stu-id="94c37-119">see [PIP](#Public-IP-address)</span></span> |

<span data-ttu-id="94c37-120">Karty sieciowej lub karty Sieciowej, reprezentuje interfejs sieciowy, który może być skojarzony tooa maszyny wirtualnej (VM).</span><span class="sxs-lookup"><span data-stu-id="94c37-120">A Network Interface Card, or NIC, represents a network interface that can be associated tooa virtual machine (VM).</span></span> <span data-ttu-id="94c37-121">Maszyna wirtualna może mieć jeden lub więcej kart sieciowych.</span><span class="sxs-lookup"><span data-stu-id="94c37-121">A VM can have one or more NICs.</span></span>

![Karty Sieciowej na jednej maszynie Wirtualnej](./media/resource-groups-networking/Figure3.png)

### <a name="ip-configurations"></a><span data-ttu-id="94c37-123">Konfiguracje adresów IP</span><span class="sxs-lookup"><span data-stu-id="94c37-123">IP configurations</span></span>
<span data-ttu-id="94c37-124">Karty sieciowe mają obiektu podrzędnego o nazwie **Ipconfiguration** zawierający hello następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="94c37-124">NICs have a child object named **ipConfigurations** containing hello following properties:</span></span>

| <span data-ttu-id="94c37-125">Właściwość</span><span class="sxs-lookup"><span data-stu-id="94c37-125">Property</span></span> | <span data-ttu-id="94c37-126">Opis</span><span class="sxs-lookup"><span data-stu-id="94c37-126">Description</span></span> | <span data-ttu-id="94c37-127">Przykładowe wartości</span><span class="sxs-lookup"><span data-stu-id="94c37-127">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="94c37-128">**podsieci**</span><span class="sxs-lookup"><span data-stu-id="94c37-128">**subnet**</span></span> |<span data-ttu-id="94c37-129">Witaj podsieci karty Sieciowej jest onnected do.</span><span class="sxs-lookup"><span data-stu-id="94c37-129">Subnet hello NIC is onnected to.</span></span> |<span data-ttu-id="94c37-130">/Subscriptions/{GUID}/../microsoft.Network/virtualNetworks/myvnet1/Subnets/mysub1</span><span class="sxs-lookup"><span data-stu-id="94c37-130">/subscriptions/{guid}/../Microsoft.Network/virtualNetworks/myvnet1/subnets/mysub1</span></span> |
| <span data-ttu-id="94c37-131">**elementu privateIPAddress**</span><span class="sxs-lookup"><span data-stu-id="94c37-131">**privateIPAddress**</span></span> |<span data-ttu-id="94c37-132">Adres IP dla hello karty Sieciowej w podsieci hello</span><span class="sxs-lookup"><span data-stu-id="94c37-132">IP address for hello NIC in hello subnet</span></span> |<span data-ttu-id="94c37-133">10.0.0.8</span><span class="sxs-lookup"><span data-stu-id="94c37-133">10.0.0.8</span></span> |
| <span data-ttu-id="94c37-134">**privateIPAllocationMethod**</span><span class="sxs-lookup"><span data-stu-id="94c37-134">**privateIPAllocationMethod**</span></span> |<span data-ttu-id="94c37-135">Metoda alokacji IP</span><span class="sxs-lookup"><span data-stu-id="94c37-135">IP allocation method</span></span> |<span data-ttu-id="94c37-136">Dynamiczne lub statyczne</span><span class="sxs-lookup"><span data-stu-id="94c37-136">Dynamic or Static</span></span> |
| <span data-ttu-id="94c37-137">**enableIPForwarding**</span><span class="sxs-lookup"><span data-stu-id="94c37-137">**enableIPForwarding**</span></span> |<span data-ttu-id="94c37-138">Czy hello kart interfejsu Sieciowego mogą być używane do routingu</span><span class="sxs-lookup"><span data-stu-id="94c37-138">Whether hello NIC can be used for routing</span></span> |<span data-ttu-id="94c37-139">wartość PRAWDA lub FAŁSZ</span><span class="sxs-lookup"><span data-stu-id="94c37-139">true or false</span></span> |
| <span data-ttu-id="94c37-140">**podstawowy**</span><span class="sxs-lookup"><span data-stu-id="94c37-140">**primary**</span></span> |<span data-ttu-id="94c37-141">Czy jest hello kart hello podstawowej karty Sieciowej hello maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="94c37-141">Whether hello NIC is hello primary NIC for hello VM</span></span> |<span data-ttu-id="94c37-142">wartość PRAWDA lub FAŁSZ</span><span class="sxs-lookup"><span data-stu-id="94c37-142">true or false</span></span> |
| <span data-ttu-id="94c37-143">**publicznego adresu IP**</span><span class="sxs-lookup"><span data-stu-id="94c37-143">**publicIPAddress**</span></span> |<span data-ttu-id="94c37-144">PIP skojarzone z hello karty Sieciowej</span><span class="sxs-lookup"><span data-stu-id="94c37-144">PIP associated with hello NIC</span></span> |<span data-ttu-id="94c37-145">zobacz [ustawienia DNS](#DNS-settings)</span><span class="sxs-lookup"><span data-stu-id="94c37-145">see [DNS Settings](#DNS-settings)</span></span> |
| <span data-ttu-id="94c37-146">**Loadbalancerbackendaddresspool**</span><span class="sxs-lookup"><span data-stu-id="94c37-146">**loadBalancerBackendAddressPools**</span></span> |<span data-ttu-id="94c37-147">Końcowy adres pule hello kart interfejsu Sieciowego jest skojarzony z kopii</span><span class="sxs-lookup"><span data-stu-id="94c37-147">Back end address pools hello NIC is associated with</span></span> | |
| <span data-ttu-id="94c37-148">**Dodatkowe**</span><span class="sxs-lookup"><span data-stu-id="94c37-148">**loadBalancerInboundNatRules**</span></span> |<span data-ttu-id="94c37-149">Liczba przychodzących hello reguły translatora adresów Sieciowych usługi równoważenia obciążenia, karty Sieciowej jest skojarzony z</span><span class="sxs-lookup"><span data-stu-id="94c37-149">Inbound load balancer NAT rules hello NIC is associated with</span></span> | |

<span data-ttu-id="94c37-150">Przykładowe publicznego adresu IP w formacie JSON:</span><span class="sxs-lookup"><span data-stu-id="94c37-150">Sample public IP address in JSON format:</span></span>

    {
        "name": "lb-nic1-be",
        "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/nrprg/providers/Microsoft.Network/networkInterfaces/lb-nic1-be",
        "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
        "type": "Microsoft.Network/networkInterfaces",
        "location": "eastus",
        "properties": {
            "provisioningState": "Succeeded",
            "resourceGuid": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
            "ipConfigurations": [
                {
                    "name": "NIC-config",
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/nrprg/providers/Microsoft.Network/networkInterfaces/lb-nic1-be/ipConfigurations/NIC-config",
                    "etag": "W/\"0027f1a2-3ac8-49de-b5d5-fd46550500b1\"",
                    "properties": {
                        "provisioningState": "Succeeded",
                        "privateIPAddress": "10.0.0.4",
                        "privateIPAllocationMethod": "Dynamic",
                        "subnet": {
                            "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/NRPRG/providers/Microsoft.Network/virtualNetworks/NRPVnet/subnets/NRPVnetSubnet"
                        },
                        "loadBalancerBackendAddressPools": [
                            {
                                "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/NRPbackendpool"
                            }
                        ],
                        "loadBalancerInboundNatRules": [
                            {
                                "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp1"
                            }
                        ]
                    }
                }
            ],
            "dnsSettings": { ... },
            "macAddress": "00-0D-3A-10-F1-29",
            "enableIPForwarding": false,
            "primary": true,
            "virtualMachine": {
                "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/nrprg/providers/Microsoft.Compute/virtualMachines/web1"
            }
        }
    }

### <a name="additional-resources"></a><span data-ttu-id="94c37-151">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="94c37-151">Additional resources</span></span>
* <span data-ttu-id="94c37-152">Witaj odczytu [dokumentacji interfejsu API REST](https://msdn.microsoft.com/library/azure/mt163579.aspx) dla kart sieciowych.</span><span class="sxs-lookup"><span data-stu-id="94c37-152">Read hello [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt163579.aspx) for NICs.</span></span>

