---
title: "Utwórz internetowy równoważenia obciążenia w przypadku adresu IPv6 - wiersza polecenia platformy Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak utworzyć internetowy modułu równoważenia obciążenia z protokołu IPv6 w usłudze Azure Resource Manager przy użyciu wiersza polecenia platformy Azure"
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
ms.openlocfilehash: efb4771800c42df544c3cc37d1d164045fdcaf3e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-internet-facing-load-balancer-with-ipv6-in-azure-resource-manager-using-the-azure-cli"></a><span data-ttu-id="8f7aa-104">Utwórz internetowy modułu równoważenia obciążenia z protokołu IPv6 w usłudze Azure Resource Manager przy użyciu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="8f7aa-104">Create an Internet facing load balancer with IPv6 in Azure Resource Manager using the Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="8f7aa-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8f7aa-105">PowerShell</span></span>](load-balancer-ipv6-internet-ps.md)
> * [<span data-ttu-id="8f7aa-106">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="8f7aa-106">Azure CLI</span></span>](load-balancer-ipv6-internet-cli.md)
> * [<span data-ttu-id="8f7aa-107">Szablon</span><span class="sxs-lookup"><span data-stu-id="8f7aa-107">Template</span></span>](load-balancer-ipv6-internet-template.md)

<span data-ttu-id="8f7aa-108">Usługa Azure Load Balancer to moduł równoważenia obciążenia w warstwie 4 (TCP, UDP).</span><span class="sxs-lookup"><span data-stu-id="8f7aa-108">An Azure load balancer is a Layer-4 (TCP, UDP) load balancer.</span></span> <span data-ttu-id="8f7aa-109">Moduł równoważenia obciążenia zapewnia wysoką dostępność, dystrybuując ruch przychodzący w wystąpieniach usług o dobrej kondycji w usługach w chmurze lub na maszynach wirtualnych w zestawie modułu równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="8f7aa-109">The load balancer provides high availability by distributing incoming traffic among healthy service instances in cloud services or virtual machines in a load balancer set.</span></span> <span data-ttu-id="8f7aa-110">Usługa Azure Load Balancer może także prezentować te usługi na wielu portach i/lub wielu adresach IP.</span><span class="sxs-lookup"><span data-stu-id="8f7aa-110">Azure Load Balancer can also present those services on multiple ports, multiple IP addresses, or both.</span></span>

## <a name="example-deployment-scenario"></a><span data-ttu-id="8f7aa-111">Przykładowy scenariusz wdrażania</span><span class="sxs-lookup"><span data-stu-id="8f7aa-111">Example deployment scenario</span></span>

<span data-ttu-id="8f7aa-112">Na poniższym diagramie przedstawiono rozwiązania do równoważenia obciążenia jest wdrażane za pomocą szablonu przykład opisane w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="8f7aa-112">The following diagram illustrates the load balancing solution being deployed using the example template described in this article.</span></span>

![Scenariusz modułu równoważenia obciążenia](./media/load-balancer-ipv6-internet-cli/lb-ipv6-scenario-cli.png)

<span data-ttu-id="8f7aa-114">W tym scenariuszu spowoduje utworzenie następujących zasobów platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="8f7aa-114">In this scenario you will create the following Azure resources:</span></span>

* <span data-ttu-id="8f7aa-115">dwóch maszyn wirtualnych (VM)</span><span class="sxs-lookup"><span data-stu-id="8f7aa-115">two virtual machines (VMs)</span></span>
* <span data-ttu-id="8f7aa-116">Interfejs sieci wirtualnej, dla każdej maszyny Wirtualnej przy użyciu adresów IPv4 i IPv6 przypisany</span><span class="sxs-lookup"><span data-stu-id="8f7aa-116">a virtual network interface for each VM with both IPv4 and IPv6 addresses assigned</span></span>
* <span data-ttu-id="8f7aa-117">Moduł równoważenia obciążenia internetowy z protokołów IPv4 i IPv6 publicznego adresu IP</span><span class="sxs-lookup"><span data-stu-id="8f7aa-117">an Internet-facing Load Balancer with an IPv4 and an IPv6 Public IP address</span></span>
* <span data-ttu-id="8f7aa-118">Zestaw dostępności w tym zawiera dwie maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="8f7aa-118">an Availability Set to that contains the two VMs</span></span>
* <span data-ttu-id="8f7aa-119">dwie reguły równoważenia do mapowania publiczne adresy VIP prywatnej punkty końcowe obciążenia</span><span class="sxs-lookup"><span data-stu-id="8f7aa-119">two load balancing rules to map the public VIPs to the private endpoints</span></span>

