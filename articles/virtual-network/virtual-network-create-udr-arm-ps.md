---
title: "Kontrolowanie routingu i wirtualnych urządzeń w usłudze Azure - PowerShell | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie kontrolowania routingu i wirtualnych urządzeń przy użyciu programu PowerShell."
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: 
tags: azure-resource-manager
ms.assetid: 9582fdaa-249c-4c98-9618-8c30d496940f
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/23/2016
ms.author: jdial
ms.openlocfilehash: 3ab24f193c74449ae7414b4ea0675c0aae0211f4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-user-defined-routes-udr-using-powershell"></a><span data-ttu-id="e1861-103">Tworzenie trasy zdefiniowane przez użytkownika (przez) przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="e1861-103">Create User-Defined Routes (UDR) using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="e1861-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e1861-104">PowerShell</span></span>](virtual-network-create-udr-arm-ps.md)
> * [<span data-ttu-id="e1861-105">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="e1861-105">Azure CLI</span></span>](virtual-network-create-udr-arm-cli.md)
> * [<span data-ttu-id="e1861-106">Szablon</span><span class="sxs-lookup"><span data-stu-id="e1861-106">Template</span></span>](virtual-network-create-udr-arm-template.md)
> * [<span data-ttu-id="e1861-107">PowerShell (klasyczny)</span><span class="sxs-lookup"><span data-stu-id="e1861-107">PowerShell (Classic)</span></span>](virtual-network-create-udr-classic-ps.md)
> * [<span data-ttu-id="e1861-108">Interfejs wiersza polecenia (klasyczny)</span><span class="sxs-lookup"><span data-stu-id="e1861-108">CLI (Classic)</span></span>](virtual-network-create-udr-classic-cli.md)


