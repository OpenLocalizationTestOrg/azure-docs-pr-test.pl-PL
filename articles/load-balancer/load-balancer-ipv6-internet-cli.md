---
title: "Moduł równoważenia obciążenia aaaCreate internetowy z IPv6 - wiersza polecenia platformy Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate Internet równoważenia obciążenia w przypadku adresu IPv6 za pomocą usługi Azure Resource Manager hello wiersza polecenia platformy Azure"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
keywords: "Protokół IPv6, usługi równoważenia obciążenia azure, podwójnego stosu, publiczny adres ip, natywnego protokołu ipv6, mobile, iot"
ms.assetid: a1957c9c-9c1d-423e-9d5c-d71449bc1f37
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 7ff75ac90d74a74e3d0c27672b36fbd955a086a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-internet-facing-load-balancer-with-ipv6-in-azure-resource-manager-using-hello-azure-cli"></a><span data-ttu-id="13e01-104">Tworzenie modułu równoważenia obciążenia z protokołu IPv6 w usłudze Azure Resource Manager przy użyciu interfejsu wiersza polecenia Azure hello internetowy</span><span class="sxs-lookup"><span data-stu-id="13e01-104">Create an Internet facing load balancer with IPv6 in Azure Resource Manager using hello Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="13e01-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="13e01-105">PowerShell</span></span>](load-balancer-ipv6-internet-ps.md)
> * [<span data-ttu-id="13e01-106">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="13e01-106">Azure CLI</span></span>](load-balancer-ipv6-internet-cli.md)
> * [<span data-ttu-id="13e01-107">Szablon</span><span class="sxs-lookup"><span data-stu-id="13e01-107">Template</span></span>](load-balancer-ipv6-internet-template.md)

<span data-ttu-id="13e01-108">Usługa Azure Load Balancer to moduł równoważenia obciążenia w warstwie 4 (TCP, UDP).</span><span class="sxs-lookup"><span data-stu-id="13e01-108">An Azure load balancer is a Layer-4 (TCP, UDP) load balancer.</span></span> <span data-ttu-id="13e01-109">Hello modułu równoważenia obciążenia zapewnia wysoką dostępność, przekazując przychodzący ruch między wystąpienie usługi działa prawidłowo usług w chmurze lub maszyn wirtualnych w zestawie usługi równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="13e01-109">hello load balancer provides high availability by distributing incoming traffic among healthy service instances in cloud services or virtual machines in a load balancer set.</span></span> <span data-ttu-id="13e01-110">Usługa Azure Load Balancer może także prezentować te usługi na wielu portach i/lub wielu adresach IP.</span><span class="sxs-lookup"><span data-stu-id="13e01-110">Azure Load Balancer can also present those services on multiple ports, multiple IP addresses, or both.</span></span>

## <a name="example-deployment-scenario"></a><span data-ttu-id="13e01-111">Przykładowy scenariusz wdrażania</span><span class="sxs-lookup"><span data-stu-id="13e01-111">Example deployment scenario</span></span>

<span data-ttu-id="13e01-112">Witaj poniższym diagramie przedstawiono rozwiązania do równoważenia obciążenia hello wdrażane za pomocą szablonu przykład hello opisane w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="13e01-112">hello following diagram illustrates hello load balancing solution being deployed using hello example template described in this article.</span></span>

![Scenariusz modułu równoważenia obciążenia](./media/load-balancer-ipv6-internet-cli/lb-ipv6-scenario-cli.png)

<span data-ttu-id="13e01-114">W tym scenariuszu utworzysz hello następujących zasobów platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="13e01-114">In this scenario you will create hello following Azure resources:</span></span>

* <span data-ttu-id="13e01-115">dwóch maszyn wirtualnych (VM)</span><span class="sxs-lookup"><span data-stu-id="13e01-115">two virtual machines (VMs)</span></span>
* <span data-ttu-id="13e01-116">Interfejs sieci wirtualnej, dla każdej maszyny Wirtualnej przy użyciu adresów IPv4 i IPv6 przypisany</span><span class="sxs-lookup"><span data-stu-id="13e01-116">a virtual network interface for each VM with both IPv4 and IPv6 addresses assigned</span></span>
* <span data-ttu-id="13e01-117">Moduł równoważenia obciążenia internetowy z protokołów IPv4 i IPv6 publicznego adresu IP</span><span class="sxs-lookup"><span data-stu-id="13e01-117">an Internet-facing Load Balancer with an IPv4 and an IPv6 Public IP address</span></span>
* <span data-ttu-id="13e01-118">toothat zestawu dostępności zawiera Witaj dwie maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="13e01-118">an Availability Set toothat contains hello two VMs</span></span>
* <span data-ttu-id="13e01-119">dwa załadować równoważenia reguły toomap hello publiczne adresy VIP toohello prywatnej punkty końcowe</span><span class="sxs-lookup"><span data-stu-id="13e01-119">two load balancing rules toomap hello public VIPs toohello private endpoints</span></span>