## <a name="deploying-the-solution-using-the-azure-cli"></a><span data-ttu-id="8f7aa-120">Wdrażanie rozwiązania za pomocą interfejsu wiersza polecenia Azure</span><span class="sxs-lookup"><span data-stu-id="8f7aa-120">Deploying the solution using the Azure CLI</span></span>

<span data-ttu-id="8f7aa-121">W poniższych krokach opisano, jak utworzyć dostępny z Internetu moduł równoważenia obciążenia przy użyciu usługi Azure Resource Manager z interfejsem wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="8f7aa-121">The following steps show how to create an Internet facing load balancer using Azure Resource Manager with CLI.</span></span> <span data-ttu-id="8f7aa-122">Usługa Azure Resource Manager pozwala tworzyć i konfigurować każdy zasób osobno, a następnie łączyć je ze sobą w celu utworzenia kolejnego zasobu.</span><span class="sxs-lookup"><span data-stu-id="8f7aa-122">With Azure Resource Manager, each resource is created and configured individually, and then put together to create a resource.</span></span>

<span data-ttu-id="8f7aa-123">Aby wdrożyć usługę równoważenia obciążenia, możesz utworzyć i skonfigurować następujące obiekty:</span><span class="sxs-lookup"><span data-stu-id="8f7aa-123">To deploy a load balancer, you create and configure the following objects:</span></span>

* <span data-ttu-id="8f7aa-124">Konfiguracja IP frontonu — publiczne adresy IP dla przychodzącego ruchu sieciowego.</span><span class="sxs-lookup"><span data-stu-id="8f7aa-124">Front-end IP configuration - contains public IP addresses for incoming network traffic.</span></span>
* <span data-ttu-id="8f7aa-125">Pula adresów zaplecza — interfejsy sieciowe (NIC) maszyn wirtualnych odbierających ruch sieciowy z modułu równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="8f7aa-125">Back-end address pool - contains network interfaces (NICs) for the virtual machines to receive network traffic from the load balancer.</span></span>
* <span data-ttu-id="8f7aa-126">Reguły równoważenia obciążenia — reguły mapowania portu publicznego modułu równoważenia obciążenia na port w puli adresów zaplecza.</span><span class="sxs-lookup"><span data-stu-id="8f7aa-126">Load balancing rules - contains rules mapping a public port on the load balancer to port in the back-end address pool.</span></span>
* <span data-ttu-id="8f7aa-127">Reguły NAT ruchu przychodzącego — reguły mapowania portu publicznego modułu równoważenia obciążenia na port określonej maszyny wirtualnej w puli adresów zaplecza.</span><span class="sxs-lookup"><span data-stu-id="8f7aa-127">Inbound NAT rules - contains rules mapping a public port on the load balancer to a port for a specific virtual machine in the back-end address pool.</span></span>
* <span data-ttu-id="8f7aa-128">Sondy — sondy kondycji używane do sprawdzania dostępności wystąpień maszyn wirtualnych w puli adresów zaplecza.</span><span class="sxs-lookup"><span data-stu-id="8f7aa-128">Probes - contains health probes used to check availability of virtual machines instances in the back-end address pool.</span></span>

<span data-ttu-id="8f7aa-129">Aby uzyskać więcej informacji, zobacz artykuł [Azure Resource Manager support for Load Balancer](load-balancer-arm.md) (Obsługa usługi Azure Resource Manager dla modułu równoważenia obciążenia).</span><span class="sxs-lookup"><span data-stu-id="8f7aa-129">For more information, see [Azure Resource Manager support for Load Balancer](load-balancer-arm.md).</span></span>

