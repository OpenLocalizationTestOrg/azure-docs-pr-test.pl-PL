---
title: "aaaHow toocreate grup NSG w klasycznym trybie przy użyciu hello Azure CLI | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate i wdrażanie grup NSG w klasycznym trybie przy użyciu hello wiersza polecenia platformy Azure"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
tags: azure-service-management
ms.assetid: 17d98950-5fbb-4653-bef6-d822ab37541e
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.openlocfilehash: eb78861e10a0dd950bb2c3783ee957d1cce55016
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-nsgs-classic-in-hello-azure-cli"></a><span data-ttu-id="f171b-103">Jak grupy NSG toocreate (klasyczne) w hello wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="f171b-103">How toocreate NSGs (classic) in hello Azure CLI</span></span>
[!INCLUDE [virtual-networks-create-nsg-selectors-classic-include](../../includes/virtual-networks-create-nsg-selectors-classic-include.md)]

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="f171b-104">W tym artykule omówiono hello klasycznego modelu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="f171b-104">This article covers hello classic deployment model.</span></span> <span data-ttu-id="f171b-105">Możesz również [tworzenia grup NSG w modelu wdrażania usługi Resource Manager hello](virtual-networks-create-nsg-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="f171b-105">You can also [create NSGs in hello Resource Manager deployment model](virtual-networks-create-nsg-arm-cli.md).</span></span>

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

<span data-ttu-id="f171b-106">Poniższe polecenia interfejsu wiersza polecenia Azure próbki Hello oczekiwać środowisku niezłożonym już utworzone w zależności od scenariusza hello powyżej.</span><span class="sxs-lookup"><span data-stu-id="f171b-106">hello sample Azure CLI commands below expect a simple environment already created based on hello scenario above.</span></span> <span data-ttu-id="f171b-107">Jeśli chcesz korzystać z poleceń hello toorun wyświetlaną w tym dokumencie, najpierw utworzyć środowisko testowe hello przez [tworzenia sieci wirtualnej](virtual-networks-create-vnet-classic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="f171b-107">If you want toorun hello commands as they are displayed in this document, first build hello test environment by [creating a VNet](virtual-networks-create-vnet-classic-cli.md).</span></span>

## <a name="how-toocreate-hello-nsg-for-hello-front-end-subnet"></a><span data-ttu-id="f171b-108">Jak toocreate hello NSG dla podsieci frontonu hello</span><span class="sxs-lookup"><span data-stu-id="f171b-108">How toocreate hello NSG for hello front end subnet</span></span>
<span data-ttu-id="f171b-109">toocreate o nazwie grupy NSG o nazwie **frontonu NSG** oparte na powyższym scenariuszu hello, wykonaj poniższe kroki hello.</span><span class="sxs-lookup"><span data-stu-id="f171b-109">toocreate an NSG named named **NSG-FrontEnd** based on hello scenario above, follow hello steps below.</span></span>

1. <span data-ttu-id="f171b-110">Jeśli po raz pierwszy używasz interfejsu wiersza polecenia Azure, zobacz [Instalowanie i Konfigurowanie interfejsu wiersza polecenia Azure hello](../cli-install-nodejs.md) i wykonaj instrukcje hello zapasowej punktu toohello, gdzie należy wybrać konto platformy Azure i subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="f171b-110">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="f171b-111">Uruchom hello  **`azure config mode`**  polecenia tooswitch tooclassic tryb, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="f171b-111">Run hello **`azure config mode`** command tooswitch tooclassic mode, as shown below.</span></span>
   
        azure config mode asm
   
    <span data-ttu-id="f171b-112">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="f171b-112">Expected output:</span></span>
   
        info:    New mode is asm
3. <span data-ttu-id="f171b-113">Uruchom hello  **`azure network nsg create`**  toocreate polecenia grupy NSG.</span><span class="sxs-lookup"><span data-stu-id="f171b-113">Run hello **`azure network nsg create`** command toocreate an NSG.</span></span>
   
        azure network nsg create -l uswest -n NSG-FrontEnd
   
    <span data-ttu-id="f171b-114">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="f171b-114">Expected output:</span></span>
   
        info:    Executing command network nsg create
        info:    Creating a network security group "NSG-FrontEnd"
        info:    Looking up hello network security group "NSG-FrontEnd"
        data:    Name                            : NSG-FrontEnd
        data:    Location                        : West US
        data:    Security group rules:
        data:    Name                               Source IP           Source Port  Destination IP   Destination Port  Protocol  Type      Action  Prior
        ity  Default
        data:    ---------------------------------  ------------------  -----------  ---------------  ----------------  --------  --------  ------  -----
        ---  -------
        data:    ALLOW VNET OUTBOUND                VIRTUAL_NETWORK     *            VIRTUAL_NETWORK  *                 *         Outbound  Allow   65000
             true   
        data:    ALLOW VNET INBOUND                 VIRTUAL_NETWORK     *            VIRTUAL_NETWORK  *                 *         Inbound   Allow   65000
             true   
        data:    ALLOW AZURE LOAD BALANCER INBOUND  AZURE_LOADBALANCER  *            *                *                 *         Inbound   Allow   65001
             true   
        data:    ALLOW INTERNET OUTBOUND            *                   *            INTERNET         *                 *         Outbound  Allow   65001
             true   
        data:    DENY ALL OUTBOUND                  *                   *            *                *                 *         Outbound  Deny    65500
             true   
        data:    DENY ALL INBOUND                   *                   *            *                *                 *         Inbound   Deny    65500
             true   
        info:    network nsg create command OK
   
    <span data-ttu-id="f171b-115">Parametry:</span><span class="sxs-lookup"><span data-stu-id="f171b-115">Parameters:</span></span>
   
   * <span data-ttu-id="f171b-116">**-l (lub --location)**.</span><span class="sxs-lookup"><span data-stu-id="f171b-116">**-l (or --location)**.</span></span> <span data-ttu-id="f171b-117">Region platformy Azure, której hello Nowa grupa NSG zostanie utworzona.</span><span class="sxs-lookup"><span data-stu-id="f171b-117">Azure region where hello new NSG will be created.</span></span> <span data-ttu-id="f171b-118">W naszym scenariuszu *westus*.</span><span class="sxs-lookup"><span data-stu-id="f171b-118">For our scenario, *westus*.</span></span>
   * <span data-ttu-id="f171b-119">**-n (lub --name)**.</span><span class="sxs-lookup"><span data-stu-id="f171b-119">**-n (or --name)**.</span></span> <span data-ttu-id="f171b-120">Nazwa hello Nowa grupa NSG.</span><span class="sxs-lookup"><span data-stu-id="f171b-120">Name for hello new NSG.</span></span> <span data-ttu-id="f171b-121">W naszym scenariuszu *frontonu NSG*.</span><span class="sxs-lookup"><span data-stu-id="f171b-121">For our scenario, *NSG-FrontEnd*.</span></span>
4. <span data-ttu-id="f171b-122">Uruchom hello  **`azure network nsg rule create`**  toocreate polecenia regułę, która umożliwia dostęp tooport 3389 (RDP) z hello Internet.</span><span class="sxs-lookup"><span data-stu-id="f171b-122">Run hello **`azure network nsg rule create`** command toocreate a rule that allows access tooport 3389 (RDP) from hello Internet.</span></span>
   
        azure network nsg rule create -a NSG-FrontEnd -n rdp-rule -c Allow -p Tcp -r Inbound -y 100 -f Internet -o * -e * -u 3389
   
    <span data-ttu-id="f171b-123">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="f171b-123">Expected output:</span></span>
   
        info:    Executing command network nsg rule create
        info:    Looking up hello network security group "NSG-FrontEnd"
        info:    Creating a network security rule "rdp-rule"
        info:    Looking up hello network security group "NSG-FrontEnd"
        data:    Name                            : rdp-rule
        data:    Source address prefix           : INTERNET
        data:    Source Port                     : *
        data:    Destination address prefix      : *
        data:    Destination Port                : 3389
        data:    Protocol                        : TCP
        data:    Type                            : Inbound
        data:    Action                          : Allow
        data:    Priority                        : 100
        info:    network nsg rule create command OK
   
    <span data-ttu-id="f171b-124">Parametry:</span><span class="sxs-lookup"><span data-stu-id="f171b-124">Parameters:</span></span>
   
   * <span data-ttu-id="f171b-125">**-nazwę (lub--nsg —)**.</span><span class="sxs-lookup"><span data-stu-id="f171b-125">**-a (or --nsg-name)**.</span></span> <span data-ttu-id="f171b-126">Nazwa grupy NSG hello, w których hello reguła zostanie utworzona.</span><span class="sxs-lookup"><span data-stu-id="f171b-126">Name of hello NSG in which hello rule will be created.</span></span> <span data-ttu-id="f171b-127">W naszym scenariuszu *frontonu NSG*.</span><span class="sxs-lookup"><span data-stu-id="f171b-127">For our scenario, *NSG-FrontEnd*.</span></span>
   * <span data-ttu-id="f171b-128">**-n (lub --name)**.</span><span class="sxs-lookup"><span data-stu-id="f171b-128">**-n (or --name)**.</span></span> <span data-ttu-id="f171b-129">Nazwa nowej reguły hello.</span><span class="sxs-lookup"><span data-stu-id="f171b-129">Name for hello new rule.</span></span> <span data-ttu-id="f171b-130">W naszym scenariuszu *reguły protokołu rdp*.</span><span class="sxs-lookup"><span data-stu-id="f171b-130">For our scenario, *rdp-rule*.</span></span>
   * <span data-ttu-id="f171b-131">**-c (lub--akcji)**.</span><span class="sxs-lookup"><span data-stu-id="f171b-131">**-c (or --action)**.</span></span> <span data-ttu-id="f171b-132">Poziom dostępu dla reguły hello (Deny lub Zezwalaj).</span><span class="sxs-lookup"><span data-stu-id="f171b-132">Access level for hello rule (Deny or Allow).</span></span>
   * <span data-ttu-id="f171b-133">**-p (lub--protokół)**.</span><span class="sxs-lookup"><span data-stu-id="f171b-133">**-p (or --protocol)**.</span></span> <span data-ttu-id="f171b-134">Protocol (Tcp, Udp lub *) hello reguły.</span><span class="sxs-lookup"><span data-stu-id="f171b-134">Protocol (Tcp, Udp, or *) for hello rule.</span></span>
   * <span data-ttu-id="f171b-135">**-r (lub--typ)**.</span><span class="sxs-lookup"><span data-stu-id="f171b-135">**-r (or --type)**.</span></span> <span data-ttu-id="f171b-136">Kierunek połączenia (przychodzący lub wychodzący).</span><span class="sxs-lookup"><span data-stu-id="f171b-136">Direction of connection (Inbound or Outbound).</span></span>
   * <span data-ttu-id="f171b-137">**-y (lub--priorytetu)**.</span><span class="sxs-lookup"><span data-stu-id="f171b-137">**-y (or --priority)**.</span></span> <span data-ttu-id="f171b-138">Priorytet reguły hello.</span><span class="sxs-lookup"><span data-stu-id="f171b-138">Priority for hello rule.</span></span>
   * <span data-ttu-id="f171b-139">**-f (lub--prefiks adresu źródłowego)**.</span><span class="sxs-lookup"><span data-stu-id="f171b-139">**-f (or --source-address-prefix)**.</span></span> <span data-ttu-id="f171b-140">Prefiks adresu źródłowego CIDR lub przy użyciu znaczników domyślnych.</span><span class="sxs-lookup"><span data-stu-id="f171b-140">Source address prefix in CIDR or using default tags.</span></span>
   * <span data-ttu-id="f171b-141">**-o (lub--zakres portów źródłowych)**.</span><span class="sxs-lookup"><span data-stu-id="f171b-141">**-o (or --source-port-range)**.</span></span> <span data-ttu-id="f171b-142">Port źródłowy, lub zakresem portów.</span><span class="sxs-lookup"><span data-stu-id="f171b-142">Source port, or port range.</span></span>
   * <span data-ttu-id="f171b-143">**-e (lub--prefiks adresu docelowego)**.</span><span class="sxs-lookup"><span data-stu-id="f171b-143">**-e (or --destination-address-prefix)**.</span></span> <span data-ttu-id="f171b-144">Prefiks adresu docelowego w CIDR lub przy użyciu znaczników domyślnych.</span><span class="sxs-lookup"><span data-stu-id="f171b-144">Destination address prefix in CIDR or using default tags.</span></span>
   * <span data-ttu-id="f171b-145">**-u (lub--zakres portów docelowych)**.</span><span class="sxs-lookup"><span data-stu-id="f171b-145">**-u (or --destination-port-range)**.</span></span> <span data-ttu-id="f171b-146">Port docelowy, lub zakresem portów.</span><span class="sxs-lookup"><span data-stu-id="f171b-146">Destination port, or port range.</span></span>
5. <span data-ttu-id="f171b-147">Uruchom hello  **`azure network nsg rule create`**  toocreate polecenia regułę, która umożliwia dostęp tooport 80 (HTTP) z hello Internet.</span><span class="sxs-lookup"><span data-stu-id="f171b-147">Run hello **`azure network nsg rule create`** command toocreate a rule that allows access tooport 80 (HTTP) from hello Internet.</span></span>
   
        azure network nsg rule create -a NSG-FrontEnd -n web-rule -c Allow -p Tcp -r Inbound -y 200 -f Internet -o * -e * -u 80
   
    <span data-ttu-id="f171b-148">Oczekiwano putput:</span><span class="sxs-lookup"><span data-stu-id="f171b-148">Expected putput:</span></span>
   
        info:    Executing command network nsg rule create
        info:    Looking up hello network security group "NSG-FrontEnd"
        info:    Creating a network security rule "web-rule"
        info:    Looking up hello network security group "NSG-FrontEnd"
        data:    Name                            : web-rule
        data:    Source address prefix           : INTERNET
        data:    Source Port                     : *
        data:    Destination address prefix      : *
        data:    Destination Port                : 80
        data:    Protocol                        : TCP
        data:    Type                            : Inbound
        data:    Action                          : Allow
        data:    Priority                        : 200
        info:    network nsg rule create command OK
6. <span data-ttu-id="f171b-149">Uruchom hello  **`azure network nsg subnet add`**  podsieci frontonu toohello polecenia toolink hello NSG.</span><span class="sxs-lookup"><span data-stu-id="f171b-149">Run hello **`azure network nsg subnet add`** command toolink hello NSG toohello front end subnet.</span></span>
   
        azure network nsg subnet add -a NSG-FrontEnd --vnet-name TestVNet --subnet-name FrontEnd
   
    <span data-ttu-id="f171b-150">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="f171b-150">Expected output:</span></span>
   
        info:    Executing command network nsg subnet add
        info:    Looking up hello network security group "NSG-FrontEnd"
        info:    Looking up hello subnet "FrontEnd"
        info:    Looking up network configuration
        info:    Creating a network security group "NSG-FrontEnd"
        info:    network nsg subnet add command OK

## <a name="how-toocreate-hello-nsg-for-hello-back-end-subnet"></a><span data-ttu-id="f171b-151">Jak hello toocreate NSG dla ponownie hello kończyć podsieci</span><span class="sxs-lookup"><span data-stu-id="f171b-151">How toocreate hello NSG for hello back end subnet</span></span>
<span data-ttu-id="f171b-152">toocreate o nazwie grupy NSG o nazwie *zaplecza NSG* oparte na powyższym scenariuszu hello, wykonaj poniższe kroki hello.</span><span class="sxs-lookup"><span data-stu-id="f171b-152">toocreate an NSG named named *NSG-BackEnd* based on hello scenario above, follow hello steps below.</span></span>

1. <span data-ttu-id="f171b-153">Uruchom hello  **`azure network nsg create`**  toocreate polecenia grupy NSG.</span><span class="sxs-lookup"><span data-stu-id="f171b-153">Run hello **`azure network nsg create`** command toocreate an NSG.</span></span>
   
        azure network nsg create -l uswest -n NSG-BackEnd
   
    <span data-ttu-id="f171b-154">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="f171b-154">Expected output:</span></span>
   
        info:    Executing command network nsg create
        info:    Creating a network security group "NSG-BackEnd"
        info:    Looking up hello network security group "NSG-BackEnd"
        data:    Name                            : NSG-BackEnd
        data:    Location                        : West US
        data:    Security group rules:
        data:    Name                               Source IP           Source Port  Destination IP   Destination Port  Protocol  Type      Action  Prior
        ity  Default
        data:    ---------------------------------  ------------------  -----------  ---------------  ----------------  --------  --------  ------  -----
        ---  -------
        data:    ALLOW VNET OUTBOUND                VIRTUAL_NETWORK     *            VIRTUAL_NETWORK  *                 *         Outbound  Allow   65000
             true   
        data:    ALLOW VNET INBOUND                 VIRTUAL_NETWORK     *            VIRTUAL_NETWORK  *                 *         Inbound   Allow   65000
             true   
        data:    ALLOW AZURE LOAD BALANCER INBOUND  AZURE_LOADBALANCER  *            *                *                 *         Inbound   Allow   65001
             true   
        data:    ALLOW INTERNET OUTBOUND            *                   *            INTERNET         *                 *         Outbound  Allow   65001
             true   
        data:    DENY ALL OUTBOUND                  *                   *            *                *                 *         Outbound  Deny    65500
             true   
        data:    DENY ALL INBOUND                   *                   *            *                *                 *         Inbound   Deny    65500
             true   
        info:    network nsg create command OK
   
    <span data-ttu-id="f171b-155">Parametry:</span><span class="sxs-lookup"><span data-stu-id="f171b-155">Parameters:</span></span>
   
   * <span data-ttu-id="f171b-156">**-l (lub --location)**.</span><span class="sxs-lookup"><span data-stu-id="f171b-156">**-l (or --location)**.</span></span> <span data-ttu-id="f171b-157">Region platformy Azure, której hello Nowa grupa NSG zostanie utworzona.</span><span class="sxs-lookup"><span data-stu-id="f171b-157">Azure region where hello new NSG will be created.</span></span> <span data-ttu-id="f171b-158">W naszym scenariuszu *westus*.</span><span class="sxs-lookup"><span data-stu-id="f171b-158">For our scenario, *westus*.</span></span>
   * <span data-ttu-id="f171b-159">**-n (lub --name)**.</span><span class="sxs-lookup"><span data-stu-id="f171b-159">**-n (or --name)**.</span></span> <span data-ttu-id="f171b-160">Nazwa hello Nowa grupa NSG.</span><span class="sxs-lookup"><span data-stu-id="f171b-160">Name for hello new NSG.</span></span> <span data-ttu-id="f171b-161">W naszym scenariuszu *frontonu NSG*.</span><span class="sxs-lookup"><span data-stu-id="f171b-161">For our scenario, *NSG-FrontEnd*.</span></span>
2. <span data-ttu-id="f171b-162">Uruchom hello  **`azure network nsg rule create`**  toocreate polecenia regułę, która umożliwia dostęp tooport 1433 (SQL) z podsieci frontonu hello.</span><span class="sxs-lookup"><span data-stu-id="f171b-162">Run hello **`azure network nsg rule create`** command toocreate a rule that allows access tooport 1433 (SQL) from hello front end subnet.</span></span>
   
        azure network nsg rule create -a NSG-BackEnd -n sql-rule -c Allow -p Tcp -r Inbound -y 100 -f 192.168.1.0/24 -o * -e * -u 1433
   
    <span data-ttu-id="f171b-163">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="f171b-163">Expected output:</span></span>
   
        info:    Executing command network nsg rule create
        info:    Looking up hello network security group "NSG-BackEnd"
        info:    Creating a network security rule "sql-rule"
        info:    Looking up hello network security group "NSG-BackEnd"
        data:    Name                            : sql-rule
        data:    Source address prefix           : 192.168.1.0/24
        data:    Source Port                     : *
        data:    Destination address prefix      : *
        data:    Destination Port                : 1433
        data:    Protocol                        : TCP
        data:    Type                            : Inbound
        data:    Action                          : Allow
        data:    Priority                        : 100
        info:    network nsg rule create command OK
3. <span data-ttu-id="f171b-164">Uruchom hello  **`azure network nsg rule create`**  toocreate polecenia regułę, która odmawia dostępu toohello Internet.</span><span class="sxs-lookup"><span data-stu-id="f171b-164">Run hello **`azure network nsg rule create`** command toocreate a rule that denies access toohello Internet.</span></span>
   
        azure network nsg rule create -a NSG-BackEnd -n web-rule -c Deny -p Tcp -r Outbound -y 200 -f * -o * -e Internet -u 80
   
    <span data-ttu-id="f171b-165">Oczekiwano putput:</span><span class="sxs-lookup"><span data-stu-id="f171b-165">Expected putput:</span></span>
   
        info:    Executing command network nsg rule create
        info:    Looking up hello network security group "NSG-BackEnd"
        info:    Creating a network security rule "web-rule"
        info:    Looking up hello network security group "NSG-BackEnd"
        data:    Name                            : web-rule
        data:    Source address prefix           : *
        data:    Source Port                     : *
        data:    Destination address prefix      : INTERNET
        data:    Destination Port                : 80
        data:    Protocol                        : TCP
        data:    Type                            : Outbound
        data:    Action                          : Deny
        data:    Priority                        : 200
        info:    network nsg rule create command OK
4. <span data-ttu-id="f171b-166">Uruchom hello  **`azure network nsg subnet add`**  polecenia toolink hello NSG toohello ponownie kończyć podsieci.</span><span class="sxs-lookup"><span data-stu-id="f171b-166">Run hello **`azure network nsg subnet add`** command toolink hello NSG toohello back end subnet.</span></span>
   
        azure network nsg subnet add -a NSG-BackEnd --vnet-name TestVNet --subnet-name BackEnd
   
    <span data-ttu-id="f171b-167">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="f171b-167">Expected output:</span></span>
   
        info:    Executing command network nsg subnet add
        info:    Looking up hello network security group "NSG-BackEndX"
        info:    Looking up hello subnet "BackEnd"
        info:    Looking up network configuration
        info:    Creating a network security group "NSG-BackEndX"
        info:    network nsg subnet add command OK

