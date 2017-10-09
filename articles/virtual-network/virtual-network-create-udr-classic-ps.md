---
title: "aaaControl routingu w sieci wirtualnej Azure - PowerShell — Classic | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocontrol routingu w sieci wirtualnych za pomocą programu PowerShell | Classic"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: 
tags: azure-service-management
ms.assetid: d8d07c16-cbe5-4536-acd6-870269346fe3
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.openlocfilehash: 36edf263fb434d5fb13310d4324da20e57f016a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="control-routing-and-use-virtual-appliances-classic-using-powershell"></a><span data-ttu-id="36029-103">Kontrolowanie routingu i używaniu urządzeń wirtualnych (klasyczne) przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="36029-103">Control routing and use virtual appliances (classic) using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="36029-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="36029-104">PowerShell</span></span>](virtual-network-create-udr-arm-ps.md)
> * [<span data-ttu-id="36029-105">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="36029-105">Azure CLI</span></span>](virtual-network-create-udr-arm-cli.md)
> * [<span data-ttu-id="36029-106">Szablon</span><span class="sxs-lookup"><span data-stu-id="36029-106">Template</span></span>](virtual-network-create-udr-arm-template.md)
> * [<span data-ttu-id="36029-107">PowerShell (klasyczny)</span><span class="sxs-lookup"><span data-stu-id="36029-107">PowerShell (Classic)</span></span>](virtual-network-create-udr-classic-ps.md)
> * [<span data-ttu-id="36029-108">Interfejs wiersza polecenia (klasyczny)</span><span class="sxs-lookup"><span data-stu-id="36029-108">CLI (Classic)</span></span>](virtual-network-create-udr-classic-cli.md)