## <a name="set-up-your-cli-environment-to-use-azure-resource-manager"></a><span data-ttu-id="8f7aa-130">Konfigurowanie środowiska interfejsu wiersza polecenia do użycia usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="8f7aa-130">Set up your CLI environment to use Azure Resource Manager</span></span>

<span data-ttu-id="8f7aa-131">Na przykład Uruchamiamy narzędzi interfejsu wiersza polecenia w oknie poleceń programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8f7aa-131">For this example, we are running the CLI tools in a PowerShell command window.</span></span> <span data-ttu-id="8f7aa-132">Nie użyto polecenia cmdlet programu Azure PowerShell, ale używamy możliwości obsługi skryptów programu PowerShell w celu zwiększenia czytelności i ponownego użycia.</span><span class="sxs-lookup"><span data-stu-id="8f7aa-132">We are not using the Azure PowerShell cmdlets but we use PowerShell's scripting capabilities to improve readability and reuse.</span></span>

1. <span data-ttu-id="8f7aa-133">Jeśli po raz pierwszy używasz interfejsu wiersza polecenia Azure, zobacz artykuł [Instalowanie i konfigurowania interfejsu wiersza polecenia Azure](../cli-install-nodejs.md) i postępuj zgodnie z instrukcjami aż do punktu, w którym należy wybrać konto platformy Azure i subskrypcję.</span><span class="sxs-lookup"><span data-stu-id="8f7aa-133">If you have never used Azure CLI, see [Install and Configure the Azure CLI](../cli-install-nodejs.md) and follow the instructions up to the point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="8f7aa-134">Uruchom **trybie azure config** polecenie, aby włączyć tryb Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="8f7aa-134">Run the **azure config mode** command to switch to Resource Manager mode.</span></span>

    ```azurecli
    azure config mode arm
    ```

    <span data-ttu-id="8f7aa-135">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="8f7aa-135">Expected output:</span></span>

        info:    New mode is arm

3. <span data-ttu-id="8f7aa-136">Logowanie do platformy Azure i uzyskać listę subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="8f7aa-136">Sign in to Azure and get a list of subscriptions.</span></span>

    ```azurecli
    azure login
    ```

    <span data-ttu-id="8f7aa-137">Wprowadź swoje poświadczenia usługi Azure, po wyświetleniu monitu.</span><span class="sxs-lookup"><span data-stu-id="8f7aa-137">Enter your Azure credentials when prompted.</span></span>

    ```azurecli
    azure account list
    ```

    <span data-ttu-id="8f7aa-138">Wybierz subskrypcję, której chcesz użyć.</span><span class="sxs-lookup"><span data-stu-id="8f7aa-138">Pick the subscription you want to use.</span></span> <span data-ttu-id="8f7aa-139">Zanotuj identyfikator subskrypcji do następnego kroku.</span><span class="sxs-lookup"><span data-stu-id="8f7aa-139">Make note of the subscription Id for the next step.</span></span>

4. <span data-ttu-id="8f7aa-140">Ustawianie zmiennych środowiska PowerShell do użycia przy użyciu poleceń interfejsu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="8f7aa-140">Set up PowerShell variables for use with the CLI commands.</span></span>

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

## <a name="create-a-resource-group-a-load-balancer-a-virtual-network-and-subnets"></a><span data-ttu-id="8f7aa-141">Utwórz grupę zasobów, usługi równoważenia obciążenia sieci wirtualnej i podsieci</span><span class="sxs-lookup"><span data-stu-id="8f7aa-141">Create a resource group, a load balancer, a virtual network, and subnets</span></span>

1. <span data-ttu-id="8f7aa-142">Tworzenie grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="8f7aa-142">Create a resource group</span></span>

    ```azurecli
    azure group create $rgName $location
    ```

2. <span data-ttu-id="8f7aa-143">Tworzenie modułu równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="8f7aa-143">Create a load balancer</span></span>

    ```azurecli
    $lb = azure network lb create --resource-group $rgname --location $location --name $lbName
    ```

