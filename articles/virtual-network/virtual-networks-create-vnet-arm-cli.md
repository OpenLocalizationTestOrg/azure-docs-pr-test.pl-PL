---
title: "sieć wirtualna — Azure CLI 2.0 aaaCreate | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate sieci wirtualnych za pomocą funkcji hello Azure CLI 2.0."
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 75966bcc-0056-4667-8482-6f08ca38e77a
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e79b7fe780fc81f4866f810d830824e43a5a43b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-using-hello-azure-cli-20"></a><span data-ttu-id="895b8-103">Utwórz sieć wirtualną przy użyciu hello Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="895b8-103">Create a virtual network using hello Azure CLI 2.0</span></span>

[!INCLUDE [virtual-networks-create-vnet-intro](../../includes/virtual-networks-create-vnet-intro-include.md)]

<span data-ttu-id="895b8-104">Platforma Azure ma dwa modele wdrażania: usługa Azure Resource Manager i wersja klasyczna.</span><span class="sxs-lookup"><span data-stu-id="895b8-104">Azure has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="895b8-105">Firma Microsoft zaleca utworzenie zasobów za pośrednictwem modelu wdrażania usługi Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="895b8-105">Microsoft recommends creating resources through hello Resource Manager deployment model.</span></span> <span data-ttu-id="895b8-106">więcej informacji o toolearn hello różnice między modelami hello dwa odczytu hello [modele wdrażania zrozumieć Azure](../azure-resource-manager/resource-manager-deployment-model.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="895b8-106">toolearn more about hello differences between hello two models, read hello [Understand Azure deployment models](../azure-resource-manager/resource-manager-deployment-model.md) article.</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="895b8-107">Zadanie hello toocomplete wersje interfejsu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="895b8-107">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="895b8-108">Można ukończyć powitalnych zadań przy użyciu jednej z hello następujące wersje interfejsu wiersza polecenia:</span><span class="sxs-lookup"><span data-stu-id="895b8-108">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="895b8-109">[Azure CLI 1.0](virtual-networks-create-vnet-cli-nodejs.md) — nasze interfejsu wiersza polecenia dla hello classic i zasobów zarządzania modelami wdrażania</span><span class="sxs-lookup"><span data-stu-id="895b8-109">[Azure CLI 1.0](virtual-networks-create-vnet-cli-nodejs.md) – our CLI for hello classic and resource management deployment models</span></span>
- <span data-ttu-id="895b8-110">[Azure CLI 2.0](#create-a-virtual-network) -naszej nowej generacji interfejsu wiersza polecenia dla modelu wdrażania zarządzania hello zasobów (w tym artykule) "</span><span class="sxs-lookup"><span data-stu-id="895b8-110">[Azure CLI 2.0](#create-a-virtual-network) - our next generation CLI for hello resource management deployment model (this article)\`</span></span>
 
    <span data-ttu-id="895b8-111">Możesz również utworzyć sieć wirtualną za pomocą Menedżera zasobów przy użyciu innych narzędzi lub utworzyć sieć wirtualną przy użyciu hello klasycznego modelu wdrażania, wybierając inną opcję z hello następującej listy:</span><span class="sxs-lookup"><span data-stu-id="895b8-111">You can also create a VNet through Resource Manager using other tools or create a VNet through hello classic deployment model by selecting a different option from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="895b8-112">Portal</span><span class="sxs-lookup"><span data-stu-id="895b8-112">Portal</span></span>](virtual-networks-create-vnet-arm-pportal.md)
> * [<span data-ttu-id="895b8-113">Program PowerShell</span><span class="sxs-lookup"><span data-stu-id="895b8-113">PowerShell</span></span>](virtual-networks-create-vnet-arm-ps.md)
> * [<span data-ttu-id="895b8-114">Interfejs wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="895b8-114">CLI</span></span>](virtual-networks-create-vnet-arm-cli.md)
> * [<span data-ttu-id="895b8-115">Szablon</span><span class="sxs-lookup"><span data-stu-id="895b8-115">Template</span></span>](virtual-networks-create-vnet-arm-template-click.md)
> * [<span data-ttu-id="895b8-116">Portal (klasyczny)</span><span class="sxs-lookup"><span data-stu-id="895b8-116">Portal (Classic)</span></span>](virtual-networks-create-vnet-classic-pportal.md)
> * [<span data-ttu-id="895b8-117">PowerShell (klasyczny)</span><span class="sxs-lookup"><span data-stu-id="895b8-117">PowerShell (Classic)</span></span>](virtual-networks-create-vnet-classic-netcfg-ps.md)
> * [<span data-ttu-id="895b8-118">Interfejs wiersza polecenia (klasyczny)</span><span class="sxs-lookup"><span data-stu-id="895b8-118">CLI (Classic)</span></span>](virtual-networks-create-vnet-classic-cli.md)

[!INCLUDE [virtual-networks-create-vnet-scenario-include](../../includes/virtual-networks-create-vnet-scenario-include.md)]


## <a name="create-a-virtual-network"></a><span data-ttu-id="895b8-119">Tworzenie sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="895b8-119">Create a virtual network</span></span>

<span data-ttu-id="895b8-120">toocreate sieci wirtualnych za pomocą funkcji hello Azure CLI 2.0, pełną hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="895b8-120">toocreate a virtual network using hello Azure CLI 2.0, complete hello following steps:</span></span>

1. <span data-ttu-id="895b8-121">Instalowanie i konfigurowanie hello najnowszych [Azure CLI 2.0](/cli/azure/install-az-cli2) i zaloguj się za pomocą konta Azure tooan [logowania az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="895b8-121">Install and configure hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in tooan Azure account using [az login](/cli/azure/#login).</span></span>

2. <span data-ttu-id="895b8-122">Utwórz grupę zasobów dla sieci wirtualnej przy użyciu hello [Tworzenie grupy az](/cli/azure/group#create) z hello `--name` i `--location` argumentów:</span><span class="sxs-lookup"><span data-stu-id="895b8-122">Create a resource group for your VNet using hello [az group create](/cli/azure/group#create) command with hello `--name` and `--location` arguments:</span></span>

    ```azurecli
    az group create --name TestRG --location centralus
    ```

3. <span data-ttu-id="895b8-123">Utwórz sieć wirtualną i podsieć:</span><span class="sxs-lookup"><span data-stu-id="895b8-123">Create a VNet and a subnet:</span></span>

    ```azurecli
    az network vnet create \
    --name TestVNet \
    --resource-group TestRG \
    --location centralus \
    --address-prefix 192.168.0.0/16 \
    --subnet-name FrontEnd \
    --subnet-prefix 192.168.1.0/24
    ```

    <span data-ttu-id="895b8-124">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="895b8-124">Expected output:</span></span>
    
    ```json
    {
        "newVNet": {
            "addressSpace": {
            "addressPrefixes": [
            "192.168.0.0/16"
            ]
            },
            "dhcpOptions": {
            "dnsServers": []
            },
            "provisioningState": "Succeeded",
            "resourceGuid": "<guid>",
            "subnets": [
            {
                "etag": "W/\"<guid>\"",
                "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                "name": "FrontEnd",
                "properties": {
                "addressPrefix": "192.168.1.0/24",
                "provisioningState": "Succeeded"
                },
                "resourceGroup": "TestRG"
            }
            ]
            }
    }
    ```

    <span data-ttu-id="895b8-125">Użyte parametry:</span><span class="sxs-lookup"><span data-stu-id="895b8-125">Parameters used:</span></span>

    - <span data-ttu-id="895b8-126">`--name TestVNet`: Nazwa toobe sieci wirtualnej hello utworzony.</span><span class="sxs-lookup"><span data-stu-id="895b8-126">`--name TestVNet`: Name of hello VNet toobe created.</span></span>
    - <span data-ttu-id="895b8-127">`--resource-group TestRG`: Nazwa grupy zasobów hello #, kontrolujące hello zasobów.</span><span class="sxs-lookup"><span data-stu-id="895b8-127">`--resource-group TestRG`: # hello resource group name that controls hello resource.</span></span> 
    - <span data-ttu-id="895b8-128">`--location centralus`: hello lokalizacji, do których toodeploy.</span><span class="sxs-lookup"><span data-stu-id="895b8-128">`--location centralus`: hello location into which toodeploy.</span></span>
    - <span data-ttu-id="895b8-129">`--address-prefix 192.168.0.0/16`: hello prefiksu adresu i bloku.</span><span class="sxs-lookup"><span data-stu-id="895b8-129">`--address-prefix 192.168.0.0/16`: hello address prefix and block.</span></span>  
    - <span data-ttu-id="895b8-130">`--subnet-name FrontEnd`: Nazwa hello hello podsieci.</span><span class="sxs-lookup"><span data-stu-id="895b8-130">`--subnet-name FrontEnd`: hello name of hello subnet.</span></span>
    - <span data-ttu-id="895b8-131">`--subnet-prefix 192.168.1.0/24`: hello prefiksu adresu i bloku.</span><span class="sxs-lookup"><span data-stu-id="895b8-131">`--subnet-prefix 192.168.1.0/24`: hello address prefix and block.</span></span>

    <span data-ttu-id="895b8-132">toolist hello podstawowe informacje toouse w hello obok polecenia, można badać przy użyciu sieci wirtualnej hello [Filtr kwerendy](/cli/azure/query-az-cli2):</span><span class="sxs-lookup"><span data-stu-id="895b8-132">toolist hello basic information toouse in hello next command, you can query hello VNet using a [query filter](/cli/azure/query-az-cli2):</span></span>

    ```azurecli
    az network vnet list --query '[?name==`TestVNet`].{Where:location,Name:name,Group:resourceGroup}' -o table
    ```

    <span data-ttu-id="895b8-133">Pozwalającą na uzyskanie hello następujące dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="895b8-133">Which produces hello following output:</span></span>

        Where      Name      Group

        centralus  TestVNet  TestRG

4. <span data-ttu-id="895b8-134">Utwórz podsieć:</span><span class="sxs-lookup"><span data-stu-id="895b8-134">Create a subnet:</span></span>

    ```azurecli
    az network vnet subnet create \
    --address-prefix 192.168.2.0/24 \
    --name BackEnd \
    --resource-group TestRG \
    --vnet-name TestVNet
    ```

    <span data-ttu-id="895b8-135">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="895b8-135">Expected output:</span></span>

    ```json
    {
    "addressPrefix": "192.168.2.0/24",
    "etag": "W/\"<guid> \"",
    "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/BackEnd",
    "ipConfigurations": null,
    "name": "BackEnd",
    "networkSecurityGroup": null,
    "provisioningState": "Succeeded",
    "resourceGroup": "TestRG",
    "resourceNavigationLinks": null,
    "routeTable": null
    }
    ```

    <span data-ttu-id="895b8-136">Użyte parametry:</span><span class="sxs-lookup"><span data-stu-id="895b8-136">Parameters used:</span></span>

    - <span data-ttu-id="895b8-137">`--address-prefix 192.168.2.0/24`: Blok CIDR podsieci.</span><span class="sxs-lookup"><span data-stu-id="895b8-137">`--address-prefix 192.168.2.0/24`: Subnet CIDR block.</span></span>
    - <span data-ttu-id="895b8-138">`--name BackEnd`: Nazwa nowej podsieci hello.</span><span class="sxs-lookup"><span data-stu-id="895b8-138">`--name BackEnd`: Name of hello new subnet.</span></span>
    - <span data-ttu-id="895b8-139">`--resource-group TestRG`: hello grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="895b8-139">`--resource-group TestRG`: hello resource group.</span></span>
    - <span data-ttu-id="895b8-140">`--vnet-name TestVNet`: Nazwa hello hello będący właścicielem sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="895b8-140">`--vnet-name TestVNet`: hello name of hello owning VNet.</span></span>

5. <span data-ttu-id="895b8-141">Właściwości hello zapytania hello nowej sieci wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="895b8-141">Query hello properties of hello new VNet:</span></span>

    ```azurecli
    az network vnet show \
    -g TestRG \
    -n TestVNet \
    --query '{Name:name,Where:location,Group:resourceGroup,Status:provisioningState,SubnetCount:subnets | length(@)}' \
    -o table
    ```

    <span data-ttu-id="895b8-142">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="895b8-142">Expected output:</span></span>

        Name      Where      Group    Status       SubnetCount

        TestVNet  centralus  TestRG   Succeeded              2

6. <span data-ttu-id="895b8-143">Właściwości hello zapytania hello podsieci:</span><span class="sxs-lookup"><span data-stu-id="895b8-143">Query hello properties of hello subnets:</span></span>

    ```azurecli
    az network vnet subnet list \
    -g TestRG \
    --vnet-name testvnet \
    --query '[].{Name:name,CIDR:addressPrefix,Status:provisioningState}' \
    -o table
    ```

    <span data-ttu-id="895b8-144">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="895b8-144">Expected output:</span></span>

        Name      CIDR            Status

        FrontEnd  192.168.1.0/24  Succeeded
        BackEnd   192.168.2.0/24  Succeeded

## <a name="next-steps"></a><span data-ttu-id="895b8-145">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="895b8-145">Next steps</span></span>

<span data-ttu-id="895b8-146">Dowiedz się, jak tooconnect:</span><span class="sxs-lookup"><span data-stu-id="895b8-146">Learn how tooconnect:</span></span>

- <span data-ttu-id="895b8-147">Sieć wirtualną maszyny wirtualnej (VM) tooa odczytując hello [Utwórz Maszynę wirtualną systemu Linux](../virtual-machines/linux/quick-create-cli.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="895b8-147">A virtual machine (VM) tooa virtual network by reading hello [Create a Linux VM](../virtual-machines/linux/quick-create-cli.md) article.</span></span> <span data-ttu-id="895b8-148">Zamiast tworzenia sieci wirtualnej i podsieci w krokach hello hello artykułów, możesz wybrać istniejącej sieci wirtualnej i tooconnect podsieci maszyny Wirtualnej, aby.</span><span class="sxs-lookup"><span data-stu-id="895b8-148">Instead of creating a VNet and subnet in hello steps of hello articles, you can select an existing VNet and subnet tooconnect a VM to.</span></span>
- <span data-ttu-id="895b8-149">Witaj sieci wirtualne sieci wirtualnej tooother odczytując hello [połączyć sieci wirtualnych](../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="895b8-149">hello virtual network tooother virtual networks by reading hello [Connect VNets](../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md) article.</span></span>
- <span data-ttu-id="895b8-150">Witaj sieci wirtualnej tooan sieci lokalnej za pomocą wirtualnej sieci prywatnej (VPN) do lokacji lub obwodu usługi expressroute.</span><span class="sxs-lookup"><span data-stu-id="895b8-150">hello virtual network tooan on-premises network using a site-to-site virtual private network (VPN) or ExpressRoute circuit.</span></span> <span data-ttu-id="895b8-151">Dowiedz się, jak odczytując hello [połączyć sieć lokalną tooan sieci wirtualnej przy użyciu sieci VPN lokacja lokacja](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) i [połączyć sieć wirtualną tooan obwodu ExpressRoute](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="895b8-151">Learn how by reading hello [Connect a VNet tooan on-premises network using a site-to-site VPN](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) and [Link a VNet tooan ExpressRoute circuit](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md).</span></span>
