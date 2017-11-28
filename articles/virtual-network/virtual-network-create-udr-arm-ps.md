---
title: "aaaControl routingu i wirtualnych urządzeń w usłudze Azure - PowerShell | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocontrol routingu i wirtualnych urządzeń przy użyciu programu PowerShell."
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
ms.openlocfilehash: b7b8717529eb2cd8b1d28b8ab9c6e21159d14882
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-user-defined-routes-udr-using-powershell"></a><span data-ttu-id="eed6f-103">Tworzenie trasy zdefiniowane przez użytkownika (przez) przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="eed6f-103">Create User-Defined Routes (UDR) using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="eed6f-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="eed6f-104">PowerShell</span></span>](virtual-network-create-udr-arm-ps.md)
> * [<span data-ttu-id="eed6f-105">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="eed6f-105">Azure CLI</span></span>](virtual-network-create-udr-arm-cli.md)
> * [<span data-ttu-id="eed6f-106">Szablon</span><span class="sxs-lookup"><span data-stu-id="eed6f-106">Template</span></span>](virtual-network-create-udr-arm-template.md)
> * [<span data-ttu-id="eed6f-107">PowerShell (klasyczny)</span><span class="sxs-lookup"><span data-stu-id="eed6f-107">PowerShell (Classic)</span></span>](virtual-network-create-udr-classic-ps.md)
> * [<span data-ttu-id="eed6f-108">Interfejs wiersza polecenia (klasyczny)</span><span class="sxs-lookup"><span data-stu-id="eed6f-108">CLI (Classic)</span></span>](virtual-network-create-udr-classic-cli.md)