3. <span data-ttu-id="8f7aa-144">Utwórz sieć wirtualną (VNet).</span><span class="sxs-lookup"><span data-stu-id="8f7aa-144">Create a virtual network (VNet).</span></span>

    ```azurecli
    $vnet = azure network vnet create  --resource-group $rgname --name $vnetName --location $location --address-prefixes $vnetPrefix
    ```

    <span data-ttu-id="8f7aa-145">Utwórz dwie podsieci w tej sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="8f7aa-145">Create two subnets in this VNet.</span></span>

    ```azurecli
    $subnet1 = azure network vnet subnet create --resource-group $rgname --name $subnet1Name --address-prefix $subnet1Prefix --vnet-name $vnetName
    $subnet2 = azure network vnet subnet create --resource-group $rgname --name $subnet2Name --address-prefix $subnet2Prefix --vnet-name $vnetName
    ```

## <a name="create-public-ip-addresses-for-the-front-end-pool"></a><span data-ttu-id="8f7aa-146">Tworzenie publicznych adresów IP dla puli frontonu</span><span class="sxs-lookup"><span data-stu-id="8f7aa-146">Create public IP addresses for the front-end pool</span></span>

1. <span data-ttu-id="8f7aa-147">Ustawianie zmiennych środowiska PowerShell</span><span class="sxs-lookup"><span data-stu-id="8f7aa-147">Set up the PowerShell variables</span></span>

    ```powershell
    $publicIpv4Name = "myIPv4Vip"
    $publicIpv6Name = "myIPv6Vip"
    ```