[!INCLUDE [virtual-network-create-udr-intro-include.md](../../includes/virtual-network-create-udr-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="e1861-109">Przed rozpoczęciem pracy z zasobami platformy Azure należy pamiętać, że ma ona obecnie dwa modele wdrażania: za pomocą usługi Azure Resource Manager i model klasyczny.</span><span class="sxs-lookup"><span data-stu-id="e1861-109">Before you work with Azure resources, it's important to understand that Azure currently has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="e1861-110">Przed rozpoczęciem pracy z dowolnym zasobem Azure należy zapoznać się z [modelami i narzędziami wdrażania](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="e1861-110">Make sure you understand [deployment models and tools](../azure-resource-manager/resource-manager-deployment-model.md) before you work with any Azure resource.</span></span> <span data-ttu-id="e1861-111">Dokumentację dotyczącą różnych narzędzi można wyświetlić, klikając karty w górnej części artykułu.</span><span class="sxs-lookup"><span data-stu-id="e1861-111">You can view the documentation for different tools by clicking the tabs at the top of this article.</span></span>
>

<span data-ttu-id="e1861-112">W tym artykule opisano model wdrażania usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="e1861-112">This article covers the Resource Manager deployment model.</span></span> <span data-ttu-id="e1861-113">Możesz również [utworzyć Udr w klasycznym modelu wdrażania](virtual-network-create-udr-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="e1861-113">You can also [create UDRs in the classic deployment model](virtual-network-create-udr-classic-ps.md).</span></span>

[!INCLUDE [virtual-network-create-udr-scenario-include.md](../../includes/virtual-network-create-udr-scenario-include.md)]

<span data-ttu-id="e1861-114">W powyższym scenariuszu na podstawie próbek PowerShell poniższe polecenia oczekiwać środowisku niezłożonym już utworzone.</span><span class="sxs-lookup"><span data-stu-id="e1861-114">The sample PowerShell commands below expect a simple environment already created based on the scenario above.</span></span> <span data-ttu-id="e1861-115">Jeśli chcesz uruchomić polecenia wyświetlaną w tym dokumencie, wdrażając najpierw utworzyć środowisko testowe [ten szablon](http://github.com/telmosampaio/azure-templates/tree/master/IaaS-NSG-UDR-Before), kliknij przycisk **wdrażanie na platformie Azure**, Zastąp domyślne wartości parametrów, jeśli to konieczne i postępuj zgodnie z instrukcjami w portalu.</span><span class="sxs-lookup"><span data-stu-id="e1861-115">If you want to run the commands as they are displayed in this document, first build the test environment by deploying [this template](http://github.com/telmosampaio/azure-templates/tree/master/IaaS-NSG-UDR-Before), click **Deploy to Azure**, replace the default parameter values if necessary, and follow the instructions in the portal.</span></span>

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-the-udr-for-the-front-end-subnet"></a><span data-ttu-id="e1861-116">Utwórz przez podsieci frontonu</span><span class="sxs-lookup"><span data-stu-id="e1861-116">Create the UDR for the front-end subnet</span></span>
<span data-ttu-id="e1861-117">Aby utworzyć tabelę tras i trasy wymagane dla podsieci frontonu, oparta na scenariuszu powyżej, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="e1861-117">To create the route table and route needed for the front-end subnet based on the scenario above, complete the following steps:</span></span>

1. <span data-ttu-id="e1861-118">Tworzenie trasy używana do wysyłania całego ruchu kierowanego do podsieci zaplecza (192.168.2.0/24), które mają być kierowane do **FW1** urządzenie wirtualne (192.168.0.4).</span><span class="sxs-lookup"><span data-stu-id="e1861-118">Create a route used to send all traffic destined to the back-end subnet (192.168.2.0/24) to be routed to the **FW1** virtual appliance (192.168.0.4).</span></span>

    ```powershell
    $route = New-AzureRmRouteConfig -Name RouteToBackEnd `
    -AddressPrefix 192.168.2.0/24 -NextHopType VirtualAppliance `
    -NextHopIpAddress 192.168.0.4
    ```

2. <span data-ttu-id="e1861-119">Utwórz tabelę tras o nazwie **frontonu przez** w **westus** regionu zawierający trasy.</span><span class="sxs-lookup"><span data-stu-id="e1861-119">Create a route table named **UDR-FrontEnd** in the **westus** region that contains the route.</span></span>

    ```powershell
    $routeTable = New-AzureRmRouteTable -ResourceGroupName TestRG -Location westus `
    -Name UDR-FrontEnd -Route $route
    ```

3. <span data-ttu-id="e1861-120">Tworzenie zmiennej, która zawiera przypadku podsieć sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e1861-120">Create a variable that contains the VNet where the subnet is.</span></span> <span data-ttu-id="e1861-121">W naszym scenariuszu sieci wirtualnej o nazwie **TestVNet**.</span><span class="sxs-lookup"><span data-stu-id="e1861-121">In our scenario, the VNet is named **TestVNet**.</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
    ```

4. <span data-ttu-id="e1861-122">Skojarz utworzone powyżej do tabeli tras **frontonu** podsieci.</span><span class="sxs-lookup"><span data-stu-id="e1861-122">Associate the route table created above to the **FrontEnd** subnet.</span></span>

    ```powershell
    Set-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name FrontEnd `
    -AddressPrefix 192.168.1.0/24 -RouteTable $routeTable
    ```

    > [!WARNING]
    > <span data-ttu-id="e1861-123">Dane wyjściowe po wprowadzeniu powyższego polecenia zawiera zawartość dla obiekt konfiguracji sieci wirtualnej, który istnieje tylko na komputerze, na którym uruchomiony jest program PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e1861-123">The output for the command above shows the content for the virtual network configuration object, which only exists on the computer where you are running PowerShell.</span></span> <span data-ttu-id="e1861-124">Musisz uruchomić **AzureVirtualNetwork zestaw** polecenia cmdlet, aby zapisać te ustawienia do platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="e1861-124">You need to run the **Set-AzureVirtualNetwork** cmdlet to save these settings to Azure.</span></span>
    > 

5. <span data-ttu-id="e1861-125">Zapisz nową konfigurację podsieci na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="e1861-125">Save the new subnet configuration in Azure.</span></span>

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

    <span data-ttu-id="e1861-126">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="e1861-126">Expected output:</span></span>
   
        Name              : TestVNet
        ResourceGroupName : TestRG
        Location          : westus
        Id                : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet
        Etag              : W/"[Id]"
        ProvisioningState : Succeeded
        Tags              : 
                            Name         Value
                            ===========  =====
                            displayName  VNet 
   
        AddressSpace      : {
                              "AddressPrefixes": [
                                "192.168.0.0/16"
                              ]
                            }
        DhcpOptions       : {
                              "DnsServers": null
                            }
        NetworkInterfaces : null
        Subnets           : [
                                ...,
                              {
                                "Name": "FrontEnd",
                                "Etag": "W/\"[Id]\"",
                                "Id": "/subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                                "AddressPrefix": "192.168.1.0/24",
                                "IpConfigurations": [
                                  {
                                    "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/NICWEB2/ipConfigurations/ipconfig1"
                                  },
                                  {
                                    "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/NICWEB1/ipConfigurations/ipconfig1"
                                  }
                                ],
                                "NetworkSecurityGroup": {
                                  "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd"
                                },
                                "RouteTable": {
                                  "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/routeTables/UDR-FrontEnd"
                                },
                                "ProvisioningState": "Succeeded"
                              },
                                ...
                            ]    

## <a name="create-the-udr-for-the-back-end-subnet"></a><span data-ttu-id="e1861-127">Utwórz przez podsieci wewnętrznej</span><span class="sxs-lookup"><span data-stu-id="e1861-127">Create the UDR for the back-end subnet</span></span>

<span data-ttu-id="e1861-128">Aby utworzyć tabelę tras i trasy wymagane dla podsieci zaplecza opartą na tym scenariuszu powyżej, wykonaj poniższe kroki.</span><span class="sxs-lookup"><span data-stu-id="e1861-128">To create the route table and route needed for the back-end subnet based on the scenario above, follow the steps below.</span></span>

1. <span data-ttu-id="e1861-129">Tworzenie trasy używana do wysyłania całego ruchu kierowanego do podsieci frontonu (192.168.1.0/24), aby być kierowane do **FW1** urządzenie wirtualne (192.168.0.4).</span><span class="sxs-lookup"><span data-stu-id="e1861-129">Create a route used to send all traffic destined to the front-end subnet (192.168.1.0/24) to be routed to the **FW1** virtual appliance (192.168.0.4).</span></span>

    ```powershell
    $route = New-AzureRmRouteConfig -Name RouteToFrontEnd `
    -AddressPrefix 192.168.1.0/24 -NextHopType VirtualAppliance `
    -NextHopIpAddress 192.168.0.4
    ```

2. <span data-ttu-id="e1861-130">Utwórz tabelę tras o nazwie **wewnętrznej bazy danych przez** w **uswest** regionu zawierający trasy utworzone powyżej.</span><span class="sxs-lookup"><span data-stu-id="e1861-130">Create a route table named **UDR-BackEnd** in the **uswest** region that contains the route created above.</span></span>

    ```
    $routeTable = New-AzureRmRouteTable -ResourceGroupName TestRG -Location westus `
    -Name UDR-BackEnd -Route $route
    ```

3. <span data-ttu-id="e1861-131">Skojarz utworzone powyżej do tabeli tras **zaplecza** podsieci.</span><span class="sxs-lookup"><span data-stu-id="e1861-131">Associate the route table created above to the **BackEnd** subnet.</span></span>

    ```powershell
    Set-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name BackEnd `
    -AddressPrefix 192.168.2.0/24 -RouteTable $routeTable
    ```

4. <span data-ttu-id="e1861-132">Zapisz nową konfigurację podsieci na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="e1861-132">Save the new subnet configuration in Azure.</span></span>

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

    <span data-ttu-id="e1861-133">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="e1861-133">Expected output:</span></span>
   
        Name              : TestVNet
        ResourceGroupName : TestRG
        Location          : westus
        Id                : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet
        Etag              : W/"[Id]"
        ProvisioningState : Succeeded
        Tags              : 
                            Name         Value
                            ===========  =====
                            displayName  VNet 
   
        AddressSpace      : {
                              "AddressPrefixes": [
                                "192.168.0.0/16"
                              ]
                            }
        DhcpOptions       : {
                              "DnsServers": null
                            }
        NetworkInterfaces : null
        Subnets           : [
                              ...,
                              {
                                "Name": "BackEnd",
                                "Etag": "W/\"[Id]\"",
                                "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/BackEnd",
                                "AddressPrefix": "192.168.2.0/24",
                                "IpConfigurations": [
                                  {
                                    "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/NICSQL2/ipConfigurations/ipconfig1"
                                  },
                                  {
                                    "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/NICSQL1/ipConfigurations/ipconfig1"
                                  }
                                ],
                                "NetworkSecurityGroup": {
                                  "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-BacEnd"
                                },
                                "RouteTable": {
                                  "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/routeTables/UDR-BackEnd"
                                },
                                "ProvisioningState": "Succeeded"
                              }
                            ]

## <a name="enable-ip-forwarding-on-fw1"></a><span data-ttu-id="e1861-134">Włącz przesyłanie dalej IP na FW1</span><span class="sxs-lookup"><span data-stu-id="e1861-134">Enable IP forwarding on FW1</span></span>
<span data-ttu-id="e1861-135">Aby włączyć przesyłanie dalej IP w używany przez kartę Sieciową **FW1**, wykonaj poniższe kroki.</span><span class="sxs-lookup"><span data-stu-id="e1861-135">To enable IP forwarding in the NIC used by **FW1**, follow the steps below.</span></span>

1. <span data-ttu-id="e1861-136">Tworzenie zmiennej, która zawiera ustawienia używane przez FW1 karty sieciowej.</span><span class="sxs-lookup"><span data-stu-id="e1861-136">Create a variable that contains the settings for the NIC used by FW1.</span></span> <span data-ttu-id="e1861-137">W naszym scenariuszu karty Sieciowej o nazwie **NICFW1**.</span><span class="sxs-lookup"><span data-stu-id="e1861-137">In our scenario, the NIC is named **NICFW1**.</span></span>

    ```powershell
    $nicfw1 = Get-AzureRmNetworkInterface -ResourceGroupName TestRG -Name NICFW1
    ```

2. <span data-ttu-id="e1861-138">Włącz przesyłanie dalej IP, a następnie Zapisz ustawienia karty Sieciowej.</span><span class="sxs-lookup"><span data-stu-id="e1861-138">Enable IP forwarding, and save the NIC settings.</span></span>

    ```powershell
    $nicfw1.EnableIPForwarding = 1
    Set-AzureRmNetworkInterface -NetworkInterface $nicfw1
    ```
   
    <span data-ttu-id="e1861-139">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="e1861-139">Expected output:</span></span>
   
        Name                 : NICFW1
        ResourceGroupName    : TestRG
        Location             : westus
        Id                   : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/NICFW1
        Etag                 : W/"[Id]"
        ProvisioningState    : Succeeded
        Tags                 : 
                               Name         Value                  
                               ===========  =======================
                               displayName  NetworkInterfaces - DMZ
   
        VirtualMachine       : {
                                 "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Compute/virtualMachines/FW1"
                               }
        IpConfigurations     : [
                                 {
                                   "Name": "ipconfig1",
                                   "Etag": "W/\"[Id]\"",
                                   "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/NICFW1/ipConfigurations/ipconfig1",
                                   "PrivateIpAddress": "192.168.0.4",
                                   "PrivateIpAllocationMethod": "Static",
                                   "Subnet": {
                                     "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/DMZ"
                                   },
                                   "PublicIpAddress": {
                                     "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/publicIPAddresses/PIPFW1"
                                   },
                                   "LoadBalancerBackendAddressPools": [],
                                   "LoadBalancerInboundNatRules": [],
                                   "ProvisioningState": "Succeeded"
                                 }
                               ]
        DnsSettings          : {
                                 "DnsServers": [],
                                 "AppliedDnsServers": [],
                                 "InternalDnsNameLabel": null,
                                 "InternalFqdn": null
                               }
        EnableIPForwarding   : True
        NetworkSecurityGroup : null
        Primary              : True