[!INCLUDE [virtual-network-create-udr-intro-include.md](../../includes/virtual-network-create-udr-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="eed6f-109">Przed rozpoczęciem pracy z zasobów platformy Azure, jest ważne toounderstand, że Azure ma obecnie dwa modele wdrażania: usługi Azure Resource Manager i model klasyczny.</span><span class="sxs-lookup"><span data-stu-id="eed6f-109">Before you work with Azure resources, it's important toounderstand that Azure currently has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="eed6f-110">Przed rozpoczęciem pracy z dowolnym zasobem Azure należy zapoznać się z [modelami i narzędziami wdrażania](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="eed6f-110">Make sure you understand [deployment models and tools](../azure-resource-manager/resource-manager-deployment-model.md) before you work with any Azure resource.</span></span> <span data-ttu-id="eed6f-111">Hello dokumentację dotyczącą różnych narzędzi można wyświetlić, klikając karty hello u góry hello tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="eed6f-111">You can view hello documentation for different tools by clicking hello tabs at hello top of this article.</span></span>
>

<span data-ttu-id="eed6f-112">W tym artykule omówiono modelu wdrażania usługi Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="eed6f-112">This article covers hello Resource Manager deployment model.</span></span> <span data-ttu-id="eed6f-113">Możesz również [utworzyć Udr w hello klasycznego modelu wdrażania](virtual-network-create-udr-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="eed6f-113">You can also [create UDRs in hello classic deployment model](virtual-network-create-udr-classic-ps.md).</span></span>

[!INCLUDE [virtual-network-create-udr-scenario-include.md](../../includes/virtual-network-create-udr-scenario-include.md)]

<span data-ttu-id="eed6f-114">w powyższym scenariuszu hello na podstawie próbek Hello PowerShell poniższe polecenia oczekiwać środowisku niezłożonym już utworzone.</span><span class="sxs-lookup"><span data-stu-id="eed6f-114">hello sample PowerShell commands below expect a simple environment already created based on hello scenario above.</span></span> <span data-ttu-id="eed6f-115">Jeśli chcesz korzystać z poleceń hello toorun wyświetlaną w tym dokumencie, wdrażając najpierw utworzyć środowisko testowe hello [ten szablon](http://github.com/telmosampaio/azure-templates/tree/master/IaaS-NSG-UDR-Before), kliknij przycisk **wdrażanie tooAzure**, Zastąp hello domyślne wartości parametrów Jeśli to konieczne i wykonaj instrukcje hello hello portalu.</span><span class="sxs-lookup"><span data-stu-id="eed6f-115">If you want toorun hello commands as they are displayed in this document, first build hello test environment by deploying [this template](http://github.com/telmosampaio/azure-templates/tree/master/IaaS-NSG-UDR-Before), click **Deploy tooAzure**, replace hello default parameter values if necessary, and follow hello instructions in hello portal.</span></span>

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-hello-udr-for-hello-front-end-subnet"></a><span data-ttu-id="eed6f-116">Utwórz hello przez hello podsieci frontonu</span><span class="sxs-lookup"><span data-stu-id="eed6f-116">Create hello UDR for hello front-end subnet</span></span>
<span data-ttu-id="eed6f-117">tabeli tras hello toocreate i trasy wymagane do podsieci frontonu hello oparte na scenariuszu hello powyżej pełną hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="eed6f-117">toocreate hello route table and route needed for hello front-end subnet based on hello scenario above, complete hello following steps:</span></span>

1. <span data-ttu-id="eed6f-118">Utwórz toosend trasy używane wszystkie toohello toobe kierowany ruch kierowany toohello podsieci zaplecza (192.168.2.0/24) **FW1** urządzenie wirtualne (192.168.0.4).</span><span class="sxs-lookup"><span data-stu-id="eed6f-118">Create a route used toosend all traffic destined toohello back-end subnet (192.168.2.0/24) toobe routed toohello **FW1** virtual appliance (192.168.0.4).</span></span>

    ```powershell
    $route = New-AzureRmRouteConfig -Name RouteToBackEnd `
    -AddressPrefix 192.168.2.0/24 -NextHopType VirtualAppliance `
    -NextHopIpAddress 192.168.0.4
    ```

2. <span data-ttu-id="eed6f-119">Utwórz tabelę tras o nazwie **frontonu przez** w hello **westus** regionu zawierający hello trasy.</span><span class="sxs-lookup"><span data-stu-id="eed6f-119">Create a route table named **UDR-FrontEnd** in hello **westus** region that contains hello route.</span></span>

    ```powershell
    $routeTable = New-AzureRmRouteTable -ResourceGroupName TestRG -Location westus `
    -Name UDR-FrontEnd -Route $route
    ```

3. <span data-ttu-id="eed6f-120">Tworzenie zmiennej, która zawiera hello przypadku hello podsieci sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="eed6f-120">Create a variable that contains hello VNet where hello subnet is.</span></span> <span data-ttu-id="eed6f-121">W naszym scenariuszu hello sieci wirtualnej nosi nazwę **TestVNet**.</span><span class="sxs-lookup"><span data-stu-id="eed6f-121">In our scenario, hello VNet is named **TestVNet**.</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
    ```

4. <span data-ttu-id="eed6f-122">Tabela tras hello Skojarz utworzone powyżej toohello **frontonu** podsieci.</span><span class="sxs-lookup"><span data-stu-id="eed6f-122">Associate hello route table created above toohello **FrontEnd** subnet.</span></span>

    ```powershell
    Set-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name FrontEnd `
    -AddressPrefix 192.168.1.0/24 -RouteTable $routeTable
    ```

    > [!WARNING]
    > <span data-ttu-id="eed6f-123">Witaj dane wyjściowe polecenia hello powyżej przedstawiono hello zawartości dla obiekt konfiguracji sieci wirtualnej hello, który istnieje tylko na komputerze hello, w którym uruchomiony jest program PowerShell.</span><span class="sxs-lookup"><span data-stu-id="eed6f-123">hello output for hello command above shows hello content for hello virtual network configuration object, which only exists on hello computer where you are running PowerShell.</span></span> <span data-ttu-id="eed6f-124">Należy toorun hello **AzureVirtualNetwork zestaw** toosave polecenia cmdlet tooAzure tych ustawień.</span><span class="sxs-lookup"><span data-stu-id="eed6f-124">You need toorun hello **Set-AzureVirtualNetwork** cmdlet toosave these settings tooAzure.</span></span>
    > 

5. <span data-ttu-id="eed6f-125">Zapisz nową konfigurację podsieci hello na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="eed6f-125">Save hello new subnet configuration in Azure.</span></span>

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

    <span data-ttu-id="eed6f-126">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="eed6f-126">Expected output:</span></span>
   
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

## <a name="create-hello-udr-for-hello-back-end-subnet"></a><span data-ttu-id="eed6f-127">Utwórz hello przez hello zaplecza podsieci</span><span class="sxs-lookup"><span data-stu-id="eed6f-127">Create hello UDR for hello back-end subnet</span></span>

<span data-ttu-id="eed6f-128">tabeli tras hello toocreate i trasy wymagane do podsieci wewnętrznej hello oparta na scenariuszu hello powyżej, wykonaj poniższe kroki hello.</span><span class="sxs-lookup"><span data-stu-id="eed6f-128">toocreate hello route table and route needed for hello back-end subnet based on hello scenario above, follow hello steps below.</span></span>

1. <span data-ttu-id="eed6f-129">Utwórz toosend trasy używane wszystkie toohello toobe kierowany ruch kierowany toohello podsieci frontonu (192.168.1.0/24) **FW1** urządzenie wirtualne (192.168.0.4).</span><span class="sxs-lookup"><span data-stu-id="eed6f-129">Create a route used toosend all traffic destined toohello front-end subnet (192.168.1.0/24) toobe routed toohello **FW1** virtual appliance (192.168.0.4).</span></span>

    ```powershell
    $route = New-AzureRmRouteConfig -Name RouteToFrontEnd `
    -AddressPrefix 192.168.1.0/24 -NextHopType VirtualAppliance `
    -NextHopIpAddress 192.168.0.4
    ```

2. <span data-ttu-id="eed6f-130">Utwórz tabelę tras o nazwie **wewnętrznej bazy danych przez** w hello **uswest** regionu zawierający trasy hello utworzone powyżej.</span><span class="sxs-lookup"><span data-stu-id="eed6f-130">Create a route table named **UDR-BackEnd** in hello **uswest** region that contains hello route created above.</span></span>

    ```
    $routeTable = New-AzureRmRouteTable -ResourceGroupName TestRG -Location westus `
    -Name UDR-BackEnd -Route $route
    ```

3. <span data-ttu-id="eed6f-131">Tabela tras hello Skojarz utworzone powyżej toohello **zaplecza** podsieci.</span><span class="sxs-lookup"><span data-stu-id="eed6f-131">Associate hello route table created above toohello **BackEnd** subnet.</span></span>

    ```powershell
    Set-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name BackEnd `
    -AddressPrefix 192.168.2.0/24 -RouteTable $routeTable
    ```

4. <span data-ttu-id="eed6f-132">Zapisz nową konfigurację podsieci hello na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="eed6f-132">Save hello new subnet configuration in Azure.</span></span>

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

    <span data-ttu-id="eed6f-133">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="eed6f-133">Expected output:</span></span>
   
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

## <a name="enable-ip-forwarding-on-fw1"></a><span data-ttu-id="eed6f-134">Włącz przesyłanie dalej IP na FW1</span><span class="sxs-lookup"><span data-stu-id="eed6f-134">Enable IP forwarding on FW1</span></span>
<span data-ttu-id="eed6f-135">przesyłanie dalej IP tooenable w hello używany przez kartę Sieciową **FW1**, wykonaj poniższe kroki hello.</span><span class="sxs-lookup"><span data-stu-id="eed6f-135">tooenable IP forwarding in hello NIC used by **FW1**, follow hello steps below.</span></span>

1. <span data-ttu-id="eed6f-136">Tworzenie zmiennej, która zawiera ustawienia hello hello używane przez FW1 karty Sieciowej.</span><span class="sxs-lookup"><span data-stu-id="eed6f-136">Create a variable that contains hello settings for hello NIC used by FW1.</span></span> <span data-ttu-id="eed6f-137">W naszym scenariuszu hello kart nosi nazwę **NICFW1**.</span><span class="sxs-lookup"><span data-stu-id="eed6f-137">In our scenario, hello NIC is named **NICFW1**.</span></span>

    ```powershell
    $nicfw1 = Get-AzureRmNetworkInterface -ResourceGroupName TestRG -Name NICFW1
    ```

2. <span data-ttu-id="eed6f-138">Włącz przesyłanie dalej IP i Zapisz ustawienia karty Sieciowej hello.</span><span class="sxs-lookup"><span data-stu-id="eed6f-138">Enable IP forwarding, and save hello NIC settings.</span></span>

    ```powershell
    $nicfw1.EnableIPForwarding = 1
    Set-AzureRmNetworkInterface -NetworkInterface $nicfw1
    ```
   
    <span data-ttu-id="eed6f-139">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="eed6f-139">Expected output:</span></span>
   
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