## <a name="deploying-hello-solution-using-hello-azure-cli"></a><span data-ttu-id="13e01-120">Wdrażanie rozwiązania hello przy użyciu hello wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="13e01-120">Deploying hello solution using hello Azure CLI</span></span>

<span data-ttu-id="13e01-121">Witaj następujące kroki pokazują, jak toocreate Internetem obciążenia przy użyciu usługi Azure Resource Manager z interfejsu wiersza polecenia usługi równoważenia.</span><span class="sxs-lookup"><span data-stu-id="13e01-121">hello following steps show how toocreate an Internet facing load balancer using Azure Resource Manager with CLI.</span></span> <span data-ttu-id="13e01-122">Usługi Azure Resource Manager każdy zasób jest tworzony i skonfigurować osobno, a następnie umieść razem toocreate zasobu.</span><span class="sxs-lookup"><span data-stu-id="13e01-122">With Azure Resource Manager, each resource is created and configured individually, and then put together toocreate a resource.</span></span>

<span data-ttu-id="13e01-123">toodeploy modułu równoważenia obciążenia, możesz utworzyć i skonfigurować hello następujące obiekty:</span><span class="sxs-lookup"><span data-stu-id="13e01-123">toodeploy a load balancer, you create and configure hello following objects:</span></span>

* <span data-ttu-id="13e01-124">Konfiguracja IP frontonu — publiczne adresy IP dla przychodzącego ruchu sieciowego.</span><span class="sxs-lookup"><span data-stu-id="13e01-124">Front-end IP configuration - contains public IP addresses for incoming network traffic.</span></span>
* <span data-ttu-id="13e01-125">Pula adresów zaplecza — zawiera interfejsów sieciowych (NIC) dla ruchu sieciowego tooreceive hello maszyn wirtualnych z hello modułu równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="13e01-125">Back-end address pool - contains network interfaces (NICs) for hello virtual machines tooreceive network traffic from hello load balancer.</span></span>
* <span data-ttu-id="13e01-126">Reguły równoważenia obciążenia — zawiera reguły mapowania port publiczny na tooport usługi równoważenia obciążenia hello hello puli adresów zaplecza.</span><span class="sxs-lookup"><span data-stu-id="13e01-126">Load balancing rules - contains rules mapping a public port on hello load balancer tooport in hello back-end address pool.</span></span>
* <span data-ttu-id="13e01-127">Reguły NAT dla ruchu przychodzącego — zawiera reguły mapowania port publiczny na porcie programu tooa usługi równoważenia obciążenia w hello dla określonej maszyny wirtualnej w puli adresów zaplecza hello.</span><span class="sxs-lookup"><span data-stu-id="13e01-127">Inbound NAT rules - contains rules mapping a public port on hello load balancer tooa port for a specific virtual machine in hello back-end address pool.</span></span>
* <span data-ttu-id="13e01-128">Sondy — zawiera dostępności toocheck badania używane kondycji wystąpień maszyn wirtualnych w puli adresów zaplecza hello.</span><span class="sxs-lookup"><span data-stu-id="13e01-128">Probes - contains health probes used toocheck availability of virtual machines instances in hello back-end address pool.</span></span>

<span data-ttu-id="13e01-129">Aby uzyskać więcej informacji, zobacz artykuł [Azure Resource Manager support for Load Balancer](load-balancer-arm.md) (Obsługa usługi Azure Resource Manager dla modułu równoważenia obciążenia).</span><span class="sxs-lookup"><span data-stu-id="13e01-129">For more information, see [Azure Resource Manager support for Load Balancer](load-balancer-arm.md).</span></span>

## <a name="set-up-your-cli-environment-toouse-azure-resource-manager"></a><span data-ttu-id="13e01-130">Konfigurowanie sieci toouse środowiska interfejsu wiersza polecenia usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="13e01-130">Set up your CLI environment toouse Azure Resource Manager</span></span>

<span data-ttu-id="13e01-131">Na przykład Uruchamiamy hello narzędzi interfejsu wiersza polecenia w oknie poleceń programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="13e01-131">For this example, we are running hello CLI tools in a PowerShell command window.</span></span> <span data-ttu-id="13e01-132">Nie użyto polecenia cmdlet programu Azure PowerShell hello, ale używamy czytelność tooimprove możliwości i ponowne użycie skryptów programu PowerShell w.</span><span class="sxs-lookup"><span data-stu-id="13e01-132">We are not using hello Azure PowerShell cmdlets but we use PowerShell's scripting capabilities tooimprove readability and reuse.</span></span>

