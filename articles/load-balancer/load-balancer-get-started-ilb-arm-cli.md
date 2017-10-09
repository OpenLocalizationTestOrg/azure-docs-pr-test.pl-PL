---
title: "Moduł równoważenia - obciążenia aaaCreate wewnętrzne, wiersza polecenia platformy Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate wewnętrznego modułu równoważenia obciążenia przy użyciu hello interfejsu wiersza polecenia Azure Resource Manager"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
ms.assetid: c7a24e92-b4da-43c0-90f2-841c1b7ce489
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 3aea6fdb07600f0d661ec6b8ffc784b03380a127
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-internal-load-balancer-by-using-hello-azure-cli"></a><span data-ttu-id="c826a-103">Tworzenie przy użyciu interfejsu wiersza polecenia Azure hello wewnętrznego modułu równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="c826a-103">Create an internal load balancer by using hello Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="c826a-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="c826a-104">Azure Portal</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-portal.md)
> * [<span data-ttu-id="c826a-105">Program PowerShell</span><span class="sxs-lookup"><span data-stu-id="c826a-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-ps.md)
> * [<span data-ttu-id="c826a-106">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="c826a-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-cli.md)
> * [<span data-ttu-id="c826a-107">Szablon</span><span class="sxs-lookup"><span data-stu-id="c826a-107">Template</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-template.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="c826a-108">Platforma Azure oferuje dwa różne modele wdrażania związane z tworzeniem zasobów i pracą z nimi: [model wdrażania przy użyciu usługi Azure Resource Manager i model klasyczny](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="c826a-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="c826a-109">W tym artykule omówiono przy użyciu modelu wdrażania Menedżera zasobów hello, który firma Microsoft zaleca dla większości nowych wdrożeń zamiast hello [klasycznego modelu wdrażania](load-balancer-get-started-ilb-classic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="c826a-109">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello [classic deployment model](load-balancer-get-started-ilb-classic-cli.md).</span></span>

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

## <a name="deploy-hello-solution-by-using-hello-azure-cli"></a><span data-ttu-id="c826a-110">Wdrażanie rozwiązania hello przy użyciu hello wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="c826a-110">Deploy hello solution by using hello Azure CLI</span></span>

<span data-ttu-id="c826a-111">Witaj następujące kroki pokazują, jak toocreate internetowy modułu równoważenia obciążenia za pomocą interfejsu wiersza polecenia przy użyciu usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c826a-111">hello following steps show how toocreate an Internet-facing load balancer by using Azure Resource Manager with CLI.</span></span> <span data-ttu-id="c826a-112">Usługi Azure Resource Manager każdy zasób jest tworzony i skonfigurować osobno, a następnie umieść razem toocreate zasobu.</span><span class="sxs-lookup"><span data-stu-id="c826a-112">With Azure Resource Manager, each resource is created and configured individually, and then put together toocreate a resource.</span></span>

<span data-ttu-id="c826a-113">Należy toocreate i skonfigurować hello następujące obiekty toodeploy modułu równoważenia obciążenia:</span><span class="sxs-lookup"><span data-stu-id="c826a-113">You need toocreate and configure hello following objects toodeploy a load balancer:</span></span>

* <span data-ttu-id="c826a-114">**Konfiguracja adresu IP frontonu** — publiczne adresy IP dla przychodzącego ruchu sieciowego.</span><span class="sxs-lookup"><span data-stu-id="c826a-114">**Front-end IP configuration**: contains public IP addresses for incoming network traffic</span></span>
* <span data-ttu-id="c826a-115">**Pula adresów zaplecza**: zawiera interfejsów sieciowych (NIC), które umożliwiają ruch sieciowy tooreceive hello maszyn wirtualnych z hello modułu równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="c826a-115">**Back-end address pool**: contains network interfaces (NICs) that enable hello virtual machines tooreceive network traffic from hello load balancer</span></span>
* <span data-ttu-id="c826a-116">**Reguły równoważenia obciążenia**: zawiera reguły, które mapują port publiczny na tooport usługi równoważenia obciążenia hello w puli adresów zaplecza hello</span><span class="sxs-lookup"><span data-stu-id="c826a-116">**Load-balancing rules**: contains rules that map a public port on hello load balancer tooport in hello back-end address pool</span></span>
* <span data-ttu-id="c826a-117">**Reguły NAT dla ruchu przychodzącego**: zawiera reguły, które mapują port publiczny na porcie programu tooa usługi równoważenia obciążenia w hello dla określonej maszyny wirtualnej w puli adresów zaplecza hello</span><span class="sxs-lookup"><span data-stu-id="c826a-117">**Inbound NAT rules**: contains rules that map a public port on hello load balancer tooa port for a specific virtual machine in hello back-end address pool</span></span>
* <span data-ttu-id="c826a-118">**Sondy**: zawiera sondy kondycji, które są używane toocheck hello dostępność wystąpień maszyn wirtualnych w puli adresów zaplecza hello</span><span class="sxs-lookup"><span data-stu-id="c826a-118">**Probes**: contains health probes that are used toocheck hello availability of virtual machines instances in hello back-end address pool</span></span>

<span data-ttu-id="c826a-119">Aby uzyskać więcej informacji, zobacz artykuł [Azure Resource Manager support for Load Balancer](load-balancer-arm.md) (Obsługa usługi Azure Resource Manager dla modułu równoważenia obciążenia).</span><span class="sxs-lookup"><span data-stu-id="c826a-119">For more information, see [Azure Resource Manager support for Load Balancer](load-balancer-arm.md).</span></span>

## <a name="set-up-cli-toouse-resource-manager"></a><span data-ttu-id="c826a-120">Konfigurowanie toouse interfejsu wiersza polecenia Menedżera zasobów</span><span class="sxs-lookup"><span data-stu-id="c826a-120">Set up CLI toouse Resource Manager</span></span>

1. <span data-ttu-id="c826a-121">Jeśli po raz pierwszy używasz interfejsu wiersza polecenia Azure, zobacz [zainstalować i skonfigurować hello Azure CLI](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="c826a-121">If you have never used Azure CLI, see [Install and configure hello Azure CLI](../cli-install-nodejs.md).</span></span> <span data-ttu-id="c826a-122">Wykonaj instrukcje hello zapasowej punktu toohello, gdzie należy wybrać konto platformy Azure i subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="c826a-122">Follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="c826a-123">Uruchom hello **trybie azure config** polecenia tooswitch tooResource Menedżera tryb, w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="c826a-123">Run hello **azure config mode** command tooswitch tooResource Manager mode, as follows:</span></span>

    ```azurecli
    azure config mode arm
    ```

    <span data-ttu-id="c826a-124">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="c826a-124">Expected output:</span></span>

        info:    New mode is arm

## <a name="create-an-internal-load-balancer-step-by-step"></a><span data-ttu-id="c826a-125">Tworzenie wewnętrznego modułu równoważenia obciążenia krok po kroku</span><span class="sxs-lookup"><span data-stu-id="c826a-125">Create an internal load balancer step by step</span></span>

1. <span data-ttu-id="c826a-126">Zaloguj się tooAzure.</span><span class="sxs-lookup"><span data-stu-id="c826a-126">Sign in tooAzure.</span></span>

    ```azurecli
    azure login
    ```

    <span data-ttu-id="c826a-127">Po wyświetleniu monitu wprowadź swoje poświadczenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c826a-127">When prompted, enter your Azure credentials.</span></span>

2. <span data-ttu-id="c826a-128">Zmień tryb usługi Resource Manager tooAzure hello polecenia narzędzia.</span><span class="sxs-lookup"><span data-stu-id="c826a-128">Change hello command tools tooAzure Resource Manager mode.</span></span>

    ```azurecli
    azure config mode arm
    ```

## <a name="create-a-resource-group"></a><span data-ttu-id="c826a-129">Tworzenie grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="c826a-129">Create a resource group</span></span>

<span data-ttu-id="c826a-130">Wszystkie zasoby usługi Azure Resource Manager są kojarzone z grupą zasobów.</span><span class="sxs-lookup"><span data-stu-id="c826a-130">All resources in Azure Resource Manager are associated with a resource group.</span></span> <span data-ttu-id="c826a-131">Jeśli jeszcze nie wykonano tej czynności, utwórz grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="c826a-131">If you haven't done so yet, create a resource group.</span></span>

```azurecli
azure group create <resource group name> <location>
```

## <a name="create-an-internal-load-balancer-set"></a><span data-ttu-id="c826a-132">Tworzenie zestawu wewnętrznego modułu równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="c826a-132">Create an internal load balancer set</span></span>

1. <span data-ttu-id="c826a-133">Utwórz wewnętrzny moduł równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="c826a-133">Create an internal load balancer</span></span>

    <span data-ttu-id="c826a-134">W następujących scenariuszy hello grupy zasobów o nazwie nrprg jest tworzony w regionie wschodnie stany USA.</span><span class="sxs-lookup"><span data-stu-id="c826a-134">In hello following scenario, a resource group named nrprg is created in East US region.</span></span>

    ```azurecli
    azure network lb create --name nrprg --location eastus
    ```

   > [!NOTE]
   > <span data-ttu-id="c826a-135">Wszystkie zasoby wewnętrzne moduły równoważenia obciążenia, takich jak sieci wirtualnych i podsieci sieci wirtualnej, musi być w hello tej samej grupie zasobów i w hello sam region.</span><span class="sxs-lookup"><span data-stu-id="c826a-135">All resources for an internal load balancers, such as virtual networks and virtual network subnets, must be in hello same resource group and in hello same region.</span></span>

2. <span data-ttu-id="c826a-136">Utwórz adres IP frontonu w hello wewnętrznego modułu równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="c826a-136">Create a front-end IP address for hello internal load balancer.</span></span>

    <span data-ttu-id="c826a-137">użyty adres IP Hello musi być w zakresie hello podsieci sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c826a-137">hello IP address that you use must be within hello subnet range of your virtual network.</span></span>

    ```azurecli
    azure network lb frontend-ip create --resource-group nrprg --lb-name ilbset --name feilb --private-ip-address 10.0.0.7 --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet
    ```

3. <span data-ttu-id="c826a-138">Utwórz pulę adresów zaplecza hello.</span><span class="sxs-lookup"><span data-stu-id="c826a-138">Create hello back-end address pool.</span></span>

    ```azurecli
    azure network lb address-pool create --resource-group nrprg --lb-name ilbset --name beilb
    ```

    <span data-ttu-id="c826a-139">Po zdefiniowaniu adresu IP frontonu i puli adresów zaplecza możesz utworzyć reguły modułu równoważenia obciążenia, reguły NAT dla ruchu przychodzącego i dostosowane sondy kondycji.</span><span class="sxs-lookup"><span data-stu-id="c826a-139">After you define a front-end IP address and a back-end address pool, you can create load balancer rules, inbound NAT rules, and customized health probes.</span></span>

4. <span data-ttu-id="c826a-140">Utwórz reguły modułu równoważenia obciążenia dla hello wewnętrznego modułu równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="c826a-140">Create a load balancer rule for hello internal load balancer.</span></span>

    <span data-ttu-id="c826a-141">Po wykonaniu poprzednich kroków hello hello polecenie tworzy regułę równoważenia obciążenia dla nasłuchiwania tooport 1433 hello puli frontonu i wysyłania równoważeniem obciążenia ruchu toohello zaplecza puli adresów sieciowych, również przy użyciu portu 1433.</span><span class="sxs-lookup"><span data-stu-id="c826a-141">When you follow hello previous steps, hello command creates a load-balancer rule for listening tooport 1433 in hello front-end pool and sending load-balanced network traffic toohello back-end address pool, also using port 1433.</span></span>

    ```azurecli
    azure network lb rule create --resource-group nrprg --lb-name ilbset --name ilbrule --protocol tcp --frontend-port 1433 --backend-port 1433 --frontend-ip-name feilb --backend-address-pool-name beilb
    ```

5. <span data-ttu-id="c826a-142">Utwórz reguły NAT dla ruchu przychodzącego.</span><span class="sxs-lookup"><span data-stu-id="c826a-142">Create inbound NAT rules.</span></span>

    <span data-ttu-id="c826a-143">Reguły ruchu przychodzącego translatora adresów Sieciowych są używane toocreate punkty końcowe w moduł równoważenia obciążenia wykraczające tooa wystąpienia określonej maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c826a-143">Inbound NAT rules are used toocreate endpoints in a load balancer that go tooa specific virtual machine instance.</span></span> <span data-ttu-id="c826a-144">poprzednie kroki Hello utworzone dwie reguły NAT dla pulpitu zdalnego.</span><span class="sxs-lookup"><span data-stu-id="c826a-144">hello previous steps created two NAT rules  for remote desktop.</span></span>

    ```azurecli
    azure network lb inbound-nat-rule create --resource-group nrprg --lb-name ilbset --name NATrule1 --protocol TCP --frontend-port 5432 --backend-port 3389

    azure network lb inbound-nat-rule create --resource-group nrprg --lb-name ilbset --name NATrule2 --protocol TCP --frontend-port 5433 --backend-port 3389
    ```

6. <span data-ttu-id="c826a-145">Utwórz sondy kondycji dla usługi równoważenia obciążenia hello.</span><span class="sxs-lookup"><span data-stu-id="c826a-145">Create health probes for hello load balancer.</span></span>

    <span data-ttu-id="c826a-146">Sondy kondycji sprawdza wszystkie toomake wystąpień maszyny wirtualnej się, że może wysyłać ruch w sieci.</span><span class="sxs-lookup"><span data-stu-id="c826a-146">A health probe checks all virtual machine instances toomake sure they can send network traffic.</span></span> <span data-ttu-id="c826a-147">Hello wystąpienie maszyny wirtualnej z sondy nie powiodło się sprawdzenie zostanie usunięty z modułu równoważenia obciążenia hello dopiero po jej przejdzie do trybu online i sprawdź sondowania Określa, że jest w dobrej kondycji.</span><span class="sxs-lookup"><span data-stu-id="c826a-147">hello virtual machine instance with failed probe checks is removed from hello load balancer until it goes back online and a probe check determines that it's healthy.</span></span>

    ```azurecli
    azure network lb probe create --resource-group nrprg --lb-name ilbset --name ilbprobe --protocol tcp --interval 300 --count 4
    ```

    > [!NOTE]
    > <span data-ttu-id="c826a-148">platformy Microsoft Azure Hello używa statycznych, publicznie routingu adresów IPv4 dla różnych scenariuszy administracyjnych.</span><span class="sxs-lookup"><span data-stu-id="c826a-148">hello Microsoft Azure platform uses a static, publicly routable IPv4 address for a variety of administrative scenarios.</span></span> <span data-ttu-id="c826a-149">adres IP Hello jest 168.63.129.16.</span><span class="sxs-lookup"><span data-stu-id="c826a-149">hello IP address is 168.63.129.16.</span></span> <span data-ttu-id="c826a-150">Ten adres IP nie powinien być blokowany przez zapory, ponieważ może to spowodować nieoczekiwane zachowanie.</span><span class="sxs-lookup"><span data-stu-id="c826a-150">This IP address should not be blocked by any firewalls, because this can cause unexpected behavior.</span></span>
    > <span data-ttu-id="c826a-151">Równoważenia obciążenia wewnętrznego tooAzure względem ten adres IP jest używana przez monitorowanie sond z stan kondycji hello toodetermine usługi równoważenia obciążenia hello maszyn wirtualnych w zestawie o zrównoważonym obciążeniu.</span><span class="sxs-lookup"><span data-stu-id="c826a-151">With respect tooAzure internal load balancing, this IP address is used by monitoring probes from hello load balancer toodetermine hello health state for virtual machines in a load-balanced set.</span></span> <span data-ttu-id="c826a-152">Jeśli grupa zabezpieczeń sieci jest toorestrict używanych maszyn wirtualnych tooAzure ruchu w zestawie wewnętrznie równoważeniem obciążenia lub zastosowane tooa podsieć sieci wirtualnej, upewnij się, że reguły zabezpieczeń sieci został dodany ruchu tooallow 168.63.129.16.</span><span class="sxs-lookup"><span data-stu-id="c826a-152">If a network security group is used toorestrict traffic tooAzure virtual machines in an internally load-balanced set or is applied tooa virtual network subnet, ensure that a network security rule is added tooallow traffic from 168.63.129.16.</span></span>

## <a name="create-nics"></a><span data-ttu-id="c826a-153">Tworzenie kart sieciowych</span><span class="sxs-lookup"><span data-stu-id="c826a-153">Create NICs</span></span>

<span data-ttu-id="c826a-154">Należy toocreate karty sieciowe (lub modyfikować istniejące) i kojarzyć je tooNAT reguły, reguły modułu równoważenia obciążenia i sondy.</span><span class="sxs-lookup"><span data-stu-id="c826a-154">You need toocreate NICs (or modify existing ones) and associate them tooNAT rules, load balancer rules, and probes.</span></span>

1. <span data-ttu-id="c826a-155">Utwórz kartę Sieciową o nazwie *można nic1 lb*i skojarz ją z hello *rdp1* NAT reguły i hello *beilb* puli adresów zaplecza.</span><span class="sxs-lookup"><span data-stu-id="c826a-155">Create an NIC named *lb-nic1-be*, and then associate it with hello *rdp1* NAT rule and hello *beilb* back-end address pool.</span></span>

    ```azurecli
    azure network nic create --resource-group nrprg --name lb-nic1-be --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet --lb-address-pool-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/beilb" --lb-inbound-nat-rule-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp1" --location eastus
    ```

    <span data-ttu-id="c826a-156">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="c826a-156">Expected output:</span></span>

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

2. <span data-ttu-id="c826a-157">Utwórz kartę Sieciową o nazwie *można nic2 lb*i skojarz ją z hello *rdp2* NAT reguły i hello *beilb* puli adresów zaplecza.</span><span class="sxs-lookup"><span data-stu-id="c826a-157">Create an NIC named *lb-nic2-be*, and then associate it with hello *rdp2* NAT rule and hello *beilb* back-end address pool.</span></span>

    ```azurecli
    azure network nic create --resource-group nrprg --name lb-nic2-be --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet --lb-address-pool-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/beilb" --lb-inbound-nat-rule-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp2" --location eastus
    ```

3. <span data-ttu-id="c826a-158">Utwórz maszynę wirtualną o nazwie *DB1*i skojarz ją z hello karty Sieciowej o nazwie *można nic1 lb*.</span><span class="sxs-lookup"><span data-stu-id="c826a-158">Create a virtual machine named *DB1*, and then associate it with hello NIC named *lb-nic1-be*.</span></span> <span data-ttu-id="c826a-159">Konto magazynu o nazwie *web1nrp* jest utworzony przed powitania po uruchomieniu polecenia:</span><span class="sxs-lookup"><span data-stu-id="c826a-159">A storage account called *web1nrp* is created before hello following command runs:</span></span>

    ```azurecli
    azure vm create --resource--resource-grouproup nrprg --name DB1 --location eastus --vnet-name nrpvnet --vnet-subnet-name nrpvnetsubnet --nic-name lb-nic1-be --availset-name nrp-avset --storage-account-name web1nrp --os-type Windows --image-urn MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:4.0.20150825
    ```
    > [!IMPORTANT]
    > <span data-ttu-id="c826a-160">Maszyny wirtualne w toobe potrzeby modułu równoważenia obciążenia, w hello tego samego zestawu dostępności.</span><span class="sxs-lookup"><span data-stu-id="c826a-160">VMs in a load balancer need toobe in hello same availability set.</span></span> <span data-ttu-id="c826a-161">Użyj `azure availset create` toocreate zestawu dostępności.</span><span class="sxs-lookup"><span data-stu-id="c826a-161">Use `azure availset create` toocreate an availability set.</span></span>

4. <span data-ttu-id="c826a-162">Utwórz maszynę wirtualną (VM) o nazwie *bazy danych DB2*i skojarz ją z hello karty Sieciowej o nazwie *można nic2 lb*.</span><span class="sxs-lookup"><span data-stu-id="c826a-162">Create a virtual machine (VM) named *DB2*, and then associate it with hello NIC named *lb-nic2-be*.</span></span> <span data-ttu-id="c826a-163">Konto magazynu o nazwie *web1nrp* został utworzony przed uruchomieniem hello następujące polecenia.</span><span class="sxs-lookup"><span data-stu-id="c826a-163">A storage account called *web1nrp* was created before running hello following command.</span></span>

    ```azurecli
    azure vm create --resource--resource-grouproup nrprg --name DB2 --location eastus --vnet-name nrpvnet --vnet-subnet-name nrpvnetsubnet --nic-name lb-nic2-be --availset-name nrp-avset --storage-account-name web2nrp --os-type Windows --image-urn MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:4.0.20150825
    ```

## <a name="delete-a-load-balancer"></a><span data-ttu-id="c826a-164">Usuwanie modułu równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="c826a-164">Delete a load balancer</span></span>

<span data-ttu-id="c826a-165">tooremove modułu równoważenia obciążenia, hello Użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="c826a-165">tooremove a load balancer, use hello following command:</span></span>

```azurecli
azure network lb delete --resource-group nrprg --name ilbset
```

## <a name="next-steps"></a><span data-ttu-id="c826a-166">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c826a-166">Next steps</span></span>

<span data-ttu-id="c826a-167">[Configure a load balancer distribution mode by using source IP affinity](load-balancer-distribution-mode.md) (Konfigurowanie trybu dystrybucji modułu równoważenia obciążenia przy użyciu koligacji źródłowych adresów IP)</span><span class="sxs-lookup"><span data-stu-id="c826a-167">[Configure a load balancer distribution mode by using source IP affinity](load-balancer-distribution-mode.md)</span></span>

<span data-ttu-id="c826a-168">[Configure idle TCP timeout settings for your load balancer](load-balancer-tcp-idle-timeout.md) (Konfigurowanie ustawień limitu czasu bezczynności protokołu TCP dla modułu równoważenia obciążenia)</span><span class="sxs-lookup"><span data-stu-id="c826a-168">[Configure idle TCP timeout settings for your load balancer](load-balancer-tcp-idle-timeout.md)</span></span>

