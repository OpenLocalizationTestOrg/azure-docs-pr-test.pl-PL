---
title: Tworzenie sieci wirtualnej - programu Azure PowerShell | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak utworzyć sieć wirtualną przy użyciu programu PowerShell."
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: a31f4f12-54ee-4339-b968-1a8097ca77d3
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/03/2017
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e7072ddf51570d46578111e2e392e3cbea53f2aa
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-virtual-network-using-powershell"></a><span data-ttu-id="e9345-103">Tworzenie sieci wirtualnej przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="e9345-103">Create a virtual network using PowerShell</span></span>

[!INCLUDE [virtual-networks-create-vnet-intro](../../includes/virtual-networks-create-vnet-intro-include.md)]

<span data-ttu-id="e9345-104">Platforma Azure ma dwa modele wdrażania: usługa Azure Resource Manager i wersja klasyczna.</span><span class="sxs-lookup"><span data-stu-id="e9345-104">Azure has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="e9345-105">Firma Microsoft zaleca tworzenie zasobów za pomocą modelu wdrożenia usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="e9345-105">Microsoft recommends creating resources through the Resource Manager deployment model.</span></span> <span data-ttu-id="e9345-106">Aby dowiedzieć się więcej o różnicach między dwoma modelami, zapoznaj się z artykułem [Understand Azure deployment models](../azure-resource-manager/resource-manager-deployment-model.md) (Informacje na temat modeli wdrażania platformy Azure).</span><span class="sxs-lookup"><span data-stu-id="e9345-106">To learn more about the differences between the two models, read the [Understand Azure deployment models](../azure-resource-manager/resource-manager-deployment-model.md) article.</span></span>
 
<span data-ttu-id="e9345-107">W tym artykule wyjaśniono, jak utworzyć sieć wirtualną przy użyciu modelu wdrażania usługi Resource Manager przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e9345-107">This article explains how to create a VNet through the Resource Manager deployment model using PowerShell.</span></span> <span data-ttu-id="e9345-108">Sieć wirtualną można również utworzyć w usłudze Resource Manager przy użyciu innych narzędzi albo za pośrednictwem klasycznego modelu wdrożenia, wybierając inną opcję z poniższej listy:</span><span class="sxs-lookup"><span data-stu-id="e9345-108">You can also create a VNet through Resource Manager using other tools or create a VNet through the classic deployment model by selecting a different option from the following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="e9345-109">Portal</span><span class="sxs-lookup"><span data-stu-id="e9345-109">Portal</span></span>](virtual-networks-create-vnet-arm-pportal.md)
> * [<span data-ttu-id="e9345-110">Program PowerShell</span><span class="sxs-lookup"><span data-stu-id="e9345-110">PowerShell</span></span>](virtual-networks-create-vnet-arm-ps.md)
> * [<span data-ttu-id="e9345-111">Interfejs wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="e9345-111">CLI</span></span>](virtual-networks-create-vnet-arm-cli.md)
> * [<span data-ttu-id="e9345-112">Szablon</span><span class="sxs-lookup"><span data-stu-id="e9345-112">Template</span></span>](virtual-networks-create-vnet-arm-template-click.md)
> * [<span data-ttu-id="e9345-113">Portal (klasyczny)</span><span class="sxs-lookup"><span data-stu-id="e9345-113">Portal (Classic)</span></span>](virtual-networks-create-vnet-classic-pportal.md)
> * [<span data-ttu-id="e9345-114">PowerShell (klasyczny)</span><span class="sxs-lookup"><span data-stu-id="e9345-114">PowerShell (Classic)</span></span>](virtual-networks-create-vnet-classic-netcfg-ps.md)
> * [<span data-ttu-id="e9345-115">Interfejs wiersza polecenia (klasyczny)</span><span class="sxs-lookup"><span data-stu-id="e9345-115">CLI (Classic)</span></span>](virtual-networks-create-vnet-classic-cli.md)

[!INCLUDE [virtual-networks-create-vnet-scenario-include](../../includes/virtual-networks-create-vnet-scenario-include.md)]

## <a name="create-a-virtual-network"></a><span data-ttu-id="e9345-116">Tworzenie sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="e9345-116">Create a virtual network</span></span>

<span data-ttu-id="e9345-117">Aby utworzyć sieć wirtualną przy użyciu programu PowerShell, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="e9345-117">To create a virtual network using PowerShell, complete the following steps:</span></span>