1. <span data-ttu-id="13e01-133">Jeśli po raz pierwszy używasz interfejsu wiersza polecenia Azure, zobacz [Instalowanie i Konfigurowanie interfejsu wiersza polecenia Azure hello](../cli-install-nodejs.md) i wykonaj instrukcje hello zapasowej punktu toohello, gdzie należy wybrać konto platformy Azure i subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="13e01-133">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="13e01-134">Uruchom hello **trybie azure config** tryb Manager tooResource tooswitch polecenia.</span><span class="sxs-lookup"><span data-stu-id="13e01-134">Run hello **azure config mode** command tooswitch tooResource Manager mode.</span></span>

    ```azurecli
    azure config mode arm
    ```

    <span data-ttu-id="13e01-135">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="13e01-135">Expected output:</span></span>

        info:    New mode is arm

3. <span data-ttu-id="13e01-136">Zaloguj się tooAzure i uzyskać listę subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="13e01-136">Sign in tooAzure and get a list of subscriptions.</span></span>

    ```azurecli
    azure login
    ```

    <span data-ttu-id="13e01-137">Wprowadź swoje poświadczenia usługi Azure, po wyświetleniu monitu.</span><span class="sxs-lookup"><span data-stu-id="13e01-137">Enter your Azure credentials when prompted.</span></span>

    ```azurecli
    azure account list
    ```

    <span data-ttu-id="13e01-138">Wybierz subskrypcję hello, który ma toouse.</span><span class="sxs-lookup"><span data-stu-id="13e01-138">Pick hello subscription you want toouse.</span></span> <span data-ttu-id="13e01-139">Zanotuj identyfikator subskrypcji hello hello następnego kroku.</span><span class="sxs-lookup"><span data-stu-id="13e01-139">Make note of hello subscription Id for hello next step.</span></span>

4. <span data-ttu-id="13e01-140">Ustawianie zmiennych środowiska PowerShell do użytku z hello polecenia interfejsu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="13e01-140">Set up PowerShell variables for use with hello CLI commands.</span></span>

    ```powershell
    $subscriptionid = "########-####-####-####-############"  # enter subscription id
    $location = "southcentralus"
    $rgName = "pscontosorg1southctrlus09152016"
    $vnetName = "contosoIPv4Vnet"
    $vnetPrefix = "10.0.0.0/16"
    $subnet1Name = "clicontosoIPv4Subnet1"
    $subnet1Prefix = "10.0.0.0/24"
    $subnet2Name = "clicontosoIPv4Subnet2"
    $subnet2Prefix = "10.0.1.0/24"
    $dnsLabel = "contoso09152016"
    $lbName = "myIPv4IPv6Lb"
    ```

## <a name="create-a-resource-group-a-load-balancer-a-virtual-network-and-subnets"></a><span data-ttu-id="13e01-141">Utwórz grupę zasobów, usługi równoważenia obciążenia sieci wirtualnej i podsieci</span><span class="sxs-lookup"><span data-stu-id="13e01-141">Create a resource group, a load balancer, a virtual network, and subnets</span></span>

1. <span data-ttu-id="13e01-142">Tworzenie grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="13e01-142">Create a resource group</span></span>

    ```azurecli
    azure group create $rgName $location
    ```

2. <span data-ttu-id="13e01-143">Tworzenie modułu równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="13e01-143">Create a load balancer</span></span>

    ```azurecli
    $lb = azure network lb create --resource-group $rgname --location $location --name $lbName
    ```

3. <span data-ttu-id="13e01-144">Utwórz sieć wirtualną (VNet).</span><span class="sxs-lookup"><span data-stu-id="13e01-144">Create a virtual network (VNet).</span></span>

    ```azurecli
    $vnet = azure network vnet create  --resource-group $rgname --name $vnetName --location $location --address-prefixes $vnetPrefix
    ```

    <span data-ttu-id="13e01-145">Utwórz dwie podsieci w tej sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="13e01-145">Create two subnets in this VNet.</span></span>

    ```azurecli
    $subnet1 = azure network vnet subnet create --resource-group $rgname --name $subnet1Name --address-prefix $subnet1Prefix --vnet-name $vnetName
    $subnet2 = azure network vnet subnet create --resource-group $rgname --name $subnet2Name --address-prefix $subnet2Prefix --vnet-name $vnetName
    ```

## <a name="create-public-ip-addresses-for-hello-front-end-pool"></a><span data-ttu-id="13e01-146">Tworzenie publicznych adresów IP dla puli frontonu hello</span><span class="sxs-lookup"><span data-stu-id="13e01-146">Create public IP addresses for hello front-end pool</span></span>