2. <span data-ttu-id="8f7aa-148">Utwórz publiczny adres IP w puli adresów IP frontonu.</span><span class="sxs-lookup"><span data-stu-id="8f7aa-148">Create a public IP address the front-end IP pool.</span></span>

    ```azurecli
    $publicipV4 = azure network public-ip create --resource-group $rgname --name $publicIpv4Name --location $location --ip-version IPv4 --allocation-method Dynamic --domain-name-label $dnsLabel
    $publicipV6 = azure network public-ip create --resource-group $rgname --name $publicIpv6Name --location $location --ip-version IPv6 --allocation-method Dynamic --domain-name-label $dnsLabel
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="8f7aa-149">Moduł równoważenia obciążenia używa etykiety domeny publicznego adresu IP jako nazwy FQDN.</span><span class="sxs-lookup"><span data-stu-id="8f7aa-149">The load balancer uses the domain label of the public IP as its FQDN.</span></span> <span data-ttu-id="8f7aa-150">To zmiana z klasycznym wdrożenia, którego używa usługa w chmurze nazwę FQDN modułu równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="8f7aa-150">This a change from classic deployment, which uses the cloud service name as the load balancer FQDN.</span></span>
    > <span data-ttu-id="8f7aa-151">W tym przykładzie nazwa FQDN to *contoso09152016.southcentralus.cloudapp.azure.com*.</span><span class="sxs-lookup"><span data-stu-id="8f7aa-151">In this example, the FQDN is *contoso09152016.southcentralus.cloudapp.azure.com*.</span></span>

## <a name="create-front-end-and-back-end-pools"></a><span data-ttu-id="8f7aa-152">Tworzenie puli frontonu i zaplecza</span><span class="sxs-lookup"><span data-stu-id="8f7aa-152">Create front-end and back-end pools</span></span>

<span data-ttu-id="8f7aa-153">W tym przykładzie tworzy frontonu pula adresów IP, która odbiera przychodzącego ruchu sieciowego w ramach usługi równoważenia obciążenia i puli adresów IP zaplecza, gdzie puli frontonu wysyła ruch sieciowy ze zrównoważonym obciążeniem.</span><span class="sxs-lookup"><span data-stu-id="8f7aa-153">This example creates the front-end IP pool that receives the incoming network traffic on the load balancer and the back-end IP pool where the front-end pool sends the load balanced network traffic.</span></span>

1. <span data-ttu-id="8f7aa-154">Ustawianie zmiennych środowiska PowerShell</span><span class="sxs-lookup"><span data-stu-id="8f7aa-154">Set up the PowerShell variables</span></span>

    ```powershell
    $frontendV4Name = "FrontendVipIPv4"
    $frontendV6Name = "FrontendVipIPv6"
    $backendAddressPoolV4Name = "BackendPoolIPv4"
    $backendAddressPoolV6Name = "BackendPoolIPv6"
    ```

2. <span data-ttu-id="8f7aa-155">Utwórz pulę adresów IP frontonu skojarzoną z publicznym adresem IP utworzonym w poprzednim kroku oraz moduł równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="8f7aa-155">Create a front-end IP pool associating the public IP created in the previous step and the load balancer.</span></span>

    ```azurecli
    $frontendV4 = azure network lb frontend-ip create --resource-group $rgname --name $frontendV4Name --public-ip-name $publicIpv4Name --lb-name $lbName
    $frontendV6 = azure network lb frontend-ip create --resource-group $rgname --name $frontendV6Name --public-ip-name $publicIpv6Name --lb-name $lbName
    $backendAddressPoolV4 = azure network lb address-pool create --resource-group $rgname --name $backendAddressPoolV4Name --lb-name $lbName
    $backendAddressPoolV6 = azure network lb address-pool create --resource-group $rgname --name $backendAddressPoolV6Name --lb-name $lbName
    ```

## <a name="create-the-probe-nat-rules-and-lb-rules"></a><span data-ttu-id="8f7aa-156">Tworzenie sondowania, reguł NAT oraz zasady równoważeniem obciążenia</span><span class="sxs-lookup"><span data-stu-id="8f7aa-156">Create the probe, NAT rules, and LB rules</span></span>

<span data-ttu-id="8f7aa-157">W tym przykładzie opisano tworzenie następujących elementów:</span><span class="sxs-lookup"><span data-stu-id="8f7aa-157">This example creates the following items:</span></span>

* <span data-ttu-id="8f7aa-158">zasada sondowania, aby sprawdzić połączenie z portem TCP 80 z</span><span class="sxs-lookup"><span data-stu-id="8f7aa-158">a probe rule to check for connectivity to TCP port 80</span></span>
* <span data-ttu-id="8f7aa-159">regułę NAT do tłumaczenia cały ruch przychodzący na porcie 3389 do portu 3389 protokołu RDP<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="8f7aa-159">a NAT rule to translate all incoming traffic on port 3389 to port 3389 for RDP<sup>1</sup></span></span>
* <span data-ttu-id="8f7aa-160">regułę NAT do tłumaczenia cały ruch przychodzący na porcie 3391 do portu 3389 protokołu RDP<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="8f7aa-160">a NAT rule to translate all incoming traffic on port 3391 to port 3389 for RDP<sup>1</sup></span></span>
* <span data-ttu-id="8f7aa-161">Reguła modułu równoważenia obciążenia do równoważenia całego ruchu przychodzącego do portu 80 na port 80 adresów w puli zaplecza.</span><span class="sxs-lookup"><span data-stu-id="8f7aa-161">a load balancer rule to balance all incoming traffic on port 80 to port 80 on the addresses in the back-end pool.</span></span>

<span data-ttu-id="8f7aa-162"><sup>1</sup> Reguły NAT są powiązane z konkretnym wystąpieniem maszyny wirtualnej za modułem równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="8f7aa-162"><sup>1</sup> NAT rules are associated to a specific virtual machine instance behind the load balancer.</span></span> <span data-ttu-id="8f7aa-163">Ruch sieciowy przychodzące do portu 3389 są wysyłane do określonej maszyny wirtualnej i skojarzonych z reguły NAT portu.</span><span class="sxs-lookup"><span data-stu-id="8f7aa-163">The network traffic arriving on port 3389 is sent to the specific virtual machine and port associated with the NAT rule.</span></span> <span data-ttu-id="8f7aa-164">Musisz określić protokół (UDP lub TCP) dla reguły NAT.</span><span class="sxs-lookup"><span data-stu-id="8f7aa-164">You must specify a protocol (UDP or TCP) for a NAT rule.</span></span> <span data-ttu-id="8f7aa-165">Nie można przypisać obu protokołów do tego samego portu.</span><span class="sxs-lookup"><span data-stu-id="8f7aa-165">Both protocols can't be assigned to the same port.</span></span>

1. <span data-ttu-id="8f7aa-166">Ustawianie zmiennych środowiska PowerShell</span><span class="sxs-lookup"><span data-stu-id="8f7aa-166">Set up the PowerShell variables</span></span>

    ```powershell
    $probeV4V6Name = "ProbeForIPv4AndIPv6"
    $natRule1V4Name = "NatRule-For-Rdp-VM1"
    $natRule2V4Name = "NatRule-For-Rdp-VM2"
    $lbRule1V4Name = "LBRuleForIPv4-Port80"
    $lbRule1V6Name = "LBRuleForIPv6-Port80"
    ```

2. <span data-ttu-id="8f7aa-167">Utwórz sondy</span><span class="sxs-lookup"><span data-stu-id="8f7aa-167">Create the probe</span></span>

    <span data-ttu-id="8f7aa-168">Poniższy przykład tworzy sondowaniem TCP, który umożliwia sprawdzenie połączenia zaplecza port TCP 80 co 15 s.</span><span class="sxs-lookup"><span data-stu-id="8f7aa-168">The following example creates a TCP probe that checks for connectivity to back-end TCP port 80 every 15 seconds.</span></span> <span data-ttu-id="8f7aa-169">Go spowoduje oznaczenie zasobów zaplecza niedostępne po dwóch kolejnych błędów.</span><span class="sxs-lookup"><span data-stu-id="8f7aa-169">It will mark the back-end resource unavailable after two consecutive failures.</span></span>

    ```azurecli
    $probeV4V6 = azure network lb probe create --resource-group $rgname --name $probeV4V6Name --protocol tcp --port 80 --interval 15 --count 2 --lb-name $lbName
    ```

3. <span data-ttu-id="8f7aa-170">Tworzenie reguły NAT ruchu przychodzącego zezwalających na połączenia RDP do zasobów wewnętrznych</span><span class="sxs-lookup"><span data-stu-id="8f7aa-170">Create inbound NAT rules that allow RDP connections to the back-end resources</span></span>

    ```azurecli
    $inboundNatRuleRdp1 = azure network lb inbound-nat-rule create --resource-group $rgname --name $natRule1V4Name --frontend-ip-name $frontendV4Name --protocol Tcp --frontend-port 3389 --backend-port 3389 --lb-name $lbName
    $inboundNatRuleRdp2 = azure network lb inbound-nat-rule create --resource-group $rgname --name $natRule2V4Name --frontend-ip-name $frontendV4Name --protocol Tcp --frontend-port 3391 --backend-port 3389 --lb-name $lbName
    ```

4. <span data-ttu-id="8f7aa-171">Tworzenie reguł, które przesyłają dane do różnych portów zaplecza w zależności od których serwer sieci Web odebrał żądanie usługi równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="8f7aa-171">Create a load balancer rules that send traffic to different back-end ports depending on which front end received the request</span></span>

    ```azurecli
    $lbruleIPv4 = azure network lb rule create --resource-group $rgname --name $lbRule1V4Name --frontend-ip-name $frontendV4Name --backend-address-pool-name $backendAddressPoolV4Name --probe-name $probeV4V6Name --protocol Tcp --frontend-port 80 --backend-port 80 --lb-name $lbName
    $lbruleIPv6 = azure network lb rule create --resource-group $rgname --name $lbRule1V6Name --frontend-ip-name $frontendV6Name --backend-address-pool-name $backendAddressPoolV6Name --probe-name $probeV4V6Name --protocol Tcp --frontend-port 80 --backend-port 8080 --lb-name $lbName
    ```

5. <span data-ttu-id="8f7aa-172">Sprawdź ustawienia</span><span class="sxs-lookup"><span data-stu-id="8f7aa-172">Check your settings</span></span>

    ```azurecli
    azure network lb show --resource-group $rgName --name $lbName
    ```

    <span data-ttu-id="8f7aa-173">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="8f7aa-173">Expected output:</span></span>

        info:    Executing command network lb show
        info:    Looking up the load balancer "myIPv4IPv6Lb"
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

## <a name="create-nics"></a><span data-ttu-id="8f7aa-174">Tworzenie kart sieciowych</span><span class="sxs-lookup"><span data-stu-id="8f7aa-174">Create NICs</span></span>

<span data-ttu-id="8f7aa-175">Tworzenie kart sieciowych i kojarzyć je z reguł NAT, reguły modułu równoważenia obciążenia i sondy.</span><span class="sxs-lookup"><span data-stu-id="8f7aa-175">Create NICs and associate them to NAT rules, load balancer rules, and probes.</span></span>

1. <span data-ttu-id="8f7aa-176">Ustawianie zmiennych środowiska PowerShell</span><span class="sxs-lookup"><span data-stu-id="8f7aa-176">Set up the PowerShell variables</span></span>

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

2. <span data-ttu-id="8f7aa-177">Utwórz kartę Sieciową dla każdej zaplecza, a następnie dodaj konfiguracji protokołu IPv6.</span><span class="sxs-lookup"><span data-stu-id="8f7aa-177">Create a NIC for each back-end and add an IPv6 configuration.</span></span>

    ```azurecli
    $nic1 = azure network nic create --name $nic1Name --resource-group $rgname --location $location --private-ip-version "IPv4" --subnet-id $subnet1Id --lb-address-pool-ids $backendAddressPoolV4Id --lb-inbound-nat-rule-ids $natRule1V4Id
    $nic1IPv6 = azure network nic ip-config create --resource-group $rgname --name "IPv6IPConfig" --private-ip-version "IPv6" --lb-address-pool-ids $backendAddressPoolV6Id --nic-name $nic1Name

    $nic2 = azure network nic create --name $nic2Name --resource-group $rgname --location $location --subnet-id $subnet1Id --lb-address-pool-ids $backendAddressPoolV4Id --lb-inbound-nat-rule-ids $natRule2V4Id
    $nic2IPv6 = azure network nic ip-config create --resource-group $rgname --name "IPv6IPConfig" --private-ip-version "IPv6" --lb-address-pool-ids $backendAddressPoolV6Id --nic-name $nic2Name
    ```

## <a name="create-the-back-end-vm-resources-and-attach-each-nic"></a><span data-ttu-id="8f7aa-178">Tworzenie zaplecza zasobów maszyny Wirtualnej i dołączyć poszczególne karty Sieciowe</span><span class="sxs-lookup"><span data-stu-id="8f7aa-178">Create the back-end VM resources and attach each NIC</span></span>

<span data-ttu-id="8f7aa-179">Aby utworzyć maszyny wirtualne, musi mieć konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="8f7aa-179">To create VMs, you must have a storage account.</span></span> <span data-ttu-id="8f7aa-180">W przypadku równoważenia obciążenia maszyn wirtualnych muszą być członkami zestawu dostępności.</span><span class="sxs-lookup"><span data-stu-id="8f7aa-180">For load balancing, the VMs need to be members of an availability set.</span></span> <span data-ttu-id="8f7aa-181">Aby uzyskać więcej informacji na temat tworzenia maszyn wirtualnych, zobacz [tworzenia maszyny Wirtualnej platformy Azure przy użyciu programu PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="8f7aa-181">For more information about creating VMs, see [Create an Azure VM using PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json)</span></span>

1. <span data-ttu-id="8f7aa-182">Ustawianie zmiennych środowiska PowerShell</span><span class="sxs-lookup"><span data-stu-id="8f7aa-182">Set up the PowerShell variables</span></span>

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
    > <span data-ttu-id="8f7aa-183">W tym przykładzie używa nazwy użytkownika i hasła dla maszyn wirtualnych w postaci zwykłego tekstu.</span><span class="sxs-lookup"><span data-stu-id="8f7aa-183">This example uses the username and password for the VMs in clear text.</span></span> <span data-ttu-id="8f7aa-184">Odpowiednie należy uważać podczas przy użyciu poświadczeń niezabezpieczona.</span><span class="sxs-lookup"><span data-stu-id="8f7aa-184">Appropriate care must be taken when using credentials in the clear.</span></span> <span data-ttu-id="8f7aa-185">Aby uzyskać bardziej bezpieczne metody obsługi poświadczenia w programie PowerShell, zobacz [Get-Credential](https://technet.microsoft.com/library/hh849815.aspx) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="8f7aa-185">For a more secure method of handling credentials in PowerShell, see the [Get-Credential](https://technet.microsoft.com/library/hh849815.aspx) cmdlet.</span></span>

2. <span data-ttu-id="8f7aa-186">Tworzenie zestawu dostępności i konto magazynu</span><span class="sxs-lookup"><span data-stu-id="8f7aa-186">Create the storage account and availability set</span></span>

    <span data-ttu-id="8f7aa-187">Podczas tworzenia maszyn wirtualnych, może użyć istniejącego konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="8f7aa-187">You may use an existing storage account when you create the VMs.</span></span> <span data-ttu-id="8f7aa-188">Poniższe polecenie tworzy nowe konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="8f7aa-188">The following command creates a new storage account.</span></span>

    ```azurecli
    $storageAcc = azure storage account create $storageAccountName --resource-group $rgName --location $location --sku-name "LRS" --kind "Storage"
    ```

    <span data-ttu-id="8f7aa-189">Następnie można utworzyć zestawu dostępności.</span><span class="sxs-lookup"><span data-stu-id="8f7aa-189">Next, create the availability set.</span></span>

    ```azurecli
    $availabilitySet = azure availset create --name $availabilitySetName --resource-group $rgName --location $location
    ```

3. <span data-ttu-id="8f7aa-190">Tworzenie maszyn wirtualnych z skojarzone kartami sieciowymi</span><span class="sxs-lookup"><span data-stu-id="8f7aa-190">Create the virtual machines with the associated NICs</span></span>

    ```azurecli
    $vm1 = azure vm create --resource-group $rgname --location $location --availset-name $availabilitySetName --name $vm1Name --nic-id $nic1Id --os-disk-vhd $osDisk1Uri --os-type "Windows" --admin-username $vmUserName --admin-password $mySecurePassword --vm-size "Standard_A1" --image-urn $imageurn --storage-account-name $storageAccountName --disable-bginfo-extension

    $vm2 = azure vm create --resource-group $rgname --location $location --availset-name $availabilitySetName --name $vm2Name --nic-id $nic2Id --os-disk-vhd $osDisk2Uri --os-type "Windows" --admin-username $vmUserName --admin-password $mySecurePassword --vm-size "Standard_A1" --image-urn $imageurn --storage-account-name $storageAccountName --disable-bginfo-extension
    ```

## <a name="next-steps"></a><span data-ttu-id="8f7aa-191">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="8f7aa-191">Next steps</span></span>

<span data-ttu-id="8f7aa-192">[Get started configuring an internal load balancer](load-balancer-get-started-ilb-arm-cli.md) (Wprowadzenie do konfigurowania wewnętrznego modułu równoważenia obciążenia)</span><span class="sxs-lookup"><span data-stu-id="8f7aa-192">[Get started configuring an internal load balancer](load-balancer-get-started-ilb-arm-cli.md)</span></span>

<span data-ttu-id="8f7aa-193">[Configure a load balancer distribution mode](load-balancer-distribution-mode.md) (Konfigurowanie trybu dystrybucji modułu równoważenia obciążenia)</span><span class="sxs-lookup"><span data-stu-id="8f7aa-193">[Configure a load balancer distribution mode](load-balancer-distribution-mode.md)</span></span>

<span data-ttu-id="8f7aa-194">[Configure idle TCP timeout settings for your load balancer](load-balancer-tcp-idle-timeout.md) (Konfigurowanie ustawień limitu czasu bezczynności protokołu TCP dla modułu równoważenia obciążenia)</span><span class="sxs-lookup"><span data-stu-id="8f7aa-194">[Configure idle TCP timeout settings for your load balancer](load-balancer-tcp-idle-timeout.md)</span></span>
