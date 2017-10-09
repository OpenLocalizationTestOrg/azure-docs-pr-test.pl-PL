---
title: "Moduł równoważenia - obciążenia aaaCreate internetowy, wiersza polecenia platformy Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate Internet równoważenia obciążenia w Menedżerze zasobów przy użyciu hello wiersza polecenia platformy Azure"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: a8bcdd88-f94c-4537-8143-c710eaa86818
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: cadb5edb3b4a4e2f0813109d027eaafdc7ef7303
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-internet-load-balancer-using-hello-azure-cli"></a><span data-ttu-id="7c0cd-103">Tworzenie usługi równoważenia obciążenia internet przy użyciu hello wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="7c0cd-103">Creating an internet load balancer using hello Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="7c0cd-104">Portal</span><span class="sxs-lookup"><span data-stu-id="7c0cd-104">Portal</span></span>](../load-balancer/load-balancer-get-started-internet-portal.md)
> * [<span data-ttu-id="7c0cd-105">Program PowerShell</span><span class="sxs-lookup"><span data-stu-id="7c0cd-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-internet-arm-ps.md)
> * [<span data-ttu-id="7c0cd-106">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="7c0cd-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-internet-arm-cli.md)
> * [<span data-ttu-id="7c0cd-107">Szablon</span><span class="sxs-lookup"><span data-stu-id="7c0cd-107">Template</span></span>](../load-balancer/load-balancer-get-started-internet-arm-template.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="7c0cd-108">W tym artykule omówiono modelu wdrażania usługi Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="7c0cd-108">This article covers hello Resource Manager deployment model.</span></span> <span data-ttu-id="7c0cd-109">Możesz również [Dowiedz się, jak usługa równoważenia przy użyciu klasycznego wdrożenia obciążenia toocreate umożliwiających dostęp z Internetu](load-balancer-get-started-internet-classic-portal.md)</span><span class="sxs-lookup"><span data-stu-id="7c0cd-109">You can also [Learn how toocreate an Internet facing load balancer using classic deployment](load-balancer-get-started-internet-classic-portal.md)</span></span>

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="deploying-hello-solution-using-hello-azure-cli"></a><span data-ttu-id="7c0cd-110">Wdrażanie rozwiązania hello przy użyciu hello wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="7c0cd-110">Deploying hello solution using hello Azure CLI</span></span>

<span data-ttu-id="7c0cd-111">Witaj następujące kroki pokazują, jak toocreate Internetem obciążenia przy użyciu usługi Azure Resource Manager z interfejsu wiersza polecenia usługi równoważenia.</span><span class="sxs-lookup"><span data-stu-id="7c0cd-111">hello following steps show how toocreate an Internet facing load balancer using Azure Resource Manager with CLI.</span></span> <span data-ttu-id="7c0cd-112">Z usługi Azure Resource Manager wszystkie zasoby, zostało utworzone i skonfigurowane osobno, następnie opracować toocreate zasobu.</span><span class="sxs-lookup"><span data-stu-id="7c0cd-112">With Azure Resource Manager each resource is created and configured individually, then put together toocreate a resource.</span></span>

<span data-ttu-id="7c0cd-113">Należy utworzyć i skonfigurować hello następujące obiekty toodeploy modułu równoważenia obciążenia:</span><span class="sxs-lookup"><span data-stu-id="7c0cd-113">You must create and configure hello following objects toodeploy a load balancer:</span></span>

* <span data-ttu-id="7c0cd-114">Konfiguracja IP frontonu — publiczne adresy IP dla przychodzącego ruchu sieciowego.</span><span class="sxs-lookup"><span data-stu-id="7c0cd-114">Front-end IP configuration - contains public IP addresses for incoming network traffic.</span></span>
* <span data-ttu-id="7c0cd-115">Pula adresów zaplecza — zawiera interfejsów sieciowych (NIC) dla ruchu sieciowego tooreceive hello maszyn wirtualnych z hello modułu równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="7c0cd-115">Back-end address pool - contains network interfaces (NICs) for hello virtual machines tooreceive network traffic from hello load balancer.</span></span>
* <span data-ttu-id="7c0cd-116">Reguły równoważenia obciążenia — zawiera reguły mapowania port publiczny na tooport usługi równoważenia obciążenia hello hello puli adresów zaplecza.</span><span class="sxs-lookup"><span data-stu-id="7c0cd-116">Load balancing rules - contains rules mapping a public port on hello load balancer tooport in hello back-end address pool.</span></span>
* <span data-ttu-id="7c0cd-117">Reguły NAT dla ruchu przychodzącego — zawiera reguły mapowania port publiczny na porcie programu tooa usługi równoważenia obciążenia w hello dla określonej maszyny wirtualnej w puli adresów zaplecza hello.</span><span class="sxs-lookup"><span data-stu-id="7c0cd-117">Inbound NAT rules - contains rules mapping a public port on hello load balancer tooa port for a specific virtual machine in hello back-end address pool.</span></span>
* <span data-ttu-id="7c0cd-118">Sondy — zawiera dostępności toocheck badania używane kondycji wystąpień maszyn wirtualnych w puli adresów zaplecza hello.</span><span class="sxs-lookup"><span data-stu-id="7c0cd-118">Probes - contains health probes used toocheck availability of virtual machines instances in hello back-end address pool.</span></span>

<span data-ttu-id="7c0cd-119">Aby uzyskać więcej informacji, zobacz artykuł [Azure Resource Manager support for Load Balancer](load-balancer-arm.md) (Obsługa usługi Azure Resource Manager dla modułu równoważenia obciążenia).</span><span class="sxs-lookup"><span data-stu-id="7c0cd-119">For more information see [Azure Resource Manager support for Load Balancer](load-balancer-arm.md).</span></span>

## <a name="set-up-cli-toouse-resource-manager"></a><span data-ttu-id="7c0cd-120">Konfigurowanie toouse interfejsu wiersza polecenia Menedżera zasobów</span><span class="sxs-lookup"><span data-stu-id="7c0cd-120">Set up CLI toouse Resource Manager</span></span>

1. <span data-ttu-id="7c0cd-121">Jeśli po raz pierwszy używasz interfejsu wiersza polecenia Azure, zobacz [Instalowanie i Konfigurowanie interfejsu wiersza polecenia Azure hello](../cli-install-nodejs.md) i wykonaj instrukcje hello zapasowej punktu toohello, gdzie należy wybrać konto platformy Azure i subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="7c0cd-121">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="7c0cd-122">Uruchom hello **trybie azure config** tooswitch tooResource menedżera trybu poleceń, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="7c0cd-122">Run hello **azure config mode** command tooswitch tooResource Manager mode, as shown below.</span></span>

    ```azurecli
        azure config mode arm
    ```

    <span data-ttu-id="7c0cd-123">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="7c0cd-123">Expected output:</span></span>

        info:    New mode is arm

## <a name="create-a-virtual-network-and-a-public-ip-address-for-hello-front-end-ip-pool"></a><span data-ttu-id="7c0cd-124">Tworzenie sieci wirtualnej i publiczny adres IP dla puli adresów IP frontonu hello</span><span class="sxs-lookup"><span data-stu-id="7c0cd-124">Create a virtual network and a public IP address for hello front-end IP pool</span></span>

1. <span data-ttu-id="7c0cd-125">Utwórz sieć wirtualną (VNet) o nazwie *NRPVnet* w lokalizacji wschodnie stany USA hello za pomocą grupy zasobów o nazwie *NRPRG*.</span><span class="sxs-lookup"><span data-stu-id="7c0cd-125">Create a virtual network (VNet) named *NRPVnet* in hello East US location using a resource group named *NRPRG*.</span></span>

    ```azurecli
        azure network vnet create NRPRG NRPVnet eastUS -a 10.0.0.0/16
    ```

    <span data-ttu-id="7c0cd-126">Utwórz podsieć o nazwie *NRPVnetSubnet* z blokiem CIDR 10.0.0.0/24 w sieci *NRPVnet*.</span><span class="sxs-lookup"><span data-stu-id="7c0cd-126">Create a subnet named *NRPVnetSubnet* with a CIDR block of 10.0.0.0/24 in *NRPVnet*.</span></span>

    ```azurecli
        azure network vnet subnet create NRPRG NRPVnet NRPVnetSubnet -a 10.0.0.0/24
    ```

2. <span data-ttu-id="7c0cd-127">Utwórz publiczny adres IP o nazwie *NRPPublicIP* toobe używane przez pulę IP frontonu z nazwą DNS *loadbalancernrp.eastus.cloudapp.azure.com*. poniższe polecenie hello używa hello alokacji statycznych typu i limit czasu bezczynności 4 minut.</span><span class="sxs-lookup"><span data-stu-id="7c0cd-127">Create a public IP address named *NRPPublicIP* toobe used by a front-end IP pool with DNS name *loadbalancernrp.eastus.cloudapp.azure.com*. hello command below uses hello static allocation type and idle timeout of 4 minutes.</span></span>

    ```azurecli
        azure network public-ip create -g NRPRG -n NRPPublicIP -l eastus -d loadbalancernrp -a static -i 4
    ```

   > [!IMPORTANT]
   > <span data-ttu-id="7c0cd-128">usługi równoważenia obciążenia Hello użyje hello etykieta domeny publicznego adresu IP hello jako nazwy FQDN.</span><span class="sxs-lookup"><span data-stu-id="7c0cd-128">hello load balancer will use hello domain label of hello public IP as its FQDN.</span></span> <span data-ttu-id="7c0cd-129">Ta zmiana wdrożenie klasyczne, używa usługi w chmurze hello hello równoważenia obciążenia w pełni kwalifikowanej domeny nazwę (FQDN).</span><span class="sxs-lookup"><span data-stu-id="7c0cd-129">This a change from classic deployment, which uses hello cloud service as hello load balancer Fully Qualified Domain Name (FQDN).</span></span>
   > <span data-ttu-id="7c0cd-130">W tym przykładzie hello nazwy FQDN jest *loadbalancernrp.eastus.cloudapp.azure.com*.</span><span class="sxs-lookup"><span data-stu-id="7c0cd-130">In this example, hello FQDN is *loadbalancernrp.eastus.cloudapp.azure.com*.</span></span>

## <a name="create-a-load-balancer"></a><span data-ttu-id="7c0cd-131">Tworzenie modułu równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="7c0cd-131">Create a load balancer</span></span>

<span data-ttu-id="7c0cd-132">Witaj poniższe polecenie tworzy moduł równoważenia obciążenia o nazwie *NRPlb* w hello *NRPRG* grupy zasobów w hello *wschodnie stany USA* lokalizacji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="7c0cd-132">hello following command creates a load balancer named *NRPlb* in hello *NRPRG* resource group in hello *East US* Azure location.</span></span>

    ```azurecli
    azure network lb create NRPRG NRPlb eastus
    ```

## <a name="create-a-front-end-ip-pool-and-a-backend-address-pool"></a><span data-ttu-id="7c0cd-133">Tworzenie puli adresów IP frontonu i puli adresów zaplecza</span><span class="sxs-lookup"><span data-stu-id="7c0cd-133">Create a front-end IP pool and a backend address pool</span></span>
<span data-ttu-id="7c0cd-134">W tym przykładzie pokazano, jak toocreate hello frontonu puli adresów IP odbierająca hello przychodzącego ruchu sieciowego na powitania modułu równoważenia obciążenia i hello puli adresów IP zaplecza, gdzie puli frontonu hello wysyła ruch sieciowy hello ze zrównoważonym obciążeniem.</span><span class="sxs-lookup"><span data-stu-id="7c0cd-134">This example demonstrates how toocreate hello front-end IP pool that receives hello incoming network traffic on hello load balancer and hello backend IP pool where hello front-end pool sends hello load balanced network traffic.</span></span>

1. <span data-ttu-id="7c0cd-135">Utwórz pulę IP frontonu skojarzenie publicznego adresu IP hello utworzone w poprzednim kroku hello i hello modułu równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="7c0cd-135">Create a front-end IP pool associating hello public IP created in hello previous step and hello load balancer.</span></span>

    ```azurecli
        azure network lb frontend-ip create nrpRG NRPlb NRPfrontendpool -i nrppublicip
    ```

2. <span data-ttu-id="7c0cd-136">Skonfiguruj pulę adresów zaplecza używane tooreceive ruch przychodzący z puli adresów IP frontonu hello.</span><span class="sxs-lookup"><span data-stu-id="7c0cd-136">Set up a back-end address pool used tooreceive incoming traffic from hello front-end IP pool.</span></span>

    ```azurecli
        azure network lb address-pool create NRPRG NRPlb NRPbackendpool
    ```

## <a name="create-lb-rules-nat-rules-and-probe"></a><span data-ttu-id="7c0cd-137">Tworzenie reguł równoważenia obciążenia, reguł NAT oraz sond</span><span class="sxs-lookup"><span data-stu-id="7c0cd-137">Create LB rules, NAT rules, and probe</span></span>

<span data-ttu-id="7c0cd-138">W tym przykładzie tworzy hello następujące elementy.</span><span class="sxs-lookup"><span data-stu-id="7c0cd-138">This example creates hello following items.</span></span>

* <span data-ttu-id="7c0cd-139">translator NAT reguły tootranslate cały ruch przychodzący na porcie 21 tooport 22<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="7c0cd-139">a NAT rule tootranslate all incoming traffic on port 21 tooport 22<sup>1</sup></span></span>
* <span data-ttu-id="7c0cd-140">translator NAT reguły tootranslate cały ruch przychodzący na porcie 23 tooport 22</span><span class="sxs-lookup"><span data-stu-id="7c0cd-140">a NAT rule tootranslate all incoming traffic on port 23 tooport 22</span></span>
* <span data-ttu-id="7c0cd-141">toobalance reguły modułu równoważenia obciążenia cały ruch przychodzący na porcie 80 tooport 80 na powitania adresów w puli zaplecza hello.</span><span class="sxs-lookup"><span data-stu-id="7c0cd-141">a load balancer rule toobalance all incoming traffic on port 80 tooport 80 on hello addresses in hello back-end pool.</span></span>
* <span data-ttu-id="7c0cd-142">stan kondycji sondowania reguł toocheck hello na stronie o nazwie *HealthProbe.aspx*.</span><span class="sxs-lookup"><span data-stu-id="7c0cd-142">a probe rule toocheck hello health status on a page named *HealthProbe.aspx*.</span></span>

<span data-ttu-id="7c0cd-143"><sup>1</sup> reguł NAT są skojarzone tooa wystąpienia określonej maszyny wirtualnej za hello równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="7c0cd-143"><sup>1</sup> NAT rules are associated tooa specific virtual machine instance behind hello load balancer.</span></span> <span data-ttu-id="7c0cd-144">ruch sieciowy Hello przychodzące do portu 21 są wysyłane tooa określonej maszyny wirtualnej na porcie 22 skojarzone z tą regułą translatora adresów Sieciowych.</span><span class="sxs-lookup"><span data-stu-id="7c0cd-144">hello network traffic arriving on port 21 is sent tooa specific virtual machine on port 22 associated with this NAT rule.</span></span> <span data-ttu-id="7c0cd-145">Musisz określić protokół (UDP lub TCP) dla reguły NAT.</span><span class="sxs-lookup"><span data-stu-id="7c0cd-145">You must specify a protocol (UDP or TCP) for a NAT rule.</span></span> <span data-ttu-id="7c0cd-146">Oba protokoły nie może być przypisana toohello tego samego portu.</span><span class="sxs-lookup"><span data-stu-id="7c0cd-146">Both protocols can't be assigned toohello same port.</span></span>

1. <span data-ttu-id="7c0cd-147">Tworzenie reguł NAT hello.</span><span class="sxs-lookup"><span data-stu-id="7c0cd-147">Create hello NAT rules.</span></span>

    ```azurecli
        azure network lb inbound-nat-rule create --resource-group nrprg --lb-name nrplb --name ssh1 --protocol tcp --frontend-port 21 --backend-port 22
        azure network lb inbound-nat-rule create --resource-group nrprg --lb-name nrplb --name ssh2 --protocol tcp --frontend-port 23 --backend-port 22
    ```

2. <span data-ttu-id="7c0cd-148">Utwórz regułę modułu równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="7c0cd-148">Create a load balancer rule.</span></span>

    ```azurecli
        azure network lb rule create --resource-group nrprg --lb-name nrplb --name lbrule --protocol tcp --frontend-port 80 --backend-port 80 --frontend-ip-name NRPfrontendpool --backend-address-pool-name NRPbackendpool
    ```

3. <span data-ttu-id="7c0cd-149">Utwórz sondę kondycji.</span><span class="sxs-lookup"><span data-stu-id="7c0cd-149">Create a health probe.</span></span>

    ```azurecli
        azure network lb probe create --resource-group nrprg --lb-name nrplb --name healthprobe --protocol "http" --port 80 --path healthprobe.aspx --interval 15 --count 4
    ```

4. <span data-ttu-id="7c0cd-150">Sprawdź ustawienia.</span><span class="sxs-lookup"><span data-stu-id="7c0cd-150">Check your settings.</span></span>

    ```azurecli
        azure network lb show nrprg nrplb
    ```

    <span data-ttu-id="7c0cd-151">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="7c0cd-151">Expected output:</span></span>

        info:    Executing command network lb show
        + Looking up hello load balancer "nrplb"
        + Looking up hello public ip "NRPPublicIP"
        data:    Id                              : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb
        data:    Name                            : nrplb
        data:    Type                            : Microsoft.Network/loadBalancers
        data:    Location                        : eastus
        data:    Provisioning State              : Succeeded
        data:    Frontend IP configurations:
        data:      Name                          : NRPfrontendpool
        data:      Provisioning state            : Succeeded
        data:      Public IP address id          : /subscriptions/####################################/resourceGroups/NRPRG/providers/Microsoft.Network/publicIPAddresses/NRPPublicIP
        data:      Public IP allocation method   : Static
        data:      Public IP address             : 40.114.13.145
        data:
        data:    Backend address pools:
        data:      Name                          : NRPbackendpool
        data:      Provisioning state            : Succeeded
        data:
        data:    Load balancing rules:
        data:      Name                          : HTTP
        data:      Provisioning state            : Succeeded
        data:      Protocol                      : Tcp
        data:      Frontend port                 : 80
        data:      Backend port                  : 80
        data:      Enable floating IP            : false
        data:      Idle timeout in minutes       : 4
        data:      Frontend IP configuration     : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/frontendIPConfigurations/NRPfrontendpool
        data:      Backend address pool          : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/NRPbackendpool
        data:
        data:    Inbound NAT rules:
        data:      Name                          : ssh1
        data:      Provisioning state            : Succeeded
        data:      Protocol                      : Tcp
        data:      Frontend port                 : 21
        data:      Backend port                  : 22
        data:      Enable floating IP            : false
        data:      Idle timeout in minutes       : 4
        data:      Frontend IP configuration     : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/frontendIPConfigurations/NRPfrontendpool
        data:
        data:      Name                          : ssh2
        data:      Provisioning state            : Succeeded
        data:      Protocol                      : Tcp
        data:      Frontend port                 : 23
        data:      Backend port                  : 22
        data:      Enable floating IP            : false
        data:      Idle timeout in minutes       : 4
        data:      Frontend IP configuration     : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/frontendIPConfigurations/NRPfrontendpool
        data:
        data:    Probes:
        data:      Name                          : healthprobe
        data:      Provisioning state            : Succeeded
        data:      Protocol                      : Http
        data:      Port                          : 80
        data:      Interval in seconds           : 15
        data:      Number of probes              : 4
        data:
        info:    network lb show command OK

## <a name="create-nics"></a><span data-ttu-id="7c0cd-152">Tworzenie kart sieciowych</span><span class="sxs-lookup"><span data-stu-id="7c0cd-152">Create NICs</span></span>

<span data-ttu-id="7c0cd-153">Należy toocreate karty sieciowe (lub modyfikować istniejące) i kojarzyć je tooNAT reguły, reguły modułu równoważenia obciążenia i sondy.</span><span class="sxs-lookup"><span data-stu-id="7c0cd-153">You need toocreate NICs (or modify existing ones) and associate them tooNAT rules, load balancer rules, and probes.</span></span>

1. <span data-ttu-id="7c0cd-154">Utwórz kartę Sieciową o nazwie *można nic1 lb*i skojarz go z hello *rdp1* NAT reguły i hello *NRPbackendpool* puli adresów zaplecza.</span><span class="sxs-lookup"><span data-stu-id="7c0cd-154">Create a NIC named *lb-nic1-be*, and associate it with hello *rdp1* NAT rule, and hello *NRPbackendpool* back-end address pool.</span></span>

    ```azurecli
        azure network nic create --resource-group nrprg --name lb-nic1-be --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet --lb-address-pool-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/NRPbackendpool" --lb-inbound-nat-rule-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp1" eastus
    ```

    <span data-ttu-id="7c0cd-155">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="7c0cd-155">Expected output:</span></span>

        info:    Executing command network nic create
        + Looking up hello network interface "lb-nic1-be"
        + Looking up hello subnet "nrpvnetsubnet"
        + Creating network interface "lb-nic1-be"
        + Looking up hello network interface "lb-nic1-be"
        data:    Id                              : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/networkInterfaces/lb-nic1-be
        data:    Name                            : lb-nic1-be
        data:    Type                            : Microsoft.Network/networkInterfaces
        data:    Location                        : eastus
        data:    Provisioning state              : Succeeded
        data:    Enable IP forwarding            : false
        data:    IP configurations:
        data:      Name                          : NIC-config
        data:      Provisioning state            : Succeeded
        data:      Private IP address            : 10.0.0.4
        data:      Private IP Allocation Method  : Dynamic
        data:      Subnet                        : /subscriptions/####################################/resourceGroups/NRPRG/providers/Microsoft.Network/virtualNetworks/NRPVnet/subnets/NRPVnetSubnet
        data:      Load balancer backend address pools
        data:        Id                          : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/NRPbackendpool
        data:      Load balancer inbound NAT rules:
        data:        Id                          : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp1
        data:
        info:    network nic create command OK

2. <span data-ttu-id="7c0cd-156">Utwórz kartę Sieciową o nazwie *można nic2 lb*i skojarz go z hello *rdp2* NAT reguły i hello *NRPbackendpool* puli adresów zaplecza.</span><span class="sxs-lookup"><span data-stu-id="7c0cd-156">Create a NIC named *lb-nic2-be*, and associate it with hello *rdp2* NAT rule, and hello *NRPbackendpool* back-end address pool.</span></span>

    ```azurecli
        azure network nic create --resource-group nrprg --name lb-nic2-be --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet --lb-address-pool-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/NRPbackendpool" --lb-inbound-nat-rule-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp2" eastus
    ```

3. <span data-ttu-id="7c0cd-157">Utwórz maszynę wirtualną (VM) o nazwie *web1*i skojarz go z hello karty Sieciowej o nazwie *można nic1 lb*.</span><span class="sxs-lookup"><span data-stu-id="7c0cd-157">Create a virtual machine (VM) named *web1*, and associate it with hello NIC named *lb-nic1-be*.</span></span> <span data-ttu-id="7c0cd-158">Konto magazynu o nazwie *web1nrp* został utworzony przed uruchomieniem polecenia hello poniżej.</span><span class="sxs-lookup"><span data-stu-id="7c0cd-158">A storage account called *web1nrp* was created before running hello command below.</span></span>

    ```azurecli
        azure vm create --resource-group nrprg --name web1 --location eastus --vnet-name nrpvnet --vnet-subnet-name nrpvnetsubnet --nic-name lb-nic1-be --availset-name nrp-avset --storage-account-name web1nrp --os-type Windows --image-urn MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:4.0.20150825
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="7c0cd-159">Maszyny wirtualne w toobe potrzeby modułu równoważenia obciążenia, w hello tego samego zestawu dostępności.</span><span class="sxs-lookup"><span data-stu-id="7c0cd-159">VMs in a load balancer need toobe in hello same availability set.</span></span> <span data-ttu-id="7c0cd-160">Użyj `azure availset create` toocreate zestawu dostępności.</span><span class="sxs-lookup"><span data-stu-id="7c0cd-160">Use `azure availset create` toocreate an availability set.</span></span>

    <span data-ttu-id="7c0cd-161">Hello dane wyjściowe powinny być podobne toohello następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="7c0cd-161">hello output should be similar toohello following:</span></span>

        info:    Executing command vm create
        + Looking up hello VM "web1"
        Enter username: azureuser
        Enter password for azureuser: *********
        Confirm password: *********
        info:    Using hello VM Size "Standard_A1"
        info:    hello [OS, Data] Disk or image configuration requires storage account
        + Looking up hello storage account web1nrp
        + Looking up hello availability set "nrp-avset"
        info:    Found an Availability set "nrp-avset"
        + Looking up hello NIC "lb-nic1-be"
        info:    Found an existing NIC "lb-nic1-be"
        info:    Found an IP configuration with virtual network subnet id "/subscriptions/####################################/resourceGroups/NRPRG/providers/Microsoft.Network/virtualNetworks/NRPVnet/subnets/NRPVnetSubnet" in hello NIC "lb-nic1-be"
        info:    This is a NIC without publicIP configured
        + Creating VM "web1"
        info:    vm create command OK

    > [!NOTE]
    > <span data-ttu-id="7c0cd-162">komunikat informacyjny Hello **jest karta sieciowa bez publicznego adresu IP skonfigurowanych** oczekuje się od chwili utworzenia hello NIC dla usługi równoważenia obciążenia hello łączenie tooInternet przy użyciu hello adres usługi równoważenia obciążenia publicznego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="7c0cd-162">hello informational message **This is a NIC without publicIP configured** is expected since hello NIC created for hello load balancer connecting tooInternet using hello load balancer public IP address.</span></span>

    <span data-ttu-id="7c0cd-163">Od hello *można nic1 lb* kart interfejsu Sieciowego jest skojarzony z hello *rdp1* reguły NAT można się połączyć za*web1* za pomocą protokołu RDP za pośrednictwem portu 3441 na powitania modułu równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="7c0cd-163">Since hello *lb-nic1-be* NIC is associated with hello *rdp1* NAT rule, you can connect too*web1* using RDP through port 3441 on hello load balancer.</span></span>

4. <span data-ttu-id="7c0cd-164">Utwórz maszynę wirtualną (VM) o nazwie *sieci Web 2*i skojarz go z hello karty Sieciowej o nazwie *można nic2 lb*.</span><span class="sxs-lookup"><span data-stu-id="7c0cd-164">Create a virtual machine (VM) named *web2*, and associate it with hello NIC named *lb-nic2-be*.</span></span> <span data-ttu-id="7c0cd-165">Konto magazynu o nazwie *web1nrp* został utworzony przed uruchomieniem polecenia hello poniżej.</span><span class="sxs-lookup"><span data-stu-id="7c0cd-165">A storage account called *web1nrp* was created before running hello command below.</span></span>

    ```azurecli
        azure vm create --resource-group nrprg --name web2 --location eastus --vnet-name nrpvnet --vnet-subnet-name nrpvnetsubnet --nic-name lb-nic2-be --availset-name nrp-avset --storage-account-name web2nrp --os-type Windows --image-urn MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:4.0.20150825
    ```

## <a name="update-an-existing-load-balancer"></a><span data-ttu-id="7c0cd-166">Aktualizowanie istniejącego modułu równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="7c0cd-166">Update an existing load balancer</span></span>
<span data-ttu-id="7c0cd-167">Możesz dodać reguły odwołujące się do istniejącego modułu równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="7c0cd-167">You can add rules referencing an existing load balancer.</span></span> <span data-ttu-id="7c0cd-168">W następnym przykładzie hello, nowe reguły modułu równoważenia obciążenia jest dodawany tooan istniejący moduł równoważenia obciążenia **NRPlb**</span><span class="sxs-lookup"><span data-stu-id="7c0cd-168">In hello next example, a new load balancer rule is added tooan existing load balancer **NRPlb**</span></span>

```azurecli
azure network lb rule create --resource-group nrprg --lb-name nrplb --name lbrule2 --protocol tcp --frontend-port 8080 --backend-port 8051 --frontend-ip-name frontendnrppool --backend-address-pool-name NRPbackendpool
```

## <a name="delete-a-load-balancer"></a><span data-ttu-id="7c0cd-169">Usuwanie modułu równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="7c0cd-169">Delete a load balancer</span></span>
<span data-ttu-id="7c0cd-170">Użyj hello następujące polecenia tooremove modułu równoważenia obciążenia:</span><span class="sxs-lookup"><span data-stu-id="7c0cd-170">Use hello following command tooremove a load balancer:</span></span>

```azurecli
azure network lb delete --resource-group nrprg --name nrplb
```

## <a name="next-steps"></a><span data-ttu-id="7c0cd-171">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="7c0cd-171">Next steps</span></span>
<span data-ttu-id="7c0cd-172">[Get started configuring an internal load balancer](load-balancer-get-started-ilb-arm-cli.md) (Wprowadzenie do konfigurowania wewnętrznego modułu równoważenia obciążenia)</span><span class="sxs-lookup"><span data-stu-id="7c0cd-172">[Get started configuring an internal load balancer](load-balancer-get-started-ilb-arm-cli.md)</span></span>

<span data-ttu-id="7c0cd-173">[Configure a load balancer distribution mode](load-balancer-distribution-mode.md) (Konfigurowanie trybu dystrybucji modułu równoważenia obciążenia)</span><span class="sxs-lookup"><span data-stu-id="7c0cd-173">[Configure a load balancer distribution mode](load-balancer-distribution-mode.md)</span></span>

<span data-ttu-id="7c0cd-174">[Configure idle TCP timeout settings for your load balancer](load-balancer-tcp-idle-timeout.md) (Konfigurowanie ustawień limitu czasu bezczynności protokołu TCP dla modułu równoważenia obciążenia)</span><span class="sxs-lookup"><span data-stu-id="7c0cd-174">[Configure idle TCP timeout settings for your load balancer](load-balancer-tcp-idle-timeout.md)</span></span>
