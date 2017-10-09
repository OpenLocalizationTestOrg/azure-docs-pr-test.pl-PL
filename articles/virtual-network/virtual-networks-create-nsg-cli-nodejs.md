---
title: "aaaCreate sieciowej grupy zabezpieczeń — 1.0 interfejsu wiersza polecenia platformy Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate i wdrażanie grup zabezpieczeń sieci przy użyciu hello Azure CLI w wersji 1.0."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/17/2017
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: eeb7feedab959d92659e03c5c46d93fdfc08faea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-network-security-groups-using-hello-azure-cli-10"></a><span data-ttu-id="7d6a6-103">Tworzenie sieci za pomocą hello Azure CLI 1.0 grup zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="7d6a6-103">Create network security groups using hello Azure CLI 1.0</span></span>


## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="7d6a6-104">Zadanie hello toocomplete wersje interfejsu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="7d6a6-104">CLI versions toocomplete hello task</span></span> 

<span data-ttu-id="7d6a6-105">Można ukończyć powitalnych zadań przy użyciu jednej z hello następujące wersje interfejsu wiersza polecenia:</span><span class="sxs-lookup"><span data-stu-id="7d6a6-105">You can complete hello task using one of hello following CLI versions:</span></span> 

- <span data-ttu-id="7d6a6-106">[Azure CLI 1.0](#how-to-create-the-nsg-for-the-front-end-subnet) — nasze interfejsu wiersza polecenia dla hello classic i zasobów zarządzania wdrażania modeli (w tym artykule)</span><span class="sxs-lookup"><span data-stu-id="7d6a6-106">[Azure CLI 1.0](#how-to-create-the-nsg-for-the-front-end-subnet) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="7d6a6-107">[Azure CLI 2.0](virtual-networks-create-nsg-arm-cli.md) — nasze CLI następnej generacji dla modelu wdrażania zarządzania zasobów hello</span><span class="sxs-lookup"><span data-stu-id="7d6a6-107">[Azure CLI 2.0](virtual-networks-create-nsg-arm-cli.md) - our next-generation CLI for hello resource management deployment model</span></span> 

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="7d6a6-108">W tym artykule omówiono modelu wdrażania usługi Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="7d6a6-108">This article covers hello Resource Manager deployment model.</span></span> <span data-ttu-id="7d6a6-109">Możesz również [tworzenia grup NSG w hello klasycznego modelu wdrażania](virtual-networks-create-nsg-classic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="7d6a6-109">You can also [create NSGs in hello classic deployment model](virtual-networks-create-nsg-classic-cli.md).</span></span>

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

<span data-ttu-id="7d6a6-110">Poniższe polecenia interfejsu wiersza polecenia Azure próbki Hello oczekiwać środowisku niezłożonym już utworzone w zależności od scenariusza hello powyżej.</span><span class="sxs-lookup"><span data-stu-id="7d6a6-110">hello sample Azure CLI commands below expect a simple environment already created based on hello scenario above.</span></span> 

## <a name="how-toocreate-hello-nsg-for-hello-front-end-subnet"></a><span data-ttu-id="7d6a6-111">Jak toocreate hello NSG dla podsieci frontonu hello</span><span class="sxs-lookup"><span data-stu-id="7d6a6-111">How toocreate hello NSG for hello front end subnet</span></span>
<span data-ttu-id="7d6a6-112">toocreate o nazwie grupy NSG o nazwie *frontonu NSG* oparte na powyższym scenariuszu hello, wykonaj poniższe kroki hello.</span><span class="sxs-lookup"><span data-stu-id="7d6a6-112">toocreate an NSG named named *NSG-FrontEnd* based on hello scenario above, follow hello steps below.</span></span>

1. <span data-ttu-id="7d6a6-113">Jeśli po raz pierwszy używasz interfejsu wiersza polecenia Azure, zobacz [Instalowanie i Konfigurowanie interfejsu wiersza polecenia Azure hello](../cli-install-nodejs.md) i wykonaj instrukcje hello zapasowej punktu toohello, gdzie należy wybrać konto platformy Azure i subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="7d6a6-113">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="7d6a6-114">Uruchom hello **trybie azure config** tooswitch tooResource menedżera trybu poleceń, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="7d6a6-114">Run hello **azure config mode** command tooswitch tooResource Manager mode, as shown below.</span></span>
   
        azure config mode arm
   
    <span data-ttu-id="7d6a6-115">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="7d6a6-115">Expected output:</span></span>
   
        info:    New mode is arm
3. <span data-ttu-id="7d6a6-116">Uruchom hello **utworzyć sieć platformy azure nsg** toocreate polecenia grupy NSG.</span><span class="sxs-lookup"><span data-stu-id="7d6a6-116">Run hello **azure network nsg create** command toocreate an NSG.</span></span>
   
        azure network nsg create -g TestRG -l westus -n NSG-FrontEnd
   
    <span data-ttu-id="7d6a6-117">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="7d6a6-117">Expected output:</span></span>
   
        info:    Executing command network nsg create
        info:    Looking up hello network security group "NSG-FrontEnd"
        info:    Creating a network security group "NSG-FrontEnd"
        info:    Looking up hello network security group "NSG-FrontEnd"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd
        data:    Name                            : NSG-FrontEnd
        data:    Type                            : Microsoft.Network/networkSecurityGroups
        data:    Location                        : westus
        data:    Provisioning state              : Succeeded
        data:    Security group rules:
        data:    Name                           Source IP          Source Port  Destination IP  Destination Port  Protocol  Direction  Access  Priority
        data:    -----------------------------  -----------------  -----------  --------------  ----------------  --------  ---------  ------  --------
        data:    AllowVnetInBound               VirtualNetwork     *            VirtualNetwork  *                 *         Inbound    Allow   65000   
        data:    AllowAzureLoadBalancerInBound  AzureLoadBalancer  *            *               *                 *         Inbound    Allow   65001   
        data:    DenyAllInBound                 *                  *            *               *                 *         Inbound    Deny    65500   
        data:    AllowVnetOutBound              VirtualNetwork     *            VirtualNetwork  *                 *         Outbound   Allow   65000   
        data:    AllowInternetOutBound          *                  *            Internet        *                 *         Outbound   Allow   65001   
        data:    DenyAllOutBound                *                  *            *               *                 *         Outbound   Deny    65500   
        info:    network nsg create command OK
   
    <span data-ttu-id="7d6a6-118">Parametry:</span><span class="sxs-lookup"><span data-stu-id="7d6a6-118">Parameters:</span></span>
   
   * <span data-ttu-id="7d6a6-119">**-g (lub --resource-group)**.</span><span class="sxs-lookup"><span data-stu-id="7d6a6-119">**-g (or --resource-group)**.</span></span> <span data-ttu-id="7d6a6-120">Nazwa grupy zasobów hello której zostanie utworzona hello NSG.</span><span class="sxs-lookup"><span data-stu-id="7d6a6-120">Name of hello resource group where hello NSG will be created.</span></span> <span data-ttu-id="7d6a6-121">W naszym scenariuszu jest to *TestRG*.</span><span class="sxs-lookup"><span data-stu-id="7d6a6-121">For our scenario, *TestRG*.</span></span>
   * <span data-ttu-id="7d6a6-122">**-l (lub --location)**.</span><span class="sxs-lookup"><span data-stu-id="7d6a6-122">**-l (or --location)**.</span></span> <span data-ttu-id="7d6a6-123">Region platformy Azure, której hello Nowa grupa NSG zostanie utworzona.</span><span class="sxs-lookup"><span data-stu-id="7d6a6-123">Azure region where hello new NSG will be created.</span></span> <span data-ttu-id="7d6a6-124">W naszym scenariuszu *westus*.</span><span class="sxs-lookup"><span data-stu-id="7d6a6-124">For our scenario, *westus*.</span></span>
   * <span data-ttu-id="7d6a6-125">**-n (lub --name)**.</span><span class="sxs-lookup"><span data-stu-id="7d6a6-125">**-n (or --name)**.</span></span> <span data-ttu-id="7d6a6-126">Nazwa hello Nowa grupa NSG.</span><span class="sxs-lookup"><span data-stu-id="7d6a6-126">Name for hello new NSG.</span></span> <span data-ttu-id="7d6a6-127">W naszym scenariuszu *frontonu NSG*.</span><span class="sxs-lookup"><span data-stu-id="7d6a6-127">For our scenario, *NSG-FrontEnd*.</span></span>
4. <span data-ttu-id="7d6a6-128">Uruchom hello **Tworzenie reguły nsg sieć platformy azure** toocreate polecenia regułę, która umożliwia dostęp tooport 3389 (RDP) z hello Internet.</span><span class="sxs-lookup"><span data-stu-id="7d6a6-128">Run hello **azure network nsg rule create** command toocreate a rule that allows access tooport 3389 (RDP) from hello Internet.</span></span>
   
        azure network nsg rule create -g TestRG -a NSG-FrontEnd -n rdp-rule -c Allow -p Tcp -r Inbound -y 100 -f Internet -o * -e * -u 3389
   
    <span data-ttu-id="7d6a6-129">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="7d6a6-129">Expected output:</span></span>
   
        info:    Executing command network nsg rule create
        warn:    Using default direction: Inbound
        info:    Looking up hello network security rule "rdp-rule"
        info:    Creating a network security rule "rdp-rule"
        info:    Looking up hello network security group "NSG-FrontEnd"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/rdp
        -rule
        data:    Name                            : rdp-rule
        data:    Type                            : Microsoft.Network/networkSecurityGroups/securityRules
        data:    Provisioning state              : Succeeded
        data:    Source IP                       : Internet
        data:    Source Port                     : *
        data:    Destination IP                  : *
        data:    Destination Port                : 3389
        data:    Protocol                        : Tcp
        data:    Direction                       : Inbound
        data:    Access                          : Allow
        data:    Priority                        : 100
        info:    network nsg rule create command OK
   
    <span data-ttu-id="7d6a6-130">Parametry:</span><span class="sxs-lookup"><span data-stu-id="7d6a6-130">Parameters:</span></span>
   
   * <span data-ttu-id="7d6a6-131">**-nazwę (lub--nsg —)**.</span><span class="sxs-lookup"><span data-stu-id="7d6a6-131">**-a (or --nsg-name)**.</span></span> <span data-ttu-id="7d6a6-132">Nazwa grupy NSG hello, w których hello reguła zostanie utworzona.</span><span class="sxs-lookup"><span data-stu-id="7d6a6-132">Name of hello NSG in which hello rule will be created.</span></span> <span data-ttu-id="7d6a6-133">W naszym scenariuszu *frontonu NSG*.</span><span class="sxs-lookup"><span data-stu-id="7d6a6-133">For our scenario, *NSG-FrontEnd*.</span></span>
   * <span data-ttu-id="7d6a6-134">**-n (lub --name)**.</span><span class="sxs-lookup"><span data-stu-id="7d6a6-134">**-n (or --name)**.</span></span> <span data-ttu-id="7d6a6-135">Nazwa nowej reguły hello.</span><span class="sxs-lookup"><span data-stu-id="7d6a6-135">Name for hello new rule.</span></span> <span data-ttu-id="7d6a6-136">W naszym scenariuszu *reguły protokołu rdp*.</span><span class="sxs-lookup"><span data-stu-id="7d6a6-136">For our scenario, *rdp-rule*.</span></span>
   * <span data-ttu-id="7d6a6-137">**-c (lub--dostępu)**.</span><span class="sxs-lookup"><span data-stu-id="7d6a6-137">**-c (or --access)**.</span></span> <span data-ttu-id="7d6a6-138">Poziom dostępu dla reguły hello (Deny lub Zezwalaj).</span><span class="sxs-lookup"><span data-stu-id="7d6a6-138">Access level for hello rule (Deny or Allow).</span></span>
   * <span data-ttu-id="7d6a6-139">**-p (lub--protokół)**.</span><span class="sxs-lookup"><span data-stu-id="7d6a6-139">**-p (or --protocol)**.</span></span> <span data-ttu-id="7d6a6-140">Protocol (Tcp, Udp lub *) hello reguły.</span><span class="sxs-lookup"><span data-stu-id="7d6a6-140">Protocol (Tcp, Udp, or *) for hello rule.</span></span>
   * <span data-ttu-id="7d6a6-141">**-r (lub--kierunek)**.</span><span class="sxs-lookup"><span data-stu-id="7d6a6-141">**-r (or --direction)**.</span></span> <span data-ttu-id="7d6a6-142">Kierunek połączenia (przychodzący lub wychodzący).</span><span class="sxs-lookup"><span data-stu-id="7d6a6-142">Direction of connection (Inbound or Outbound).</span></span>
   * <span data-ttu-id="7d6a6-143">**-y (lub--priorytetu)**.</span><span class="sxs-lookup"><span data-stu-id="7d6a6-143">**-y (or --priority)**.</span></span> <span data-ttu-id="7d6a6-144">Priorytet reguły hello.</span><span class="sxs-lookup"><span data-stu-id="7d6a6-144">Priority for hello rule.</span></span>
   * <span data-ttu-id="7d6a6-145">**-f (lub--prefiks adresu źródłowego)**.</span><span class="sxs-lookup"><span data-stu-id="7d6a6-145">**-f (or --source-address-prefix)**.</span></span> <span data-ttu-id="7d6a6-146">Prefiks adresu źródłowego CIDR lub przy użyciu znaczników domyślnych.</span><span class="sxs-lookup"><span data-stu-id="7d6a6-146">Source address prefix in CIDR or using default tags.</span></span>
   * <span data-ttu-id="7d6a6-147">**-o (lub--zakres portów źródłowych)**.</span><span class="sxs-lookup"><span data-stu-id="7d6a6-147">**-o (or --source-port-range)**.</span></span> <span data-ttu-id="7d6a6-148">Port źródłowy, lub zakresem portów.</span><span class="sxs-lookup"><span data-stu-id="7d6a6-148">Source port, or port range.</span></span>
   * <span data-ttu-id="7d6a6-149">**-e (lub--prefiks adresu docelowego)**.</span><span class="sxs-lookup"><span data-stu-id="7d6a6-149">**-e (or --destination-address-prefix)**.</span></span> <span data-ttu-id="7d6a6-150">Prefiks adresu docelowego w CIDR lub przy użyciu znaczników domyślnych.</span><span class="sxs-lookup"><span data-stu-id="7d6a6-150">Destination address prefix in CIDR or using default tags.</span></span>
   * <span data-ttu-id="7d6a6-151">**-u (lub--zakres portów docelowych)**.</span><span class="sxs-lookup"><span data-stu-id="7d6a6-151">**-u (or --destination-port-range)**.</span></span> <span data-ttu-id="7d6a6-152">Port docelowy, lub zakresem portów.</span><span class="sxs-lookup"><span data-stu-id="7d6a6-152">Destination port, or port range.</span></span>    
5. <span data-ttu-id="7d6a6-153">Uruchom hello **Tworzenie reguły nsg sieć platformy azure** toocreate polecenia regułę, która umożliwia dostęp tooport 80 (HTTP) z hello Internet.</span><span class="sxs-lookup"><span data-stu-id="7d6a6-153">Run hello **azure network nsg rule create** command toocreate a rule that allows access tooport 80 (HTTP) from hello Internet.</span></span>
   
        azure network nsg rule create -g TestRG -a NSG-FrontEnd -n web-rule -c Allow -p Tcp -r Inbound -y 200 -f Internet -o * -e * -u 80
   
    <span data-ttu-id="7d6a6-154">Oczekiwano putput:</span><span class="sxs-lookup"><span data-stu-id="7d6a6-154">Expected putput:</span></span>
   
        info:    Executing command network nsg rule create
        info:    Looking up hello network security rule "web-rule"
        info:    Creating a network security rule "web-rule"
        info:    Looking up hello network security group "NSG-FrontEnd"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/
        networkSecurityGroups/NSG-FrontEnd/securityRules/web-rule
        data:    Name                            : web-rule
        data:    Type                            : Microsoft.Network/networkSecurityGroups/securityRules
        data:    Provisioning state              : Succeeded
        data:    Source IP                       : Internet
        data:    Source Port                     : *
        data:    Destination IP                  : *
        data:    Destination Port                : 80
        data:    Protocol                        : Tcp
        data:    Direction                       : Inbound
        data:    Access                          : Allow
        data:    Priority                        : 200
        info:    network nsg rule create command OK
6. <span data-ttu-id="7d6a6-155">Uruchom hello **zestaw podsieci sieci wirtualnej platformy azure sieciowej** podsieci frontonu toohello polecenia toolink hello NSG.</span><span class="sxs-lookup"><span data-stu-id="7d6a6-155">Run hello **azure network vnet subnet set** command toolink hello NSG toohello front end subnet.</span></span>
   
        azure network vnet subnet set -g TestRG -e TestVNet -n FrontEnd -o NSG-FrontEnd
   
    <span data-ttu-id="7d6a6-156">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="7d6a6-156">Expected output:</span></span>
   
        info:    Executing command network vnet subnet set
        info:    Looking up hello subnet "FrontEnd"
        info:    Looking up hello network security group "NSG-FrontEnd"
        info:    Setting subnet "FrontEnd"
        info:    Looking up hello subnet "FrontEnd"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/
        virtualNetworks/TestVNet/subnets/FrontEnd
        data:    Type                            : Microsoft.Network/virtualNetworks/subnets
        data:    ProvisioningState               : Succeeded
        data:    Name                            : FrontEnd
        data:    Address prefix                  : 192.168.1.0/24
        data:    Network security group          : [object Object]
        data:    IP configurations:
        data:      /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNICWeb2/ip
        Configurations/ipconfig1
        data:      /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNICWeb1/ip
        Configurations/ipconfig1
        data:    
        info:    network vnet subnet set command OK

## <a name="how-toocreate-hello-nsg-for-hello-back-end-subnet"></a><span data-ttu-id="7d6a6-157">Jak hello toocreate NSG dla ponownie hello kończyć podsieci</span><span class="sxs-lookup"><span data-stu-id="7d6a6-157">How toocreate hello NSG for hello back end subnet</span></span>
<span data-ttu-id="7d6a6-158">toocreate o nazwie grupy NSG o nazwie *zaplecza NSG* oparte na powyższym scenariuszu hello, wykonaj poniższe kroki hello.</span><span class="sxs-lookup"><span data-stu-id="7d6a6-158">toocreate an NSG named named *NSG-BackEnd* based on hello scenario above, follow hello steps below.</span></span>

1. <span data-ttu-id="7d6a6-159">Uruchom hello **utworzyć sieć platformy azure nsg** toocreate polecenia grupy NSG.</span><span class="sxs-lookup"><span data-stu-id="7d6a6-159">Run hello **azure network nsg create** command toocreate an NSG.</span></span>
   
        azure network nsg create -g TestRG -l westus -n NSG-BackEnd
   
    <span data-ttu-id="7d6a6-160">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="7d6a6-160">Expected output:</span></span>
   
        info:    Executing command network nsg create
        info:    Looking up hello network security group "NSG-BackEnd"
        info:    Creating a network security group "NSG-BackEnd"
        info:    Looking up hello network security group "NSG-BackEnd"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/
        networkSecurityGroups/NSG-BackEnd
        data:    Name                            : NSG-BackEnd
        data:    Type                            : Microsoft.Network/networkSecurityGroups
        data:    Location                        : westus
        data:    Provisioning state              : Succeeded
        data:    Security group rules:
        data:    Name                           Source IP          Source Port  Destination IP  Destination Port  Protocol  Direction  Access  Priority
        data:    -----------------------------  -----------------  -----------  --------------  ----------------  --------  ---------  ------  --------
        data:    AllowVnetInBound               VirtualNetwork     *            VirtualNetwork  *                 *         Inbound    Allow   65000   
        data:    AllowAzureLoadBalancerInBound  AzureLoadBalancer  *            *               *                 *         Inbound    Allow   65001   
        data:    DenyAllInBound                 *                  *            *               *                 *         Inbound    Deny    65500   
        data:    AllowVnetOutBound              VirtualNetwork     *            VirtualNetwork  *                 *         Outbound   Allow   65000   
        data:    AllowInternetOutBound          *                  *            Internet        *                 *         Outbound   Allow   65001   
        data:    DenyAllOutBound                *                  *            *               *                 *         Outbound   Deny    65500   
        info:    network nsg create command OK
2. <span data-ttu-id="7d6a6-161">Uruchom hello **Tworzenie reguły nsg sieć platformy azure** toocreate polecenia regułę, która umożliwia dostęp tooport 1433 (SQL) z podsieci frontonu hello.</span><span class="sxs-lookup"><span data-stu-id="7d6a6-161">Run hello **azure network nsg rule create** command toocreate a rule that allows access tooport 1433 (SQL) from hello front end subnet.</span></span>
   
        azure network nsg rule create -g TestRG -a NSG-BackEnd -n sql-rule -c Allow -p Tcp -r Inbound -y 100 -f 192.168.1.0/24 -o * -e * -u 1433
   
    <span data-ttu-id="7d6a6-162">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="7d6a6-162">Expected output:</span></span>
   
        info:    Executing command network nsg rule create
        info:    Looking up hello network security rule "sql-rule"
        info:    Creating a network security rule "sql-rule"
        info:    Looking up hello network security group "NSG-BackEnd"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/
        networkSecurityGroups/NSG-BackEnd/securityRules/sql-rule
        data:    Name                            : sql-rule
        data:    Type                            : Microsoft.Network/networkSecurityGroups/securityRules
        data:    Provisioning state              : Succeeded
        data:    Source IP                       : 192.168.1.0/24
        data:    Source Port                     : *
        data:    Destination IP                  : *
        data:    Destination Port                : 1433
        data:    Protocol                        : Tcp
        data:    Direction                       : Inbound
        data:    Access                          : Allow
        data:    Priority                        : 100
        info:    network nsg rule create command OK
3. <span data-ttu-id="7d6a6-163">Uruchom hello **Tworzenie reguły nsg sieć platformy azure** toocreate polecenia regułę, która nie zezwala na toohello dostęp do Internetu z.</span><span class="sxs-lookup"><span data-stu-id="7d6a6-163">Run hello **azure network nsg rule create** command toocreate a rule that denies access toohello Internet from.</span></span>
   
        azure network nsg rule create -g TestRG -a NSG-BackEnd -n web-rule -c Deny -p * -r Outbound -y 200 -f * -o * -e Internet -u *
   
    <span data-ttu-id="7d6a6-164">Oczekiwano putput:</span><span class="sxs-lookup"><span data-stu-id="7d6a6-164">Expected putput:</span></span>
   
        info:    Executing command network nsg rule create
        info:    Looking up hello network security rule "web-rule"
        info:    Creating a network security rule "web-rule"
        info:    Looking up hello network security group "NSG-BackEnd"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/
        networkSecurityGroups/NSG-BackEnd/securityRules/web-rule
        data:    Name                            : web-rule
        data:    Type                            : Microsoft.Network/networkSecurityGroups/securityRules
        data:    Provisioning state              : Succeeded
        data:    Source IP                       : *
        data:    Source Port                     : *
        data:    Destination IP                  : Internet
        data:    Destination Port                : *
        data:    Protocol                        : *
        data:    Direction                       : Outbound
        data:    Access                          : Deny
        data:    Priority                        : 200
        info:    network nsg rule create command OK
4. <span data-ttu-id="7d6a6-165">Uruchom hello **zestaw podsieci sieci wirtualnej platformy azure sieciowej** polecenia toolink hello NSG toohello ponownie kończyć podsieci.</span><span class="sxs-lookup"><span data-stu-id="7d6a6-165">Run hello **azure network vnet subnet set** command toolink hello NSG toohello back end subnet.</span></span>
   
        azure network vnet subnet set -g TestRG -e TestVNet -n BackEnd -o NSG-BackEnd
   
    <span data-ttu-id="7d6a6-166">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="7d6a6-166">Expected output:</span></span>
   
        info:    Executing command network vnet subnet set
        info:    Looking up hello subnet "BackEnd"
        info:    Looking up hello network security group "NSG-BackEnd"
        info:    Setting subnet "BackEnd"
        info:    Looking up hello subnet "BackEnd"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/
        virtualNetworks/TestVNet/subnets/BackEnd
        data:    Type                            : Microsoft.Network/virtualNetworks/subnets
        data:    ProvisioningState               : Succeeded
        data:    Name                            : BackEnd
        data:    Address prefix                  : 192.168.2.0/24
        data:    Network security group          : [object Object]
        data:    IP configurations:
        data:      /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNICSQL1/ip
        Configurations/ipconfig1
        data:      /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNICSQL2/ip
        Configurations/ipconfig1
        data:    
        info:    network vnet subnet set command OK

