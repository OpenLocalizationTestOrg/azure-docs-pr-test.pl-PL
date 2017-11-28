---
title: aaaCreate sieci wirtualnej - programu Azure PowerShell | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toocreate a wirtualnych sieci za pomocą programu PowerShell."
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
ms.openlocfilehash: 8d6e395a77f71de9f94b6304b05450e46b47544f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-using-powershell"></a><span data-ttu-id="0315e-103">Tworzenie sieci wirtualnej przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="0315e-103">Create a virtual network using PowerShell</span></span>

[!INCLUDE [virtual-networks-create-vnet-intro](../../includes/virtual-networks-create-vnet-intro-include.md)]

<span data-ttu-id="0315e-104">Platforma Azure ma dwa modele wdrażania: usługa Azure Resource Manager i wersja klasyczna.</span><span class="sxs-lookup"><span data-stu-id="0315e-104">Azure has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="0315e-105">Firma Microsoft zaleca utworzenie zasobów za pośrednictwem modelu wdrażania usługi Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="0315e-105">Microsoft recommends creating resources through hello Resource Manager deployment model.</span></span> <span data-ttu-id="0315e-106">więcej informacji o toolearn hello różnice między modelami hello dwa odczytu hello [modele wdrażania zrozumieć Azure](../azure-resource-manager/resource-manager-deployment-model.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="0315e-106">toolearn more about hello differences between hello two models, read hello [Understand Azure deployment models](../azure-resource-manager/resource-manager-deployment-model.md) article.</span></span>
 
<span data-ttu-id="0315e-107">W tym artykule opisano, jak toocreate sieci wirtualnej przez wdrożenie usługi Resource Manager hello modelu przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0315e-107">This article explains how toocreate a VNet through hello Resource Manager deployment model using PowerShell.</span></span> <span data-ttu-id="0315e-108">Możesz również utworzyć sieć wirtualną za pomocą Menedżera zasobów przy użyciu innych narzędzi lub utworzyć sieć wirtualną przy użyciu hello klasycznego modelu wdrażania, wybierając inną opcję z hello następującej listy:</span><span class="sxs-lookup"><span data-stu-id="0315e-108">You can also create a VNet through Resource Manager using other tools or create a VNet through hello classic deployment model by selecting a different option from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="0315e-109">Portal</span><span class="sxs-lookup"><span data-stu-id="0315e-109">Portal</span></span>](virtual-networks-create-vnet-arm-pportal.md)
> * [<span data-ttu-id="0315e-110">Program PowerShell</span><span class="sxs-lookup"><span data-stu-id="0315e-110">PowerShell</span></span>](virtual-networks-create-vnet-arm-ps.md)
> * [<span data-ttu-id="0315e-111">Interfejs wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="0315e-111">CLI</span></span>](virtual-networks-create-vnet-arm-cli.md)
> * [<span data-ttu-id="0315e-112">Szablon</span><span class="sxs-lookup"><span data-stu-id="0315e-112">Template</span></span>](virtual-networks-create-vnet-arm-template-click.md)
> * [<span data-ttu-id="0315e-113">Portal (klasyczny)</span><span class="sxs-lookup"><span data-stu-id="0315e-113">Portal (Classic)</span></span>](virtual-networks-create-vnet-classic-pportal.md)
> * [<span data-ttu-id="0315e-114">PowerShell (klasyczny)</span><span class="sxs-lookup"><span data-stu-id="0315e-114">PowerShell (Classic)</span></span>](virtual-networks-create-vnet-classic-netcfg-ps.md)
> * [<span data-ttu-id="0315e-115">Interfejs wiersza polecenia (klasyczny)</span><span class="sxs-lookup"><span data-stu-id="0315e-115">CLI (Classic)</span></span>](virtual-networks-create-vnet-classic-cli.md)

[!INCLUDE [virtual-networks-create-vnet-scenario-include](../../includes/virtual-networks-create-vnet-scenario-include.md)]

## <a name="create-a-virtual-network"></a><span data-ttu-id="0315e-116">Tworzenie sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="0315e-116">Create a virtual network</span></span>

<span data-ttu-id="0315e-117">toocreate przez sieć wirtualną przy użyciu programu PowerShell, pełną hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="0315e-117">toocreate a virtual network using PowerShell, complete hello following steps:</span></span>

1. <span data-ttu-id="0315e-118">Instalowanie i konfigurowanie programu Azure PowerShell, wykonując następujące kroki hello hello [jak tooInstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview) artykułu.</span><span class="sxs-lookup"><span data-stu-id="0315e-118">Install and configure Azure PowerShell, by following hello steps in hello [How tooInstall and Configure Azure PowerShell](/powershell/azure/overview) article.</span></span>

2. <span data-ttu-id="0315e-119">W razie potrzeby utwórz nową grupę zasobów, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="0315e-119">If necessary, create a new resource group, as shown below.</span></span> <span data-ttu-id="0315e-120">W tym scenariuszu, należy utworzyć grupę zasobów o nazwie *TestRG*.</span><span class="sxs-lookup"><span data-stu-id="0315e-120">For this scenario, create a resource group named *TestRG*.</span></span> <span data-ttu-id="0315e-121">Aby uzyskać więcej informacji na temat grup zasobów, zobacz temat [Omówienie usługi Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0315e-121">For more information about resource groups, visit [Azure Resource Manager Overview](../azure-resource-manager/resource-group-overview.md).</span></span>

    ```powershell   
    New-AzureRmResourceGroup -Name TestRG -Location centralus
    ```

    <span data-ttu-id="0315e-122">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="0315e-122">Expected output:</span></span>

        ResourceGroupName : TestRG
        Location          : centralus
        ProvisioningState : Succeeded
        Tags              :
        ResourceId        : /subscriptions/[Subscription Id]/resourceGroups/TestRG    
3. <span data-ttu-id="0315e-123">Tworzenie nowej sieci wirtualnej o nazwie *TestVNet*:</span><span class="sxs-lookup"><span data-stu-id="0315e-123">Create a new VNet named *TestVNet*:</span></span>

    ```powershell
    New-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet `
    -AddressPrefix 192.168.0.0/16 -Location centralus
    ```

    <span data-ttu-id="0315e-124">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="0315e-124">Expected output:</span></span>

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
4. <span data-ttu-id="0315e-125">Obiekt sieci wirtualnej hello należy przechowywać w zmiennej:</span><span class="sxs-lookup"><span data-stu-id="0315e-125">Store hello virtual network object in a variable:</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
    ```

   > [!TIP]
   > <span data-ttu-id="0315e-126">Można połączyć kroki 3 i 4, uruchamiając `$vnet = New-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet -AddressPrefix 192.168.0.0/16 -Location centralus`.</span><span class="sxs-lookup"><span data-stu-id="0315e-126">You can combine steps 3 and 4 by running `$vnet = New-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet -AddressPrefix 192.168.0.0/16 -Location centralus`.</span></span>
   > 

5. <span data-ttu-id="0315e-127">Dodawanie nowej zmiennej sieci wirtualnej podsieci toohello:</span><span class="sxs-lookup"><span data-stu-id="0315e-127">Add a subnet toohello new VNet variable:</span></span>

    ```powershell
    Add-AzureRmVirtualNetworkSubnetConfig -Name FrontEnd `
    -VirtualNetwork $vnet -AddressPrefix 192.168.1.0/24
    ```

    <span data-ttu-id="0315e-128">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="0315e-128">Expected output:</span></span>
   
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

6. <span data-ttu-id="0315e-129">Powtórz krok 5 powyżej dla każdej podsieci ma toocreate.</span><span class="sxs-lookup"><span data-stu-id="0315e-129">Repeat step 5 above for each subnet you want toocreate.</span></span> <span data-ttu-id="0315e-130">Witaj poniższe polecenie tworzy hello *zaplecza* podsieci dla scenariusza hello:</span><span class="sxs-lookup"><span data-stu-id="0315e-130">hello following command creates hello *BackEnd* subnet for hello scenario:</span></span>

    ```powershell
    Add-AzureRmVirtualNetworkSubnetConfig -Name BackEnd `
    -VirtualNetwork $vnet -AddressPrefix 192.168.2.0/24
    ```

7. <span data-ttu-id="0315e-131">Mimo że można utworzyć podsieci, istnieją one tylko w hello hello lokalnej zmiennej tooretrieve używana sieć wirtualna została utworzona w kroku 4 powyżej.</span><span class="sxs-lookup"><span data-stu-id="0315e-131">Although you create subnets, they currently only exist in hello local variable used tooretrieve hello VNet you create in step 4 above.</span></span> <span data-ttu-id="0315e-132">toosave hello zmiany tooAzure, uruchom następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="0315e-132">toosave hello changes tooAzure, run hello following command:</span></span>

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```
   
    <span data-ttu-id="0315e-133">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="0315e-133">Expected output:</span></span>
   
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

## <a name="next-steps"></a><span data-ttu-id="0315e-134">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="0315e-134">Next steps</span></span>

<span data-ttu-id="0315e-135">Dowiedz się, jak tooconnect:</span><span class="sxs-lookup"><span data-stu-id="0315e-135">Learn how tooconnect:</span></span>

- <span data-ttu-id="0315e-136">Sieć wirtualną maszyny wirtualnej (VM) tooa odczytując hello [utworzyć Maszynę wirtualną systemu Windows](../virtual-machines/virtual-machines-windows-ps-create.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="0315e-136">A virtual machine (VM) tooa virtual network by reading hello [Create a Windows VM](../virtual-machines/virtual-machines-windows-ps-create.md) article.</span></span> <span data-ttu-id="0315e-137">Zamiast tworzenia sieci wirtualnej i podsieci w krokach hello hello artykułów, możesz wybrać istniejącej sieci wirtualnej i tooconnect podsieci maszyny Wirtualnej, aby.</span><span class="sxs-lookup"><span data-stu-id="0315e-137">Instead of creating a VNet and subnet in hello steps of hello articles, you can select an existing VNet and subnet tooconnect a VM to.</span></span>
- <span data-ttu-id="0315e-138">Witaj sieci wirtualne sieci wirtualnej tooother odczytując hello [połączyć sieci wirtualnych](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="0315e-138">hello virtual network tooother virtual networks by reading hello [Connect VNets](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md) article.</span></span>
- <span data-ttu-id="0315e-139">Witaj sieci wirtualnej tooan sieci lokalnej za pomocą wirtualnej sieci prywatnej (VPN) do lokacji lub obwodu usługi expressroute.</span><span class="sxs-lookup"><span data-stu-id="0315e-139">hello virtual network tooan on-premises network using a site-to-site virtual private network (VPN) or ExpressRoute circuit.</span></span> <span data-ttu-id="0315e-140">Dowiedz się, jak odczytując hello [połączyć sieć lokalną tooan sieci wirtualnej przy użyciu sieci VPN lokacja lokacja](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) i [połączyć sieć wirtualną tooan obwodu ExpressRoute](../expressroute/expressroute-howto-linkvnet-arm.md) artykułów.</span><span class="sxs-lookup"><span data-stu-id="0315e-140">Learn how by reading hello [Connect a VNet tooan on-premises network using a site-to-site VPN](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) and [Link a VNet tooan ExpressRoute circuit](../expressroute/expressroute-howto-linkvnet-arm.md) articles.</span></span>