[!INCLUDE [virtual-network-create-udr-intro-include.md](../../includes/virtual-network-create-udr-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="36029-109">Przed rozpoczęciem pracy z zasobów platformy Azure, jest ważne toounderstand, że Azure ma obecnie dwa modele wdrażania: usługi Azure Resource Manager i model klasyczny.</span><span class="sxs-lookup"><span data-stu-id="36029-109">Before you work with Azure resources, it's important toounderstand that Azure currently has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="36029-110">Przed rozpoczęciem pracy z dowolnym zasobem Azure należy zapoznać się z [modelami i narzędziami wdrażania](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="36029-110">Make sure you understand [deployment models and tools](../azure-resource-manager/resource-manager-deployment-model.md) before you work with any Azure resource.</span></span> <span data-ttu-id="36029-111">Hello dokumentację dotyczącą różnych narzędzi można wyświetlić, wybierając opcję u góry hello w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="36029-111">You can view hello documentation for different tools by selecting an option at hello top of this article.</span></span> <span data-ttu-id="36029-112">W tym artykule omówiono hello klasycznego modelu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="36029-112">This article covers hello classic deployment model.</span></span>
> 

[!INCLUDE [virtual-network-create-udr-scenario-include.md](../../includes/virtual-network-create-udr-scenario-include.md)]

<span data-ttu-id="36029-113">w powyższym scenariuszu hello na podstawie próbek Hello programu Azure PowerShell poniższe polecenia oczekiwać środowisku niezłożonym już utworzone.</span><span class="sxs-lookup"><span data-stu-id="36029-113">hello sample Azure PowerShell commands below expect a simple environment already created based on hello scenario above.</span></span> <span data-ttu-id="36029-114">Polecenia hello toorun wyświetlaną w tym dokumencie, utworzyć środowisko hello pokazano [Utwórz sieć wirtualną (klasyczne) przy użyciu programu PowerShell](virtual-networks-create-vnet-classic-netcfg-ps.md).</span><span class="sxs-lookup"><span data-stu-id="36029-114">If you want toorun hello commands as they are displayed in this document, create hello environment shown in [create a VNet (classic) using PowerShell](virtual-networks-create-vnet-classic-netcfg-ps.md).</span></span>

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-hello-udr-for-hello-front-end-subnet"></a><span data-ttu-id="36029-115">Utwórz hello przez dla podsieci frontonu hello</span><span class="sxs-lookup"><span data-stu-id="36029-115">Create hello UDR for hello front end subnet</span></span>
<span data-ttu-id="36029-116">tabeli tras hello toocreate i trasy wymagane do podsieci frontonu hello oparta na scenariuszu hello powyżej, wykonaj poniższe kroki hello.</span><span class="sxs-lookup"><span data-stu-id="36029-116">toocreate hello route table and route needed for hello front end subnet based on hello scenario above, follow hello steps below.</span></span>

1. <span data-ttu-id="36029-117">Uruchom następujące polecenie toocreate hello tabelę tras dla podsieci frontonu hello:</span><span class="sxs-lookup"><span data-stu-id="36029-117">Run hello following command toocreate a route table for hello front-end subnet:</span></span>

    ```powershell
    New-AzureRouteTable -Name UDR-FrontEnd -Location uswest `
    -Label "Route table for front end subnet"
    ```

2. <span data-ttu-id="36029-118">Uruchom następujące polecenie toocreate trasy w toosend tabeli tras hello hello wszystkich toohello podsieci zaplecza (192.168.2.0/24) toohello ruch kierowany **FW1** maszyny Wirtualnej (192.168.0.4):</span><span class="sxs-lookup"><span data-stu-id="36029-118">Run hello following command toocreate a route in hello route table toosend all traffic destined toohello back-end subnet (192.168.2.0/24) toohello **FW1** VM (192.168.0.4):</span></span>

    ```powershell
    Get-AzureRouteTable UDR-FrontEnd `
    |Set-AzureRoute -RouteName RouteToBackEnd -AddressPrefix 192.168.2.0/24 `
    -NextHopType VirtualAppliance `
    -NextHopIpAddress 192.168.0.4
    ```

3. <span data-ttu-id="36029-119">Uruchom hello następujących tabeli tras hello tooassociate polecenie z hello **frontonu** podsieci:</span><span class="sxs-lookup"><span data-stu-id="36029-119">Run hello following command tooassociate hello route table with hello **FrontEnd** subnet:</span></span>

    ```powershell
    Set-AzureSubnetRouteTable -VirtualNetworkName TestVNet `
    -SubnetName FrontEnd `
    -RouteTableName UDR-FrontEnd
    ```

## <a name="create-hello-udr-for-hello-back-end-subnet"></a><span data-ttu-id="36029-120">Utwórz hello przez hello zaplecza podsieci</span><span class="sxs-lookup"><span data-stu-id="36029-120">Create hello UDR for hello back-end subnet</span></span>
<span data-ttu-id="36029-121">Tabela tras hello toocreate i trasy wymagane do tyłu hello kończyć podsieci oparta na scenariuszu hello, ukończyć powitalnych następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="36029-121">toocreate hello route table and route needed for hello back end subnet based on hello scenario, complete hello following steps:</span></span>

1. <span data-ttu-id="36029-122">Uruchom następujące polecenie toocreate hello tabelę tras dla podsieci wewnętrznej hello:</span><span class="sxs-lookup"><span data-stu-id="36029-122">Run hello following command toocreate a route table for hello back-end subnet:</span></span>

    ```powershell
    New-AzureRouteTable -Name UDR-BackEnd `
    -Location uswest `
    -Label "Route table for back end subnet"
    ```

2. <span data-ttu-id="36029-123">Uruchom następujące polecenia toocreate trasy w toosend tabeli tras hello hello wszystkich ruch kierowany toohello podsieci frontonu (192.168.1.0/24) toohello **FW1** maszyny Wirtualnej (192.168.0.4):</span><span class="sxs-lookup"><span data-stu-id="36029-123">Run hello following command toocreate a route in hello route table toosend all traffic destined toohello front-end subnet (192.168.1.0/24) toohello **FW1** VM (192.168.0.4):</span></span>

    ```powershell
    Get-AzureRouteTable UDR-BackEnd
    | Set-AzureRoute `
    -RouteName RouteToFrontEnd `
    -AddressPrefix 192.168.1.0/24 `
    -NextHopType VirtualAppliance `
    -NextHopIpAddress 192.168.0.4
    ```

3. <span data-ttu-id="36029-124">Uruchom hello następujących tabeli tras hello tooassociate polecenie z hello **zaplecza** podsieci:</span><span class="sxs-lookup"><span data-stu-id="36029-124">Run hello following command tooassociate hello route table with hello **BackEnd** subnet:</span></span>

    ```powershell
    Set-AzureSubnetRouteTable -VirtualNetworkName TestVNet `
    -SubnetName BackEnd `
    -RouteTableName UDR-BackEnd
    ```

## <a name="enable-ip-forwarding-on-hello-fw1-vm"></a><span data-ttu-id="36029-125">Włącz przesyłanie dalej IP na powitania FW1 maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="36029-125">Enable IP forwarding on hello FW1 VM</span></span>

<span data-ttu-id="36029-126">przesyłanie dalej IP tooenable w hello FW1 maszyny Wirtualnej, pełną hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="36029-126">tooenable IP forwarding in hello FW1 VM, complete hello following steps:</span></span>

1. <span data-ttu-id="36029-127">Uruchom następujące polecenie toocheck hello stan przesyłanie dalej IP hello:</span><span class="sxs-lookup"><span data-stu-id="36029-127">Run hello following command toocheck hello status of IP forwarding:</span></span>

    ```powershell
    Get-AzureVM -Name FW1 -ServiceName TestRGFW `
    | Get-AzureIPForwarding
    ```

2. <span data-ttu-id="36029-128">Witaj uruchom następujące polecenie tooenable przesyłanie dalej IP dla hello *FW1* maszyny Wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="36029-128">Run hello following command tooenable IP forwarding for hello *FW1* VM:</span></span>

    ```powershell
    Get-AzureVM -Name FW1 -ServiceName TestRGFW `
    | Set-AzureIPForwarding -Enable
    ```
