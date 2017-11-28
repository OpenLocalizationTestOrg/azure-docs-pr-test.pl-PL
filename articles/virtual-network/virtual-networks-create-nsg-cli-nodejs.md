---
title: "Utwórz grupy zabezpieczeń sieci - Azure CLI 1.0 | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak utworzyć i wdrożyć przy użyciu 1.0 interfejsu wiersza polecenia Azure grup zabezpieczeń sieci."
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
ms.openlocfilehash: ca8c182651e3c9f2f1f3a85b94361755d8e638d4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-network-security-groups-using-the-azure-cli-10"></a><span data-ttu-id="c1086-103">Tworzenie grup zabezpieczeń za pomocą 1.0 interfejsu wiersza polecenia platformy Azure w sieci</span><span class="sxs-lookup"><span data-stu-id="c1086-103">Create network security groups using the Azure CLI 1.0</span></span>


## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="c1086-104">Wersje interfejsu wiersza polecenia umożliwiające wykonanie zadania</span><span class="sxs-lookup"><span data-stu-id="c1086-104">CLI versions to complete the task</span></span> 

<span data-ttu-id="c1086-105">Zadanie można wykonać przy użyciu jednej z następujących wersji interfejsu wiersza polecenia:</span><span class="sxs-lookup"><span data-stu-id="c1086-105">You can complete the task using one of the following CLI versions:</span></span> 

