---
title: "Utwórz sieć wirtualną przy użyciu 1.0 interfejsu wiersza polecenia platformy Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak utworzyć sieć wirtualną przy użyciu 1.0 interfejsu wiersza polecenia platformy Azure | Menedżer zasobów."
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
ms.openlocfilehash: f0649c5c8c04dda72d2f147601efb37217f9bade
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-virtual-network-using-the-azure-cli"></a><span data-ttu-id="ab9fb-103">Utwórz sieć wirtualną przy użyciu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="ab9fb-103">Create a virtual network using the Azure CLI</span></span>

[!INCLUDE [virtual-networks-create-vnet-intro](../../includes/virtual-networks-create-vnet-intro-include.md)]

<span data-ttu-id="ab9fb-104">Platforma Azure ma dwa modele wdrażania: usługa Azure Resource Manager i wersja klasyczna.</span><span class="sxs-lookup"><span data-stu-id="ab9fb-104">Azure has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="ab9fb-105">Firma Microsoft zaleca tworzenie zasobów za pomocą modelu wdrożenia usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ab9fb-105">Microsoft recommends creating resources through the Resource Manager deployment model.</span></span> <span data-ttu-id="ab9fb-106">Aby dowiedzieć się więcej o różnicach między dwoma modelami, zapoznaj się z artykułem [Understand Azure deployment models](../azure-resource-manager/resource-manager-deployment-model.md) (Informacje na temat modeli wdrażania platformy Azure).</span><span class="sxs-lookup"><span data-stu-id="ab9fb-106">To learn more about the differences between the two models, read the [Understand Azure deployment models](../azure-resource-manager/resource-manager-deployment-model.md) article.</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="ab9fb-107">Wersje interfejsu wiersza polecenia umożliwiające wykonanie zadania</span><span class="sxs-lookup"><span data-stu-id="ab9fb-107">CLI versions to complete the task</span></span>
<span data-ttu-id="ab9fb-108">Zadanie można wykonać przy użyciu jednej z następujących wersji interfejsu wiersza polecenia:</span><span class="sxs-lookup"><span data-stu-id="ab9fb-108">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="ab9fb-109">[Interfejs wiersza polecenia platformy Azure w wersji 2.0](virtual-networks-create-vnet-arm-cli.md) — nasz interfejs wiersza polecenia nowej generacji dla modelu wdrażania na potrzeby zarządzania zasobami</span><span class="sxs-lookup"><span data-stu-id="ab9fb-109">[Azure CLI 2.0](virtual-networks-create-vnet-arm-cli.md) - our next generation CLI for the resource management deployment model</span></span>
- <span data-ttu-id="ab9fb-110">[Azure CLI 1.0](#create-a-virtual-network) — nasze interfejsu wiersza polecenia dla klasycznego i zasobów zarządzania wdrażania modeli (w tym artykule)</span><span class="sxs-lookup"><span data-stu-id="ab9fb-110">[Azure CLI 1.0](#create-a-virtual-network) – our CLI for the classic and resource management deployment models (this article)</span></span>

 
[!INCLUDE [virtual-networks-create-vnet-scenario-include](../../includes/virtual-networks-create-vnet-scenario-include.md)]

## <a name="create-a-virtual-network"></a><span data-ttu-id="ab9fb-111">Tworzenie sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="ab9fb-111">Create a virtual network</span></span>

<span data-ttu-id="ab9fb-112">Aby utworzyć sieć wirtualną przy użyciu wiersza polecenia platformy Azure, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="ab9fb-112">To create a virtual network using the Azure CLI, complete the following steps:</span></span>

1. <span data-ttu-id="ab9fb-113">Instalowanie i Konfigurowanie interfejsu wiersza polecenia Azure, wykonując kroki opisane w [Instalowanie i Konfigurowanie interfejsu wiersza polecenia Azure](../cli-install-nodejs.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="ab9fb-113">Install and configure the Azure CLI by following the steps in the [Install and Configure the Azure CLI](../cli-install-nodejs.md) article.</span></span>

2. <span data-ttu-id="ab9fb-114">Utwórz sieć wirtualną i podsieć:</span><span class="sxs-lookup"><span data-stu-id="ab9fb-114">Create a VNet and a subnet:</span></span>

    ```azurecli
    azure network vnet create --vnet TestVNet -e 192.168.0.0 -i 16 -n FrontEnd -p 192.168.1.0 -r 24 -l "Central US"
    ```

    <span data-ttu-id="ab9fb-115">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="ab9fb-115">Expected output:</span></span>
   
            info:    Executing command network vnet create
            + Looking up network configuration
            + Looking up locations
            + Setting network configuration
            info:    network vnet create command OK

    <span data-ttu-id="ab9fb-116">Użyte parametry:</span><span class="sxs-lookup"><span data-stu-id="ab9fb-116">Parameters used:</span></span>

   * <span data-ttu-id="ab9fb-117">**--vnet**.</span><span class="sxs-lookup"><span data-stu-id="ab9fb-117">**--vnet**.</span></span> <span data-ttu-id="ab9fb-118">Nazwa sieci wirtualnej, która zostanie utworzona.</span><span class="sxs-lookup"><span data-stu-id="ab9fb-118">Name of the VNet to be created.</span></span> <span data-ttu-id="ab9fb-119">W naszym scenariuszu jest to *TestVNet*</span><span class="sxs-lookup"><span data-stu-id="ab9fb-119">For our scenario, *TestVNet*</span></span>
   * <span data-ttu-id="ab9fb-120">**-e (lub--przestrzeni adresowej)**.</span><span class="sxs-lookup"><span data-stu-id="ab9fb-120">**-e (or --address-space)**.</span></span> <span data-ttu-id="ab9fb-121">Przestrzeń adresowa sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ab9fb-121">VNet address space.</span></span> <span data-ttu-id="ab9fb-122">W naszym scenariuszu *192.168.0.0*</span><span class="sxs-lookup"><span data-stu-id="ab9fb-122">For our scenario, *192.168.0.0*</span></span>
   * <span data-ttu-id="ab9fb-123">**-i (lub - cidr)**.</span><span class="sxs-lookup"><span data-stu-id="ab9fb-123">**-i (or -cidr)**.</span></span> <span data-ttu-id="ab9fb-124">Maska sieci w formacie CIDR.</span><span class="sxs-lookup"><span data-stu-id="ab9fb-124">Network mask in CIDR format.</span></span> <span data-ttu-id="ab9fb-125">W naszym scenariuszu *16*.</span><span class="sxs-lookup"><span data-stu-id="ab9fb-125">For our scenario, *16*.</span></span>
   * <span data-ttu-id="ab9fb-126">**-n (lub--nazwy podsieci**).</span><span class="sxs-lookup"><span data-stu-id="ab9fb-126">**-n (or --subnet-name**).</span></span> <span data-ttu-id="ab9fb-127">Nazwa pierwszej podsieci.</span><span class="sxs-lookup"><span data-stu-id="ab9fb-127">Name of the first subnet.</span></span> <span data-ttu-id="ab9fb-128">W naszym scenariuszu jest to *FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="ab9fb-128">For our scenario, *FrontEnd*.</span></span>
   * <span data-ttu-id="ab9fb-129">**-p (lub--podsieci start-ip)**.</span><span class="sxs-lookup"><span data-stu-id="ab9fb-129">**-p (or --subnet-start-ip)**.</span></span> <span data-ttu-id="ab9fb-130">Początkowy adres IP dla podsieci lub przestrzeni adresowej podsieci.</span><span class="sxs-lookup"><span data-stu-id="ab9fb-130">Starting IP address for subnet, or subnet address space.</span></span> <span data-ttu-id="ab9fb-131">W naszym scenariuszu *192.168.1.0*.</span><span class="sxs-lookup"><span data-stu-id="ab9fb-131">For our scenario, *192.168.1.0*.</span></span>
   * <span data-ttu-id="ab9fb-132">**-r (lub--podsieci cidr)**.</span><span class="sxs-lookup"><span data-stu-id="ab9fb-132">**-r (or --subnet-cidr)**.</span></span> <span data-ttu-id="ab9fb-133">Maska sieci w formacie CIDR podsieci.</span><span class="sxs-lookup"><span data-stu-id="ab9fb-133">Network mask in CIDR format for subnet.</span></span> <span data-ttu-id="ab9fb-134">W naszym scenariuszu *24*.</span><span class="sxs-lookup"><span data-stu-id="ab9fb-134">For our scenario, *24*.</span></span>
   * <span data-ttu-id="ab9fb-135">**-l (lub --location)**.</span><span class="sxs-lookup"><span data-stu-id="ab9fb-135">**-l (or --location)**.</span></span> <span data-ttu-id="ab9fb-136">Region platformy Azure, w którym utworzona sieć wirtualna.</span><span class="sxs-lookup"><span data-stu-id="ab9fb-136">Azure region where the VNet is created.</span></span> <span data-ttu-id="ab9fb-137">W naszym scenariuszu *środkowe stany USA*.</span><span class="sxs-lookup"><span data-stu-id="ab9fb-137">For our scenario, *Central US*.</span></span>

3. <span data-ttu-id="ab9fb-138">Utwórz podsieć:</span><span class="sxs-lookup"><span data-stu-id="ab9fb-138">Create a subnet:</span></span>

    ```azurecli
    azure network vnet subnet create -t TestVNet -n BackEnd -a 192.168.2.0/24
    ```
   
    <span data-ttu-id="ab9fb-139">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="ab9fb-139">Expected output:</span></span>

            info:    Executing command network vnet subnet create
            + Looking up network configuration
            + Creating subnet "BackEnd"
            + Setting network configuration
            + Looking up the subnet "BackEnd"
            + Looking up network configuration
            data:    Name                            : BackEnd
            data:    Address prefix                  : 192.168.2.0/24
            info:    network vnet subnet create command OK

    <span data-ttu-id="ab9fb-140">Użyte parametry:</span><span class="sxs-lookup"><span data-stu-id="ab9fb-140">Parameters used:</span></span>

   * <span data-ttu-id="ab9fb-141">**-t (lub--vnet-name**.</span><span class="sxs-lookup"><span data-stu-id="ab9fb-141">**-t (or --vnet-name**.</span></span> <span data-ttu-id="ab9fb-142">Nazwa sieci wirtualnej, w której zostanie utworzona podsieć.</span><span class="sxs-lookup"><span data-stu-id="ab9fb-142">Name of the VNet where the subnet will be created.</span></span> <span data-ttu-id="ab9fb-143">W naszym scenariuszu jest to *TestVNet*.</span><span class="sxs-lookup"><span data-stu-id="ab9fb-143">For our scenario, *TestVNet*.</span></span>
   * <span data-ttu-id="ab9fb-144">**-n (lub --name)**.</span><span class="sxs-lookup"><span data-stu-id="ab9fb-144">**-n (or --name)**.</span></span> <span data-ttu-id="ab9fb-145">Nazwa nowej podsieci.</span><span class="sxs-lookup"><span data-stu-id="ab9fb-145">Name of the new subnet.</span></span> <span data-ttu-id="ab9fb-146">W naszym scenariuszu *zaplecza*.</span><span class="sxs-lookup"><span data-stu-id="ab9fb-146">For our scenario, *BackEnd*.</span></span>
   * <span data-ttu-id="ab9fb-147">**-a (lub --address-prefix)**.</span><span class="sxs-lookup"><span data-stu-id="ab9fb-147">**-a (or --address-prefix)**.</span></span> <span data-ttu-id="ab9fb-148">Blok CIDR podsieci.</span><span class="sxs-lookup"><span data-stu-id="ab9fb-148">Subnet CIDR block.</span></span> <span data-ttu-id="ab9fb-149">Cztery naszym scenariuszu *192.168.2.0/24*.</span><span class="sxs-lookup"><span data-stu-id="ab9fb-149">Four our scenario, *192.168.2.0/24*.</span></span>
   
4. <span data-ttu-id="ab9fb-150">Aby wyświetlić właściwości nowej sieci wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="ab9fb-150">To view the properties of the new VNet:</span></span>

    ```azurecli
    azure network vnet show
    ```
   
    <span data-ttu-id="ab9fb-151">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="ab9fb-151">Expected output:</span></span>
   
            info:    Executing command network vnet show
            Virtual network name: TestVNet
            + Looking up the virtual network sites
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

## <a name="next-steps"></a><span data-ttu-id="ab9fb-152">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ab9fb-152">Next steps</span></span>

<span data-ttu-id="ab9fb-153">Dowiedz się, jak połączyć:</span><span class="sxs-lookup"><span data-stu-id="ab9fb-153">Learn how to connect:</span></span>

- <span data-ttu-id="ab9fb-154">Maszyna wirtualna (VM) do sieci wirtualnej, odczytując [Utwórz Maszynę wirtualną systemu Linux](../virtual-machines/linux/quick-create-cli.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="ab9fb-154">A virtual machine (VM) to a virtual network by reading the [Create a Linux VM](../virtual-machines/linux/quick-create-cli.md) article.</span></span> <span data-ttu-id="ab9fb-155">Zamiast tworzyć sieć wirtualną i podsieć, wykonując kroki opisane w artykułach, można wybrać istniejącą sieć wirtualną i podsieć, z którymi zostanie połączona maszyna wirtualna.</span><span class="sxs-lookup"><span data-stu-id="ab9fb-155">Instead of creating a VNet and subnet in the steps of the articles, you can select an existing VNet and subnet to connect a VM to.</span></span>
- <span data-ttu-id="ab9fb-156">Sieć wirtualną z innymi sieciami wirtualnymi. Odpowiednie informacje możesz znaleźć w artykule [Łączenie sieci wirtualnych](../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md).</span><span class="sxs-lookup"><span data-stu-id="ab9fb-156">The virtual network to other virtual networks by reading the [Connect VNets](../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md) article.</span></span>
- <span data-ttu-id="ab9fb-157">Sieć wirtualną z siecią lokalną za pomocą prywatnej sieci wirtualnej (VPN) typu lokacja-lokacja lub obwodu usługi ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="ab9fb-157">The virtual network to an on-premises network using a site-to-site virtual private network (VPN) or ExpressRoute circuit.</span></span> <span data-ttu-id="ab9fb-158">Dowiedz się, jak odczytując [połączyć sieć wirtualną z siecią lokalną przy użyciu sieci VPN lokacja lokacja](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) i [połączyć sieć wirtualną z obwodem usługi ExpressRoute](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="ab9fb-158">Learn how by reading the [Connect a VNet to an on-premises network using a site-to-site VPN](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) and [Link a VNet to an ExpressRoute circuit](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md).</span></span>