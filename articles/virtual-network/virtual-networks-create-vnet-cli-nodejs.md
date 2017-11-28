---
title: "aaaCreate sieci wirtualnych za pomocą funkcji hello Azure CLI 1.0 | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate sieci wirtualnych za pomocą funkcji hello Azure CLI 1.0 | Menedżer zasobów."
services: virtual-network
documentationcenter: 
author: jimdial
manager: carmonm
editor: 
tags: azure-resource-manager
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/16/2017
ms.author: jdial
ms.openlocfilehash: f48a8b23a5994164b71c9b51ee8a6810d17f9392
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-using-hello-azure-cli"></a><span data-ttu-id="e1fb2-103">Utwórz sieć wirtualną przy użyciu hello wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="e1fb2-103">Create a virtual network using hello Azure CLI</span></span>

[!INCLUDE [virtual-networks-create-vnet-intro](../../includes/virtual-networks-create-vnet-intro-include.md)]

<span data-ttu-id="e1fb2-104">Platforma Azure ma dwa modele wdrażania: usługa Azure Resource Manager i wersja klasyczna.</span><span class="sxs-lookup"><span data-stu-id="e1fb2-104">Azure has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="e1fb2-105">Firma Microsoft zaleca utworzenie zasobów za pośrednictwem modelu wdrażania usługi Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="e1fb2-105">Microsoft recommends creating resources through hello Resource Manager deployment model.</span></span> <span data-ttu-id="e1fb2-106">więcej informacji o toolearn hello różnice między modelami hello dwa odczytu hello [modele wdrażania zrozumieć Azure](../azure-resource-manager/resource-manager-deployment-model.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="e1fb2-106">toolearn more about hello differences between hello two models, read hello [Understand Azure deployment models](../azure-resource-manager/resource-manager-deployment-model.md) article.</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="e1fb2-107">Zadanie hello toocomplete wersje interfejsu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="e1fb2-107">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="e1fb2-108">Można ukończyć powitalnych zadań przy użyciu jednej z hello następujące wersje interfejsu wiersza polecenia:</span><span class="sxs-lookup"><span data-stu-id="e1fb2-108">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="e1fb2-109">[Azure CLI 2.0](virtual-networks-create-vnet-arm-cli.md) -naszej nowej generacji interfejsu wiersza polecenia dla modelu wdrażania zarządzania zasobów hello</span><span class="sxs-lookup"><span data-stu-id="e1fb2-109">[Azure CLI 2.0](virtual-networks-create-vnet-arm-cli.md) - our next generation CLI for hello resource management deployment model</span></span>
- <span data-ttu-id="e1fb2-110">[Azure CLI 1.0](#create-a-virtual-network) — nasze interfejsu wiersza polecenia dla hello classic i zasobów zarządzania wdrażania modeli (w tym artykule)</span><span class="sxs-lookup"><span data-stu-id="e1fb2-110">[Azure CLI 1.0](#create-a-virtual-network) – our CLI for hello classic and resource management deployment models (this article)</span></span>

 
[!INCLUDE [virtual-networks-create-vnet-scenario-include](../../includes/virtual-networks-create-vnet-scenario-include.md)]

## <a name="create-a-virtual-network"></a><span data-ttu-id="e1fb2-111">Tworzenie sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="e1fb2-111">Create a virtual network</span></span>

<span data-ttu-id="e1fb2-112">toocreate sieci wirtualnych za pomocą funkcji hello Azure CLI, pełną hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="e1fb2-112">toocreate a virtual network using hello Azure CLI, complete hello following steps:</span></span>

1. <span data-ttu-id="e1fb2-113">Instalowanie i konfigurowanie hello Azure CLI przez hello następujące kroki w hello [Instalowanie i Konfigurowanie interfejsu wiersza polecenia Azure hello](../cli-install-nodejs.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="e1fb2-113">Install and configure hello Azure CLI by following hello steps in hello [Install and Configure hello Azure CLI](../cli-install-nodejs.md) article.</span></span>

2. <span data-ttu-id="e1fb2-114">Utwórz sieć wirtualną i podsieć:</span><span class="sxs-lookup"><span data-stu-id="e1fb2-114">Create a VNet and a subnet:</span></span>

    ```azurecli
    azure network vnet create --vnet TestVNet -e 192.168.0.0 -i 16 -n FrontEnd -p 192.168.1.0 -r 24 -l "Central US"
    ```

    <span data-ttu-id="e1fb2-115">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="e1fb2-115">Expected output:</span></span>
   
            info:    Executing command network vnet create
            + Looking up network configuration
            + Looking up locations
            + Setting network configuration
            info:    network vnet create command OK

    <span data-ttu-id="e1fb2-116">Użyte parametry:</span><span class="sxs-lookup"><span data-stu-id="e1fb2-116">Parameters used:</span></span>

   * <span data-ttu-id="e1fb2-117">**--vnet**.</span><span class="sxs-lookup"><span data-stu-id="e1fb2-117">**--vnet**.</span></span> <span data-ttu-id="e1fb2-118">Nazwa toobe sieci wirtualnej hello utworzony.</span><span class="sxs-lookup"><span data-stu-id="e1fb2-118">Name of hello VNet toobe created.</span></span> <span data-ttu-id="e1fb2-119">W naszym scenariuszu jest to *TestVNet*</span><span class="sxs-lookup"><span data-stu-id="e1fb2-119">For our scenario, *TestVNet*</span></span>
   * <span data-ttu-id="e1fb2-120">**-e (lub--przestrzeni adresowej)**.</span><span class="sxs-lookup"><span data-stu-id="e1fb2-120">**-e (or --address-space)**.</span></span> <span data-ttu-id="e1fb2-121">Przestrzeń adresowa sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e1fb2-121">VNet address space.</span></span> <span data-ttu-id="e1fb2-122">W naszym scenariuszu *192.168.0.0*</span><span class="sxs-lookup"><span data-stu-id="e1fb2-122">For our scenario, *192.168.0.0*</span></span>
   * <span data-ttu-id="e1fb2-123">**-i (lub - cidr)**.</span><span class="sxs-lookup"><span data-stu-id="e1fb2-123">**-i (or -cidr)**.</span></span> <span data-ttu-id="e1fb2-124">Maska sieci w formacie CIDR.</span><span class="sxs-lookup"><span data-stu-id="e1fb2-124">Network mask in CIDR format.</span></span> <span data-ttu-id="e1fb2-125">W naszym scenariuszu *16*.</span><span class="sxs-lookup"><span data-stu-id="e1fb2-125">For our scenario, *16*.</span></span>
   * <span data-ttu-id="e1fb2-126">**-n (lub--nazwy podsieci**).</span><span class="sxs-lookup"><span data-stu-id="e1fb2-126">**-n (or --subnet-name**).</span></span> <span data-ttu-id="e1fb2-127">Nazwa hello pierwszej podsieci.</span><span class="sxs-lookup"><span data-stu-id="e1fb2-127">Name of hello first subnet.</span></span> <span data-ttu-id="e1fb2-128">W naszym scenariuszu jest to *FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="e1fb2-128">For our scenario, *FrontEnd*.</span></span>
   * <span data-ttu-id="e1fb2-129">**-p (lub--podsieci start-ip)**.</span><span class="sxs-lookup"><span data-stu-id="e1fb2-129">**-p (or --subnet-start-ip)**.</span></span> <span data-ttu-id="e1fb2-130">Początkowy adres IP dla podsieci lub przestrzeni adresowej podsieci.</span><span class="sxs-lookup"><span data-stu-id="e1fb2-130">Starting IP address for subnet, or subnet address space.</span></span> <span data-ttu-id="e1fb2-131">W naszym scenariuszu *192.168.1.0*.</span><span class="sxs-lookup"><span data-stu-id="e1fb2-131">For our scenario, *192.168.1.0*.</span></span>
   * <span data-ttu-id="e1fb2-132">**-r (lub--podsieci cidr)**.</span><span class="sxs-lookup"><span data-stu-id="e1fb2-132">**-r (or --subnet-cidr)**.</span></span> <span data-ttu-id="e1fb2-133">Maska sieci w formacie CIDR podsieci.</span><span class="sxs-lookup"><span data-stu-id="e1fb2-133">Network mask in CIDR format for subnet.</span></span> <span data-ttu-id="e1fb2-134">W naszym scenariuszu *24*.</span><span class="sxs-lookup"><span data-stu-id="e1fb2-134">For our scenario, *24*.</span></span>
   * <span data-ttu-id="e1fb2-135">**-l (lub --location)**.</span><span class="sxs-lookup"><span data-stu-id="e1fb2-135">**-l (or --location)**.</span></span> <span data-ttu-id="e1fb2-136">Region platformy Azure, w której jest tworzony hello sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e1fb2-136">Azure region where hello VNet is created.</span></span> <span data-ttu-id="e1fb2-137">W naszym scenariuszu *środkowe stany USA*.</span><span class="sxs-lookup"><span data-stu-id="e1fb2-137">For our scenario, *Central US*.</span></span>

3. <span data-ttu-id="e1fb2-138">Utwórz podsieć:</span><span class="sxs-lookup"><span data-stu-id="e1fb2-138">Create a subnet:</span></span>

    ```azurecli
    azure network vnet subnet create -t TestVNet -n BackEnd -a 192.168.2.0/24
    ```
   
    <span data-ttu-id="e1fb2-139">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="e1fb2-139">Expected output:</span></span>

            info:    Executing command network vnet subnet create
            + Looking up network configuration
            + Creating subnet "BackEnd"
            + Setting network configuration
            + Looking up hello subnet "BackEnd"
            + Looking up network configuration
            data:    Name                            : BackEnd
            data:    Address prefix                  : 192.168.2.0/24
            info:    network vnet subnet create command OK

    <span data-ttu-id="e1fb2-140">Użyte parametry:</span><span class="sxs-lookup"><span data-stu-id="e1fb2-140">Parameters used:</span></span>

   * <span data-ttu-id="e1fb2-141">**-t (lub--vnet-name**.</span><span class="sxs-lookup"><span data-stu-id="e1fb2-141">**-t (or --vnet-name**.</span></span> <span data-ttu-id="e1fb2-142">Nazwa sieci wirtualnej, w którym zostanie utworzona podsieć hello hello.</span><span class="sxs-lookup"><span data-stu-id="e1fb2-142">Name of hello VNet where hello subnet will be created.</span></span> <span data-ttu-id="e1fb2-143">W naszym scenariuszu jest to *TestVNet*.</span><span class="sxs-lookup"><span data-stu-id="e1fb2-143">For our scenario, *TestVNet*.</span></span>
   * <span data-ttu-id="e1fb2-144">**-n (lub --name)**.</span><span class="sxs-lookup"><span data-stu-id="e1fb2-144">**-n (or --name)**.</span></span> <span data-ttu-id="e1fb2-145">Nazwa nowej podsieci hello.</span><span class="sxs-lookup"><span data-stu-id="e1fb2-145">Name of hello new subnet.</span></span> <span data-ttu-id="e1fb2-146">W naszym scenariuszu *zaplecza*.</span><span class="sxs-lookup"><span data-stu-id="e1fb2-146">For our scenario, *BackEnd*.</span></span>
   * <span data-ttu-id="e1fb2-147">**-a (lub --address-prefix)**.</span><span class="sxs-lookup"><span data-stu-id="e1fb2-147">**-a (or --address-prefix)**.</span></span> <span data-ttu-id="e1fb2-148">Blok CIDR podsieci.</span><span class="sxs-lookup"><span data-stu-id="e1fb2-148">Subnet CIDR block.</span></span> <span data-ttu-id="e1fb2-149">Cztery naszym scenariuszu *192.168.2.0/24*.</span><span class="sxs-lookup"><span data-stu-id="e1fb2-149">Four our scenario, *192.168.2.0/24*.</span></span>
   
4. <span data-ttu-id="e1fb2-150">właściwości hello tooview hello nowej sieci wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="e1fb2-150">tooview hello properties of hello new VNet:</span></span>

    ```azurecli
    azure network vnet show
    ```
   
    <span data-ttu-id="e1fb2-151">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="e1fb2-151">Expected output:</span></span>
   
            info:    Executing command network vnet show
            Virtual network name: TestVNet
            + Looking up hello virtual network sites
            data:    Name                            : TestVNet
            data:    Location                        : Central US
            data:    State                           : Created
            data:    Address space                   : 192.168.0.0/16
            data:    Subnets:
            data:      Name                          : FrontEnd
            data:      Address prefix                : 192.168.1.0/24
            data:
            data:      Name                          : BackEnd
            data:      Address prefix                : 192.168.2.0/24
            data:
            info:    network vnet show command OK

## <a name="next-steps"></a><span data-ttu-id="e1fb2-152">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e1fb2-152">Next steps</span></span>

<span data-ttu-id="e1fb2-153">Dowiedz się, jak tooconnect:</span><span class="sxs-lookup"><span data-stu-id="e1fb2-153">Learn how tooconnect:</span></span>

- <span data-ttu-id="e1fb2-154">Sieć wirtualną maszyny wirtualnej (VM) tooa odczytując hello [Utwórz Maszynę wirtualną systemu Linux](../virtual-machines/linux/quick-create-cli.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="e1fb2-154">A virtual machine (VM) tooa virtual network by reading hello [Create a Linux VM](../virtual-machines/linux/quick-create-cli.md) article.</span></span> <span data-ttu-id="e1fb2-155">Zamiast tworzenia sieci wirtualnej i podsieci w krokach hello hello artykułów, możesz wybrać istniejącej sieci wirtualnej i tooconnect podsieci maszyny Wirtualnej, aby.</span><span class="sxs-lookup"><span data-stu-id="e1fb2-155">Instead of creating a VNet and subnet in hello steps of hello articles, you can select an existing VNet and subnet tooconnect a VM to.</span></span>
- <span data-ttu-id="e1fb2-156">Witaj sieci wirtualne sieci wirtualnej tooother odczytując hello [połączyć sieci wirtualnych](../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="e1fb2-156">hello virtual network tooother virtual networks by reading hello [Connect VNets](../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md) article.</span></span>
- <span data-ttu-id="e1fb2-157">Witaj sieci wirtualnej tooan sieci lokalnej za pomocą wirtualnej sieci prywatnej (VPN) do lokacji lub obwodu usługi expressroute.</span><span class="sxs-lookup"><span data-stu-id="e1fb2-157">hello virtual network tooan on-premises network using a site-to-site virtual private network (VPN) or ExpressRoute circuit.</span></span> <span data-ttu-id="e1fb2-158">Dowiedz się, jak odczytując hello [połączyć sieć lokalną tooan sieci wirtualnej przy użyciu sieci VPN lokacja lokacja](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) i [połączyć sieć wirtualną tooan obwodu ExpressRoute](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="e1fb2-158">Learn how by reading hello [Connect a VNet tooan on-premises network using a site-to-site VPN](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) and [Link a VNet tooan ExpressRoute circuit](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md).</span></span>