- <span data-ttu-id="c1086-106">[Azure CLI 1.0](#how-to-create-the-nsg-for-the-front-end-subnet) — nasze interfejsu wiersza polecenia dla klasycznego i zasobów zarządzania wdrażania modeli (w tym artykule)</span><span class="sxs-lookup"><span data-stu-id="c1086-106">[Azure CLI 1.0](#how-to-create-the-nsg-for-the-front-end-subnet) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="c1086-107">[Azure CLI 2.0](virtual-networks-create-nsg-arm-cli.md) -CLI naszych następnej generacji dla model wdrażania zasobów zarządzania</span><span class="sxs-lookup"><span data-stu-id="c1086-107">[Azure CLI 2.0](virtual-networks-create-nsg-arm-cli.md) - our next-generation CLI for the resource management deployment model</span></span> 

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="c1086-108">W tym artykule opisano model wdrażania usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c1086-108">This article covers the Resource Manager deployment model.</span></span> <span data-ttu-id="c1086-109">Możesz również [tworzenia grup NSG w klasycznym modelu wdrażania](virtual-networks-create-nsg-classic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="c1086-109">You can also [create NSGs in the classic deployment model](virtual-networks-create-nsg-classic-cli.md).</span></span>

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

<span data-ttu-id="c1086-110">Poniższe przykładowe polecenia interfejsu wiersza polecenia Azure oczekiwać środowisku niezłożonym już utworzone w zależności od scenariusza powyżej.</span><span class="sxs-lookup"><span data-stu-id="c1086-110">The sample Azure CLI commands below expect a simple environment already created based on the scenario above.</span></span> 

## <a name="how-to-create-the-nsg-for-the-front-end-subnet"></a><span data-ttu-id="c1086-111">Jak utworzyć grupę NSG dla podsieci frontonu</span><span class="sxs-lookup"><span data-stu-id="c1086-111">How to create the NSG for the front end subnet</span></span>
<span data-ttu-id="c1086-112">Aby utworzyć grupy NSG o nazwie o nazwie *frontonu NSG* oparte na powyższym scenariuszu, wykonaj poniższe kroki.</span><span class="sxs-lookup"><span data-stu-id="c1086-112">To create an NSG named named *NSG-FrontEnd* based on the scenario above, follow the steps below.</span></span>

1. <span data-ttu-id="c1086-113">Jeśli po raz pierwszy używasz interfejsu wiersza polecenia Azure, zobacz artykuł [Instalowanie i konfigurowania interfejsu wiersza polecenia Azure](../cli-install-nodejs.md) i postępuj zgodnie z instrukcjami aż do punktu, w którym należy wybrać konto platformy Azure i subskrypcję.</span><span class="sxs-lookup"><span data-stu-id="c1086-113">If you have never used Azure CLI, see [Install and Configure the Azure CLI](../cli-install-nodejs.md) and follow the instructions up to the point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="c1086-114">Uruchom polecenie **azure config mode**, aby włączyć tryb Resource Manager, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="c1086-114">Run the **azure config mode** command to switch to Resource Manager mode, as shown below.</span></span>
   
        azure config mode arm
   
    <span data-ttu-id="c1086-115">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="c1086-115">Expected output:</span></span>
   
        info:    New mode is arm
3. <span data-ttu-id="c1086-116">Uruchom **utworzyć sieć platformy azure nsg** polecenie, aby utworzyć grupy NSG.</span><span class="sxs-lookup"><span data-stu-id="c1086-116">Run the **azure network nsg create** command to create an NSG.</span></span>
   
        azure network nsg create -g TestRG -l westus -n NSG-FrontEnd
   
    <span data-ttu-id="c1086-117">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="c1086-117">Expected output:</span></span>
   
        info:    Executing command network nsg create
        info:    Looking up the network security group "NSG-FrontEnd"
        info:    Creating a network security group "NSG-FrontEnd"
        info:    Looking up the network security group "NSG-FrontEnd"
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
   
    <span data-ttu-id="c1086-118">Parametry:</span><span class="sxs-lookup"><span data-stu-id="c1086-118">Parameters:</span></span>
   
   * <span data-ttu-id="c1086-119">**-g (lub --resource-group)**.</span><span class="sxs-lookup"><span data-stu-id="c1086-119">**-g (or --resource-group)**.</span></span> <span data-ttu-id="c1086-120">Nazwa grupy zasobów, w której zostanie utworzona grupa NSG.</span><span class="sxs-lookup"><span data-stu-id="c1086-120">Name of the resource group where the NSG will be created.</span></span> <span data-ttu-id="c1086-121">W naszym scenariuszu jest to *TestRG*.</span><span class="sxs-lookup"><span data-stu-id="c1086-121">For our scenario, *TestRG*.</span></span>
   * <span data-ttu-id="c1086-122">**-l (lub --location)**.</span><span class="sxs-lookup"><span data-stu-id="c1086-122">**-l (or --location)**.</span></span> <span data-ttu-id="c1086-123">Region platformy Azure, w którym zostanie utworzona nowa grupa NSG.</span><span class="sxs-lookup"><span data-stu-id="c1086-123">Azure region where the new NSG will be created.</span></span> <span data-ttu-id="c1086-124">W naszym scenariuszu *westus*.</span><span class="sxs-lookup"><span data-stu-id="c1086-124">For our scenario, *westus*.</span></span>
   * <span data-ttu-id="c1086-125">**-n (lub --name)**.</span><span class="sxs-lookup"><span data-stu-id="c1086-125">**-n (or --name)**.</span></span> <span data-ttu-id="c1086-126">Nazwa nowej grupy NSG.</span><span class="sxs-lookup"><span data-stu-id="c1086-126">Name for the new NSG.</span></span> <span data-ttu-id="c1086-127">W naszym scenariuszu *frontonu NSG*.</span><span class="sxs-lookup"><span data-stu-id="c1086-127">For our scenario, *NSG-FrontEnd*.</span></span>
4. <span data-ttu-id="c1086-128">Uruchom **Tworzenie reguły nsg sieć platformy azure** polecenie, aby utworzyć regułę, która zezwala na dostęp do portu 3389 (RDP) z Internetu.</span><span class="sxs-lookup"><span data-stu-id="c1086-128">Run the **azure network nsg rule create** command to create a rule that allows access to port 3389 (RDP) from the Internet.</span></span>
   
        azure network nsg rule create -g TestRG -a NSG-FrontEnd -n rdp-rule -c Allow -p Tcp -r Inbound -y 100 -f Internet -o * -e * -u 3389
   
    <span data-ttu-id="c1086-129">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="c1086-129">Expected output:</span></span>
   
        info:    Executing command network nsg rule create
        warn:    Using default direction: Inbound
        info:    Looking up the network security rule "rdp-rule"
        info:    Creating a network security rule "rdp-rule"
        info:    Looking up the network security group "NSG-FrontEnd"
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
   
    <span data-ttu-id="c1086-130">Parametry:</span><span class="sxs-lookup"><span data-stu-id="c1086-130">Parameters:</span></span>
   
   * <span data-ttu-id="c1086-131">**-nazwę (lub--nsg —)**.</span><span class="sxs-lookup"><span data-stu-id="c1086-131">**-a (or --nsg-name)**.</span></span> <span data-ttu-id="c1086-132">Nazwa grupy NSG, w którym zostaną utworzone reguły.</span><span class="sxs-lookup"><span data-stu-id="c1086-132">Name of the NSG in which the rule will be created.</span></span> <span data-ttu-id="c1086-133">W naszym scenariuszu *frontonu NSG*.</span><span class="sxs-lookup"><span data-stu-id="c1086-133">For our scenario, *NSG-FrontEnd*.</span></span>
   * <span data-ttu-id="c1086-134">**-n (lub --name)**.</span><span class="sxs-lookup"><span data-stu-id="c1086-134">**-n (or --name)**.</span></span> <span data-ttu-id="c1086-135">Nazwa nowej reguły.</span><span class="sxs-lookup"><span data-stu-id="c1086-135">Name for the new rule.</span></span> <span data-ttu-id="c1086-136">W naszym scenariuszu *reguły protokołu rdp*.</span><span class="sxs-lookup"><span data-stu-id="c1086-136">For our scenario, *rdp-rule*.</span></span>
   * <span data-ttu-id="c1086-137">**-c (lub--dostępu)**.</span><span class="sxs-lookup"><span data-stu-id="c1086-137">**-c (or --access)**.</span></span> <span data-ttu-id="c1086-138">Poziom dostępu dla reguły (Deny lub Zezwalaj).</span><span class="sxs-lookup"><span data-stu-id="c1086-138">Access level for the rule (Deny or Allow).</span></span>
   * <span data-ttu-id="c1086-139">**-p (lub--protokół)**.</span><span class="sxs-lookup"><span data-stu-id="c1086-139">**-p (or --protocol)**.</span></span> <span data-ttu-id="c1086-140">Protocol (Tcp, Udp lub *) dla reguły.</span><span class="sxs-lookup"><span data-stu-id="c1086-140">Protocol (Tcp, Udp, or *) for the rule.</span></span>
   * <span data-ttu-id="c1086-141">**-r (lub--kierunek)**.</span><span class="sxs-lookup"><span data-stu-id="c1086-141">**-r (or --direction)**.</span></span> <span data-ttu-id="c1086-142">Kierunek połączenia (przychodzący lub wychodzący).</span><span class="sxs-lookup"><span data-stu-id="c1086-142">Direction of connection (Inbound or Outbound).</span></span>
   * <span data-ttu-id="c1086-143">**-y (lub--priorytetu)**.</span><span class="sxs-lookup"><span data-stu-id="c1086-143">**-y (or --priority)**.</span></span> <span data-ttu-id="c1086-144">Priorytet reguły.</span><span class="sxs-lookup"><span data-stu-id="c1086-144">Priority for the rule.</span></span>
   * <span data-ttu-id="c1086-145">**-f (lub--prefiks adresu źródłowego)**.</span><span class="sxs-lookup"><span data-stu-id="c1086-145">**-f (or --source-address-prefix)**.</span></span> <span data-ttu-id="c1086-146">Prefiks adresu źródłowego CIDR lub przy użyciu znaczników domyślnych.</span><span class="sxs-lookup"><span data-stu-id="c1086-146">Source address prefix in CIDR or using default tags.</span></span>
   * <span data-ttu-id="c1086-147">**-o (lub--zakres portów źródłowych)**.</span><span class="sxs-lookup"><span data-stu-id="c1086-147">**-o (or --source-port-range)**.</span></span> <span data-ttu-id="c1086-148">Port źródłowy, lub zakresem portów.</span><span class="sxs-lookup"><span data-stu-id="c1086-148">Source port, or port range.</span></span>
   * <span data-ttu-id="c1086-149">**-e (lub--prefiks adresu docelowego)**.</span><span class="sxs-lookup"><span data-stu-id="c1086-149">**-e (or --destination-address-prefix)**.</span></span> <span data-ttu-id="c1086-150">Prefiks adresu docelowego w CIDR lub przy użyciu znaczników domyślnych.</span><span class="sxs-lookup"><span data-stu-id="c1086-150">Destination address prefix in CIDR or using default tags.</span></span>
   * <span data-ttu-id="c1086-151">**-u (lub--zakres portów docelowych)**.</span><span class="sxs-lookup"><span data-stu-id="c1086-151">**-u (or --destination-port-range)**.</span></span> <span data-ttu-id="c1086-152">Port docelowy, lub zakresem portów.</span><span class="sxs-lookup"><span data-stu-id="c1086-152">Destination port, or port range.</span></span>    
5. <span data-ttu-id="c1086-153">Uruchom **Tworzenie reguły nsg sieć platformy azure** polecenie, aby utworzyć regułę, która zezwala na dostęp do portu 80 (HTTP) z Internetu.</span><span class="sxs-lookup"><span data-stu-id="c1086-153">Run the **azure network nsg rule create** command to create a rule that allows access to port 80 (HTTP) from the Internet.</span></span>
   
        azure network nsg rule create -g TestRG -a NSG-FrontEnd -n web-rule -c Allow -p Tcp -r Inbound -y 200 -f Internet -o * -e * -u 80
   
    <span data-ttu-id="c1086-154">Oczekiwano putput:</span><span class="sxs-lookup"><span data-stu-id="c1086-154">Expected putput:</span></span>
   
        info:    Executing command network nsg rule create
        info:    Looking up the network security rule "web-rule"
        info:    Creating a network security rule "web-rule"
        info:    Looking up the network security group "NSG-FrontEnd"
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
6. <span data-ttu-id="c1086-155">Uruchom **zestaw podsieci sieci wirtualnej platformy azure sieciowej** poleceń połączyć grupy NSG do podsieci frontonu.</span><span class="sxs-lookup"><span data-stu-id="c1086-155">Run the **azure network vnet subnet set** command to link the NSG to the front end subnet.</span></span>
   
        azure network vnet subnet set -g TestRG -e TestVNet -n FrontEnd -o NSG-FrontEnd
   
    <span data-ttu-id="c1086-156">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="c1086-156">Expected output:</span></span>
   
        info:    Executing command network vnet subnet set
        info:    Looking up the subnet "FrontEnd"
        info:    Looking up the network security group "NSG-FrontEnd"
        info:    Setting subnet "FrontEnd"
        info:    Looking up the subnet "FrontEnd"
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

## <a name="how-to-create-the-nsg-for-the-back-end-subnet"></a><span data-ttu-id="c1086-157">Jak utworzyć grupę NSG podsieci wewnętrznej</span><span class="sxs-lookup"><span data-stu-id="c1086-157">How to create the NSG for the back end subnet</span></span>
<span data-ttu-id="c1086-158">Aby utworzyć grupy NSG o nazwie o nazwie *zaplecza NSG* oparte na powyższym scenariuszu, wykonaj poniższe kroki.</span><span class="sxs-lookup"><span data-stu-id="c1086-158">To create an NSG named named *NSG-BackEnd* based on the scenario above, follow the steps below.</span></span>

1. <span data-ttu-id="c1086-159">Uruchom **utworzyć sieć platformy azure nsg** polecenie, aby utworzyć grupy NSG.</span><span class="sxs-lookup"><span data-stu-id="c1086-159">Run the **azure network nsg create** command to create an NSG.</span></span>
   
        azure network nsg create -g TestRG -l westus -n NSG-BackEnd
   
    <span data-ttu-id="c1086-160">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="c1086-160">Expected output:</span></span>
   
        info:    Executing command network nsg create
        info:    Looking up the network security group "NSG-BackEnd"
        info:    Creating a network security group "NSG-BackEnd"
        info:    Looking up the network security group "NSG-BackEnd"
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
2. <span data-ttu-id="c1086-161">Uruchom **Tworzenie reguły nsg sieć platformy azure** polecenie, aby utworzyć regułę, która umożliwia dostęp do portu 1433 (SQL) z podsieci frontonu.</span><span class="sxs-lookup"><span data-stu-id="c1086-161">Run the **azure network nsg rule create** command to create a rule that allows access to port 1433 (SQL) from the front end subnet.</span></span>
   
        azure network nsg rule create -g TestRG -a NSG-BackEnd -n sql-rule -c Allow -p Tcp -r Inbound -y 100 -f 192.168.1.0/24 -o * -e * -u 1433
   
    <span data-ttu-id="c1086-162">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="c1086-162">Expected output:</span></span>
   
        info:    Executing command network nsg rule create
        info:    Looking up the network security rule "sql-rule"
        info:    Creating a network security rule "sql-rule"
        info:    Looking up the network security group "NSG-BackEnd"
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
3. <span data-ttu-id="c1086-163">Uruchom **Tworzenie reguły nsg sieć platformy azure** polecenie, aby utworzyć regułę, która nie zezwala na dostęp do Internetu za pomocą.</span><span class="sxs-lookup"><span data-stu-id="c1086-163">Run the **azure network nsg rule create** command to create a rule that denies access to the Internet from.</span></span>
   
        azure network nsg rule create -g TestRG -a NSG-BackEnd -n web-rule -c Deny -p * -r Outbound -y 200 -f * -o * -e Internet -u *
   
    <span data-ttu-id="c1086-164">Oczekiwano putput:</span><span class="sxs-lookup"><span data-stu-id="c1086-164">Expected putput:</span></span>
   
        info:    Executing command network nsg rule create
        info:    Looking up the network security rule "web-rule"
        info:    Creating a network security rule "web-rule"
        info:    Looking up the network security group "NSG-BackEnd"
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
4. <span data-ttu-id="c1086-165">Uruchom **zestaw podsieci sieci wirtualnej platformy azure sieciowej** poleceń połączyć grupy NSG podsieci wewnętrznej.</span><span class="sxs-lookup"><span data-stu-id="c1086-165">Run the **azure network vnet subnet set** command to link the NSG to the back end subnet.</span></span>
   
        azure network vnet subnet set -g TestRG -e TestVNet -n BackEnd -o NSG-BackEnd
   
    <span data-ttu-id="c1086-166">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="c1086-166">Expected output:</span></span>
   
        info:    Executing command network vnet subnet set
        info:    Looking up the subnet "BackEnd"
        info:    Looking up the network security group "NSG-BackEnd"
        info:    Setting subnet "BackEnd"
        info:    Looking up the subnet "BackEnd"
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