1. <span data-ttu-id="e9345-118">Instalowanie i konfigurowanie programu Azure PowerShell, wykonując kroki opisane w [Instalowanie i konfigurowanie programu Azure PowerShell](/powershell/azure/overview) artykułu.</span><span class="sxs-lookup"><span data-stu-id="e9345-118">Install and configure Azure PowerShell, by following the steps in the [How to Install and Configure Azure PowerShell](/powershell/azure/overview) article.</span></span>

2. <span data-ttu-id="e9345-119">W razie potrzeby utwórz nową grupę zasobów, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="e9345-119">If necessary, create a new resource group, as shown below.</span></span> <span data-ttu-id="e9345-120">W tym scenariuszu, należy utworzyć grupę zasobów o nazwie *TestRG*.</span><span class="sxs-lookup"><span data-stu-id="e9345-120">For this scenario, create a resource group named *TestRG*.</span></span> <span data-ttu-id="e9345-121">Aby uzyskać więcej informacji na temat grup zasobów, zobacz temat [Omówienie usługi Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e9345-121">For more information about resource groups, visit [Azure Resource Manager Overview](../azure-resource-manager/resource-group-overview.md).</span></span>

    ```powershell   
    New-AzureRmResourceGroup -Name TestRG -Location centralus
    ```

    <span data-ttu-id="e9345-122">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="e9345-122">Expected output:</span></span>

        ResourceGroupName : TestRG
        Location          : centralus
        ProvisioningState : Succeeded
        Tags              :
        ResourceId        : /subscriptions/[Subscription Id]/resourceGroups/TestRG    
3. <span data-ttu-id="e9345-123">Tworzenie nowej sieci wirtualnej o nazwie *TestVNet*:</span><span class="sxs-lookup"><span data-stu-id="e9345-123">Create a new VNet named *TestVNet*:</span></span>

    ```powershell
    New-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet `
    -AddressPrefix 192.168.0.0/16 -Location centralus
    ```

    <span data-ttu-id="e9345-124">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="e9345-124">Expected output:</span></span>

        Name                  : TestVNet
        ResourceGroupName     : TestRG
        Location              : centralus
        Id                    : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet
        Etag                   : W/"[Id]"
        ProvisioningState          : Succeeded
        Tags                       : 
        AddressSpace               : {
                                   "AddressPrefixes": [
                                     "192.168.0.0/16"
                                   ]
                                  }
        DhcpOptions                : {}
        Subnets                    : []
        VirtualNetworkPeerings     : []
4. <span data-ttu-id="e9345-125">Obiekt sieci wirtualnej można przechowywać w zmiennej:</span><span class="sxs-lookup"><span data-stu-id="e9345-125">Store the virtual network object in a variable:</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
    ```

   > [!TIP]
   > <span data-ttu-id="e9345-126">Można połączyć kroki 3 i 4, uruchamiając `$vnet = New-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet -AddressPrefix 192.168.0.0/16 -Location centralus`.</span><span class="sxs-lookup"><span data-stu-id="e9345-126">You can combine steps 3 and 4 by running `$vnet = New-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet -AddressPrefix 192.168.0.0/16 -Location centralus`.</span></span>
   > 

5. <span data-ttu-id="e9345-127">Dodaj podsieć do nowej zmiennej sieci wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="e9345-127">Add a subnet to the new VNet variable:</span></span>

    ```powershell
    Add-AzureRmVirtualNetworkSubnetConfig -Name FrontEnd `
    -VirtualNetwork $vnet -AddressPrefix 192.168.1.0/24
    ```

    <span data-ttu-id="e9345-128">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="e9345-128">Expected output:</span></span>
   
        Name                  : TestVNet
        ResourceGroupName     : TestRG
        Location              : centralus
        Id                    : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet
        Etag                  : W/"[Id]"
        ProvisioningState     : Succeeded
        Tags                  :
        AddressSpace          : {
                                  "AddressPrefixes": [
                                    "192.168.0.0/16"
                                  ]
                                }
        DhcpOptions           : {}
        Subnets             : [
                                  {
                                    "Name": "FrontEnd",
                                    "AddressPrefix": "192.168.1.0/24"
                                  }
                                ]
        VirtualNetworkPeerings     : []

6. <span data-ttu-id="e9345-129">Powtórz krok 5 opisany powyżej dla każdej podsieci, którą chcesz utworzyć.</span><span class="sxs-lookup"><span data-stu-id="e9345-129">Repeat step 5 above for each subnet you want to create.</span></span> <span data-ttu-id="e9345-130">Poniższe polecenie tworzy *zaplecza* podsieci dla tego scenariusza:</span><span class="sxs-lookup"><span data-stu-id="e9345-130">The following command creates the *BackEnd* subnet for the scenario:</span></span>

    ```powershell
    Add-AzureRmVirtualNetworkSubnetConfig -Name BackEnd `
    -VirtualNetwork $vnet -AddressPrefix 192.168.2.0/24
    ```

7. <span data-ttu-id="e9345-131">Chociaż w toku tego procesu są tworzone podsieci, to na tym etapie istnieją one tylko w zmiennej lokalnej używanej do pobierania sieci wirtualnej, która została utworzona w kroku 4.</span><span class="sxs-lookup"><span data-stu-id="e9345-131">Although you create subnets, they currently only exist in the local variable used to retrieve the VNet you create in step 4 above.</span></span> <span data-ttu-id="e9345-132">Aby zapisać zmiany na platformie Azure, uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="e9345-132">To save the changes to Azure, run the following command:</span></span>

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```
   
    <span data-ttu-id="e9345-133">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="e9345-133">Expected output:</span></span>
   
        Name                  : TestVNet
        ResourceGroupName     : TestRG
        Location              : centralus
        Id                    : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet
        Etag                  : W/"[Id]"
        ProvisioningState     : Succeeded
        Tags                  :
        AddressSpace          : {
                                  "AddressPrefixes": [
                                    "192.168.0.0/16"
                                  ]
                                }
        DhcpOptions           : {
                                  "DnsServers": []
                                }
        Subnets               : [
                                  {
                                    "Name": "FrontEnd",
                                    "Etag": "W/\"[Id]\"",
                                    "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                                    "AddressPrefix": "192.168.1.0/24",
                                    "IpConfigurations": [],
                                    "ProvisioningState": "Succeeded"
                                  },
                                  {
                                    "Name": "BackEnd",
                                    "Etag": "W/\"[Id]\"",
                                    "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/BackEnd",
                                    "AddressPrefix": "192.168.2.0/24",
                                    "IpConfigurations": [],
                                    "ProvisioningState": "Succeeded"
                                  }
                                ]
        VirtualNetworkPeerings : []

## <a name="next-steps"></a><span data-ttu-id="e9345-134">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e9345-134">Next steps</span></span>

<span data-ttu-id="e9345-135">Dowiedz się, jak połączyć:</span><span class="sxs-lookup"><span data-stu-id="e9345-135">Learn how to connect:</span></span>

- <span data-ttu-id="e9345-136">Maszyna wirtualna (VM) do sieci wirtualnej, odczytując [utworzyć Maszynę wirtualną systemu Windows](../virtual-machines/virtual-machines-windows-ps-create.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="e9345-136">A virtual machine (VM) to a virtual network by reading the [Create a Windows VM](../virtual-machines/virtual-machines-windows-ps-create.md) article.</span></span> <span data-ttu-id="e9345-137">Zamiast tworzyć sieć wirtualną i podsieć, wykonując kroki opisane w artykułach, można wybrać istniejącą sieć wirtualną i podsieć, z którymi zostanie połączona maszyna wirtualna.</span><span class="sxs-lookup"><span data-stu-id="e9345-137">Instead of creating a VNet and subnet in the steps of the articles, you can select an existing VNet and subnet to connect a VM to.</span></span>
- <span data-ttu-id="e9345-138">Sieć wirtualną z innymi sieciami wirtualnymi. Odpowiednie informacje możesz znaleźć w artykule [Łączenie sieci wirtualnych](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="e9345-138">The virtual network to other virtual networks by reading the [Connect VNets](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md) article.</span></span>
- <span data-ttu-id="e9345-139">Sieć wirtualną z siecią lokalną za pomocą prywatnej sieci wirtualnej (VPN) typu lokacja-lokacja lub obwodu usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="e9345-139">The virtual network to an on-premises network using a site-to-site virtual private network (VPN) or ExpressRoute circuit.</span></span> <span data-ttu-id="e9345-140">Odpowiednie informacje znajdziesz w artykułach [Connect a VNet to an on-premises network using a site-to-site VPN](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) (Łączenie sieci wirtualnej z siecią lokalną za pomocą sieci VPN typu lokacja-lokacja) i [Link a VNet to an ExpressRoute circuit](../expressroute/expressroute-howto-linkvnet-arm.md) (Łączenie sieci wirtualnej z obwodem usługi ExpressRoute).</span><span class="sxs-lookup"><span data-stu-id="e9345-140">Learn how by reading the [Connect a VNet to an on-premises network using a site-to-site VPN](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) and [Link a VNet to an ExpressRoute circuit](../expressroute/expressroute-howto-linkvnet-arm.md) articles.</span></span>