1. <span data-ttu-id="13e01-147">Ustawianie zmiennych środowiska PowerShell hello</span><span class="sxs-lookup"><span data-stu-id="13e01-147">Set up hello PowerShell variables</span></span>

    ```powershell
    $publicIpv4Name = "myIPv4Vip"
    $publicIpv6Name = "myIPv6Vip"
    ```

2. <span data-ttu-id="13e01-148">Utwórz publiczny pulę adresów IP hello frontonu IP.</span><span class="sxs-lookup"><span data-stu-id="13e01-148">Create a public IP address hello front-end IP pool.</span></span>

    ```azurecli
    $publicipV4 = azure network public-ip create --resource-group $rgname --name $publicIpv4Name --location $location --ip-version IPv4 --allocation-method Dynamic --domain-name-label $dnsLabel
    $publicipV6 = azure network public-ip create --resource-group $rgname --name $publicIpv6Name --location $location --ip-version IPv6 --allocation-method Dynamic --domain-name-label $dnsLabel
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="13e01-149">Moduł równoważenia obciążenia Hello używa hello etykieta domeny publicznego adresu IP hello jako nazwy FQDN.</span><span class="sxs-lookup"><span data-stu-id="13e01-149">hello load balancer uses hello domain label of hello public IP as its FQDN.</span></span> <span data-ttu-id="13e01-150">Ta zmiana wdrożenie klasyczne, używający nazwa usługi w chmurze hello hello równoważenia obciążenia w pełni kwalifikowaną nazwę domeny.</span><span class="sxs-lookup"><span data-stu-id="13e01-150">This a change from classic deployment, which uses hello cloud service name as hello load balancer FQDN.</span></span>
    > <span data-ttu-id="13e01-151">W tym przykładzie hello nazwy FQDN jest *contoso09152016.southcentralus.cloudapp.azure.com*.</span><span class="sxs-lookup"><span data-stu-id="13e01-151">In this example, hello FQDN is *contoso09152016.southcentralus.cloudapp.azure.com*.</span></span>

## <a name="create-front-end-and-back-end-pools"></a><span data-ttu-id="13e01-152">Tworzenie puli frontonu i zaplecza</span><span class="sxs-lookup"><span data-stu-id="13e01-152">Create front-end and back-end pools</span></span>

<span data-ttu-id="13e01-153">W tym przykładzie tworzy hello frontonu puli adresów IP odbierająca hello przychodzącego ruchu sieciowego na powitania modułu równoważenia obciążenia i puli adresów IP zaplecza hello gdzie puli frontonu hello wysyła ruch sieciowy hello ze zrównoważonym obciążeniem.</span><span class="sxs-lookup"><span data-stu-id="13e01-153">This example creates hello front-end IP pool that receives hello incoming network traffic on hello load balancer and hello back-end IP pool where hello front-end pool sends hello load balanced network traffic.</span></span>

1. <span data-ttu-id="13e01-154">Ustawianie zmiennych środowiska PowerShell hello</span><span class="sxs-lookup"><span data-stu-id="13e01-154">Set up hello PowerShell variables</span></span>

    ```powershell
    $frontendV4Name = "FrontendVipIPv4"
    $frontendV6Name = "FrontendVipIPv6"
    $backendAddressPoolV4Name = "BackendPoolIPv4"
    $backendAddressPoolV6Name = "BackendPoolIPv6"
    ```

2. <span data-ttu-id="13e01-155">Utwórz pulę IP frontonu skojarzenie publicznego adresu IP hello utworzone w poprzednim kroku hello i hello modułu równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="13e01-155">Create a front-end IP pool associating hello public IP created in hello previous step and hello load balancer.</span></span>

    ```azurecli
    $frontendV4 = azure network lb frontend-ip create --resource-group $rgname --name $frontendV4Name --public-ip-name $publicIpv4Name --lb-name $lbName
    $frontendV6 = azure network lb frontend-ip create --resource-group $rgname --name $frontendV6Name --public-ip-name $publicIpv6Name --lb-name $lbName
    $backendAddressPoolV4 = azure network lb address-pool create --resource-group $rgname --name $backendAddressPoolV4Name --lb-name $lbName
    $backendAddressPoolV6 = azure network lb address-pool create --resource-group $rgname --name $backendAddressPoolV6Name --lb-name $lbName
    ```

## <a name="create-hello-probe-nat-rules-and-lb-rules"></a><span data-ttu-id="13e01-156">Tworzenie hello sondowania, reguł NAT oraz zasady równoważeniem obciążenia</span><span class="sxs-lookup"><span data-stu-id="13e01-156">Create hello probe, NAT rules, and LB rules</span></span>

<span data-ttu-id="13e01-157">W tym przykładzie jest tworzony hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="13e01-157">This example creates hello following items:</span></span>

* <span data-ttu-id="13e01-158">Sonda toocheck reguły dla łączności tooTCP portu 80</span><span class="sxs-lookup"><span data-stu-id="13e01-158">a probe rule toocheck for connectivity tooTCP port 80</span></span>
* <span data-ttu-id="13e01-159">translator NAT reguły tootranslate cały ruch przychodzący na porcie 3389 tooport 3389 protokołu RDP<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="13e01-159">a NAT rule tootranslate all incoming traffic on port 3389 tooport 3389 for RDP<sup>1</sup></span></span>
* <span data-ttu-id="13e01-160">translator NAT reguły tootranslate cały ruch przychodzący na porcie 3391 tooport 3389 protokołu RDP<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="13e01-160">a NAT rule tootranslate all incoming traffic on port 3391 tooport 3389 for RDP<sup>1</sup></span></span>
* <span data-ttu-id="13e01-161">toobalance reguły modułu równoważenia obciążenia cały ruch przychodzący na porcie 80 tooport 80 na powitania adresów w puli zaplecza hello.</span><span class="sxs-lookup"><span data-stu-id="13e01-161">a load balancer rule toobalance all incoming traffic on port 80 tooport 80 on hello addresses in hello back-end pool.</span></span>

<span data-ttu-id="13e01-162"><sup>1</sup> reguł NAT są skojarzone tooa wystąpienia określonej maszyny wirtualnej za hello równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="13e01-162"><sup>1</sup> NAT rules are associated tooa specific virtual machine instance behind hello load balancer.</span></span> <span data-ttu-id="13e01-163">ruch sieciowy Hello przychodzące do portu 3389 jest wysyłane toohello określonej maszyny wirtualnej i skojarzonych z hello reguły NAT portu.</span><span class="sxs-lookup"><span data-stu-id="13e01-163">hello network traffic arriving on port 3389 is sent toohello specific virtual machine and port associated with hello NAT rule.</span></span> <span data-ttu-id="13e01-164">Musisz określić protokół (UDP lub TCP) dla reguły NAT.</span><span class="sxs-lookup"><span data-stu-id="13e01-164">You must specify a protocol (UDP or TCP) for a NAT rule.</span></span> <span data-ttu-id="13e01-165">Oba protokoły nie może być przypisana toohello tego samego portu.</span><span class="sxs-lookup"><span data-stu-id="13e01-165">Both protocols can't be assigned toohello same port.</span></span>

1. <span data-ttu-id="13e01-166">Ustawianie zmiennych środowiska PowerShell hello</span><span class="sxs-lookup"><span data-stu-id="13e01-166">Set up hello PowerShell variables</span></span>

    ```powershell
    $probeV4V6Name = "ProbeForIPv4AndIPv6"
    $natRule1V4Name = "NatRule-For-Rdp-VM1"
    $natRule2V4Name = "NatRule-For-Rdp-VM2"
    $lbRule1V4Name = "LBRuleForIPv4-Port80"
    $lbRule1V6Name = "LBRuleForIPv6-Port80"
    ```

2. <span data-ttu-id="13e01-167">Utworzyć hello sondy</span><span class="sxs-lookup"><span data-stu-id="13e01-167">Create hello probe</span></span>

    <span data-ttu-id="13e01-168">Witaj poniższy przykład tworzy sondowaniem TCP sprawdzającą dla łączności tooback-end-port TCP 80 co 15 s.</span><span class="sxs-lookup"><span data-stu-id="13e01-168">hello following example creates a TCP probe that checks for connectivity tooback-end TCP port 80 every 15 seconds.</span></span> <span data-ttu-id="13e01-169">Go spowoduje oznaczenie zasobów zaplecza hello niedostępne po dwóch kolejnych błędów.</span><span class="sxs-lookup"><span data-stu-id="13e01-169">It will mark hello back-end resource unavailable after two consecutive failures.</span></span>

    ```azurecli
    $probeV4V6 = azure network lb probe create --resource-group $rgname --name $probeV4V6Name --protocol tcp --port 80 --interval 15 --count 2 --lb-name $lbName
    ```

3. <span data-ttu-id="13e01-170">Tworzenie reguł ruchu przychodzącego translatora adresów Sieciowych, które połączeń protokołu RDP toohello zaplecza zasobów</span><span class="sxs-lookup"><span data-stu-id="13e01-170">Create inbound NAT rules that allow RDP connections toohello back-end resources</span></span>

    ```azurecli
    $inboundNatRuleRdp1 = azure network lb inbound-nat-rule create --resource-group $rgname --name $natRule1V4Name --frontend-ip-name $frontendV4Name --protocol Tcp --frontend-port 3389 --backend-port 3389 --lb-name $lbName
    $inboundNatRuleRdp2 = azure network lb inbound-nat-rule create --resource-group $rgname --name $natRule2V4Name --frontend-ip-name $frontendV4Name --protocol Tcp --frontend-port 3391 --backend-port 3389 --lb-name $lbName
    ```

4. <span data-ttu-id="13e01-171">Tworzenie reguł, które przesyłają toodifferent wewnętrznych portów w zależności od tego, które frontonu odebrał żądanie hello modułu równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="13e01-171">Create a load balancer rules that send traffic toodifferent back-end ports depending on which front end received hello request</span></span>

    ```azurecli
    $lbruleIPv4 = azure network lb rule create --resource-group $rgname --name $lbRule1V4Name --frontend-ip-name $frontendV4Name --backend-address-pool-name $backendAddressPoolV4Name --probe-name $probeV4V6Name --protocol Tcp --frontend-port 80 --backend-port 80 --lb-name $lbName
    $lbruleIPv6 = azure network lb rule create --resource-group $rgname --name $lbRule1V6Name --frontend-ip-name $frontendV6Name --backend-address-pool-name $backendAddressPoolV6Name --probe-name $probeV4V6Name --protocol Tcp --frontend-port 80 --backend-port 8080 --lb-name $lbName
    ```

5. <span data-ttu-id="13e01-172">Sprawdź ustawienia</span><span class="sxs-lookup"><span data-stu-id="13e01-172">Check your settings</span></span>

    ```azurecli
    azure network lb show --resource-group $rgName --name $lbName
    ```

    <span data-ttu-id="13e01-173">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="13e01-173">Expected output:</span></span>

        info:    Executing command network lb show
        info:    Looking up hello load balancer "myIPv4IPv6Lb"
        data:    Id                              : /subscriptions/########-####-####-####-############/resourceGroups/pscontosorg1southctrlus09152016/providers/Microsoft.Network/loadBalancers/myIPv4IPv6Lb
        data:    Name                            : myIPv4IPv6Lb
        data:    Type                            : Microsoft.Network/loadBalancers
        data:    Location                        : southcentralus
        data:    Provisioning state              : Succeeded
        data:
        data:    Frontend IP configurations:
        data:    Name             Provisioning state  Private IP allocation  Private IP   Subnet  Public IP
        data:    ---------------  ------------------  ---------------------  -----------  ------  ---------
        data:    FrontendVipIPv4  Succeeded           Dynamic                                     myIPv4Vip
        data:    FrontendVipIPv6  Succeeded           Dynamic                                     myIPv6Vip
        data:
        data:    Probes:
        data:    Name                 Provisioning state  Protocol  Port  Path  Interval  Count
        data:    -------------------  ------------------  --------  ----  ----  --------  -----
        data:    ProbeForIPv4AndIPv6  Succeeded           Tcp       80          15        2
        data:
        data:    Backend Address Pools:
        data:    Name             Provisioning state
        data:    ---------------  ------------------
        data:    BackendPoolIPv4  Succeeded
        data:    BackendPoolIPv6  Succeeded
        data:
        data:    Load Balancing Rules:
        data:    Name                  Provisioning state  Load distribution  Protocol  Frontend port  Backend port  Enable floating IP  Idle timeout in minutes
        data:    --------------------  ------------------  -----------------  --------  -------------  ------------  ------------------  -----------------------
        data:    LBRuleForIPv4-Port80  Succeeded           Default            Tcp       80             80            false               4
        data:    LBRuleForIPv6-Port80  Succeeded           Default            Tcp       80             8080          false               4
        data:
        data:    Inbound NAT Rules:
        data:    Name                 Provisioning state  Protocol  Frontend port  Backend port  Enable floating IP  Idle timeout in minutes
        data:    -------------------  ------------------  --------  -------------  ------------  ------------------  -----------------------
        data:    NatRule-For-Rdp-VM1  Succeeded           Tcp       3389           3389          false               4
        data:    NatRule-For-Rdp-VM2  Succeeded           Tcp       3391           3389          false               4
        info:    network lb show

## <a name="create-nics"></a><span data-ttu-id="13e01-174">Tworzenie kart sieciowych</span><span class="sxs-lookup"><span data-stu-id="13e01-174">Create NICs</span></span>

<span data-ttu-id="13e01-175">Tworzenie kart sieciowych i skojarzyć je tooNAT reguły, reguły modułu równoważenia obciążenia i sondy.</span><span class="sxs-lookup"><span data-stu-id="13e01-175">Create NICs and associate them tooNAT rules, load balancer rules, and probes.</span></span>

1. <span data-ttu-id="13e01-176">Ustawianie zmiennych środowiska PowerShell hello</span><span class="sxs-lookup"><span data-stu-id="13e01-176">Set up hello PowerShell variables</span></span>

    ```powershell
    $nic1Name = "myIPv4IPv6Nic1"
    $nic2Name = "myIPv4IPv6Nic2"
    $subnet1Id = "/subscriptions/$subscriptionid/resourceGroups/$rgName/providers/Microsoft.Network/VirtualNetworks/$vnetName/subnets/$subnet1Name"
    $subnet2Id = "/subscriptions/$subscriptionid/resourceGroups/$rgName/providers/Microsoft.Network/VirtualNetworks/$vnetName/subnets/$subnet2Name"
    $backendAddressPoolV4Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/loadbalancers/$lbName/backendAddressPools/$backendAddressPoolV4Name"
    $backendAddressPoolV6Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/loadbalancers/$lbName/backendAddressPools/$backendAddressPoolV6Name"
    $natRule1V4Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/loadbalancers/$lbName/inboundNatRules/$natRule1V4Name"
    $natRule2V4Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/loadbalancers/$lbName/inboundNatRules/$natRule2V4Name"
    ```

2. <span data-ttu-id="13e01-177">Utwórz kartę Sieciową dla każdej zaplecza, a następnie dodaj konfiguracji protokołu IPv6.</span><span class="sxs-lookup"><span data-stu-id="13e01-177">Create a NIC for each back-end and add an IPv6 configuration.</span></span>

    ```azurecli
    $nic1 = azure network nic create --name $nic1Name --resource-group $rgname --location $location --private-ip-version "IPv4" --subnet-id $subnet1Id --lb-address-pool-ids $backendAddressPoolV4Id --lb-inbound-nat-rule-ids $natRule1V4Id
    $nic1IPv6 = azure network nic ip-config create --resource-group $rgname --name "IPv6IPConfig" --private-ip-version "IPv6" --lb-address-pool-ids $backendAddressPoolV6Id --nic-name $nic1Name

    $nic2 = azure network nic create --name $nic2Name --resource-group $rgname --location $location --subnet-id $subnet1Id --lb-address-pool-ids $backendAddressPoolV4Id --lb-inbound-nat-rule-ids $natRule2V4Id
    $nic2IPv6 = azure network nic ip-config create --resource-group $rgname --name "IPv6IPConfig" --private-ip-version "IPv6" --lb-address-pool-ids $backendAddressPoolV6Id --nic-name $nic2Name
    ```

## <a name="create-hello-back-end-vm-resources-and-attach-each-nic"></a><span data-ttu-id="13e01-178">Utwórz zasobów maszyny Wirtualnej hello zaplecza i Dołącz poszczególne karty Sieciowe</span><span class="sxs-lookup"><span data-stu-id="13e01-178">Create hello back-end VM resources and attach each NIC</span></span>

<span data-ttu-id="13e01-179">toocreate maszyn wirtualnych, musisz mieć konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="13e01-179">toocreate VMs, you must have a storage account.</span></span> <span data-ttu-id="13e01-180">W przypadku równoważenia obciążenia hello maszyny wirtualne muszą toobe członkami zestawu dostępności.</span><span class="sxs-lookup"><span data-stu-id="13e01-180">For load balancing, hello VMs need toobe members of an availability set.</span></span> <span data-ttu-id="13e01-181">Aby uzyskać więcej informacji na temat tworzenia maszyn wirtualnych, zobacz [tworzenia maszyny Wirtualnej platformy Azure przy użyciu programu PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="13e01-181">For more information about creating VMs, see [Create an Azure VM using PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json)</span></span>

1. <span data-ttu-id="13e01-182">Ustawianie zmiennych środowiska PowerShell hello</span><span class="sxs-lookup"><span data-stu-id="13e01-182">Set up hello PowerShell variables</span></span>

    ```powershell
    $storageAccountName = "ps08092016v6sa0"
    $availabilitySetName = "myIPv4IPv6AvailabilitySet"
    $vm1Name = "myIPv4IPv6VM1"
    $vm2Name = "myIPv4IPv6VM2"
    $nic1Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/networkInterfaces/$nic1Name"
    $nic2Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/networkInterfaces/$nic2Name"
    $disk1Name = "WindowsVMosDisk1"
    $disk2Name = "WindowsVMosDisk2"
    $osDisk1Uri = "https://$storageAccountName.blob.core.windows.net/vhds/$disk1Name.vhd"
    $osDisk2Uri = "https://$storageAccountName.blob.core.windows.net/vhds/$disk2Name.vhd"
    $imageurn "MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:latest"
    $vmUserName = "vmUser"
    $mySecurePassword = "PlainTextPassword*1"
    ```

    > [!WARNING]
    > <span data-ttu-id="13e01-183">W tym przykładzie używane hello nazwy użytkownika i hasła dla maszyn wirtualnych hello w postaci zwykłego tekstu.</span><span class="sxs-lookup"><span data-stu-id="13e01-183">This example uses hello username and password for hello VMs in clear text.</span></span> <span data-ttu-id="13e01-184">Odpowiednie należy uważać podczas przy użyciu poświadczeń w hello Wyczyść.</span><span class="sxs-lookup"><span data-stu-id="13e01-184">Appropriate care must be taken when using credentials in hello clear.</span></span> <span data-ttu-id="13e01-185">Aby bardziej bezpieczne metody obsługi poświadczenia w programie PowerShell, zobacz hello [Get-Credential](https://technet.microsoft.com/library/hh849815.aspx) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="13e01-185">For a more secure method of handling credentials in PowerShell, see hello [Get-Credential](https://technet.microsoft.com/library/hh849815.aspx) cmdlet.</span></span>

2. <span data-ttu-id="13e01-186">Tworzenie zestawu dostępności i konto magazynu hello</span><span class="sxs-lookup"><span data-stu-id="13e01-186">Create hello storage account and availability set</span></span>

    <span data-ttu-id="13e01-187">Po utworzeniu hello maszyn wirtualnych, może używać istniejącego konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="13e01-187">You may use an existing storage account when you create hello VMs.</span></span> <span data-ttu-id="13e01-188">Witaj następujące polecenie tworzy nowe konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="13e01-188">hello following command creates a new storage account.</span></span>

    ```azurecli
    $storageAcc = azure storage account create $storageAccountName --resource-group $rgName --location $location --sku-name "LRS" --kind "Storage"
    ```

    <span data-ttu-id="13e01-189">Następnie należy utworzyć hello zestawu dostępności.</span><span class="sxs-lookup"><span data-stu-id="13e01-189">Next, create hello availability set.</span></span>

    ```azurecli
    $availabilitySet = azure availset create --name $availabilitySetName --resource-group $rgName --location $location
    ```

3. <span data-ttu-id="13e01-190">Tworzenie maszyn wirtualnych hello z kartami sieciowymi hello skojarzone</span><span class="sxs-lookup"><span data-stu-id="13e01-190">Create hello virtual machines with hello associated NICs</span></span>

    ```azurecli
    $vm1 = azure vm create --resource-group $rgname --location $location --availset-name $availabilitySetName --name $vm1Name --nic-id $nic1Id --os-disk-vhd $osDisk1Uri --os-type "Windows" --admin-username $vmUserName --admin-password $mySecurePassword --vm-size "Standard_A1" --image-urn $imageurn --storage-account-name $storageAccountName --disable-bginfo-extension

    $vm2 = azure vm create --resource-group $rgname --location $location --availset-name $availabilitySetName --name $vm2Name --nic-id $nic2Id --os-disk-vhd $osDisk2Uri --os-type "Windows" --admin-username $vmUserName --admin-password $mySecurePassword --vm-size "Standard_A1" --image-urn $imageurn --storage-account-name $storageAccountName --disable-bginfo-extension
    ```

## <a name="next-steps"></a><span data-ttu-id="13e01-191">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="13e01-191">Next steps</span></span>

<span data-ttu-id="13e01-192">[Get started configuring an internal load balancer](load-balancer-get-started-ilb-arm-cli.md) (Wprowadzenie do konfigurowania wewnętrznego modułu równoważenia obciążenia)</span><span class="sxs-lookup"><span data-stu-id="13e01-192">[Get started configuring an internal load balancer](load-balancer-get-started-ilb-arm-cli.md)</span></span>

<span data-ttu-id="13e01-193">[Configure a load balancer distribution mode](load-balancer-distribution-mode.md) (Konfigurowanie trybu dystrybucji modułu równoważenia obciążenia)</span><span class="sxs-lookup"><span data-stu-id="13e01-193">[Configure a load balancer distribution mode](load-balancer-distribution-mode.md)</span></span>

<span data-ttu-id="13e01-194">[Configure idle TCP timeout settings for your load balancer](load-balancer-tcp-idle-timeout.md) (Konfigurowanie ustawień limitu czasu bezczynności protokołu TCP dla modułu równoważenia obciążenia)</span><span class="sxs-lookup"><span data-stu-id="13e01-194">[Configure idle TCP timeout settings for your load balancer](load-balancer-tcp-idle-timeout.md)</span></span>
