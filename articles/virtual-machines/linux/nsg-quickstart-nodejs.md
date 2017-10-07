---
title: aaaOpen porty tooa maszyny Wirtualnej systemu Linux z interfejsu wiersza polecenia platformy Azure w wersji 1.0 | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak tooopen portu / create tooyour punktu końcowego maszyny Wirtualnej systemu Linux przy użyciu wdrażania Menedżera zasobów Azure hello modelu i hello Azure CLI w wersji 1.0"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 337c37d151f527b43d4852291159b2f70a00accc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="opening-ports-and-endpoints-tooa-linux-vm-in-azure-using-hello-azure-cli-10"></a><span data-ttu-id="8cd28-103">Otwieranie portów i punkty końcowe tooa maszyny Wirtualnej systemu Linux platformy Azure przy użyciu hello Azure CLI w wersji 1.0</span><span class="sxs-lookup"><span data-stu-id="8cd28-103">Opening ports and endpoints tooa Linux VM in Azure using hello Azure CLI 1.0</span></span>
<span data-ttu-id="8cd28-104">Otwarcie portu lub tworzenie punktu końcowego tooa maszyny wirtualnej (VM) na platformie Azure przez utworzenie filtru sieci w podsieci lub interfejsu sieciowego maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="8cd28-104">You open a port, or create an endpoint, tooa virtual machine (VM) in Azure by creating a network filter on a subnet or VM network interface.</span></span> <span data-ttu-id="8cd28-105">Te filtry, które kontrolują ruchu przychodzącego i wychodzącego, należy umieścić na zasób toohello dołączony sieciowej grupy zabezpieczeń, który odbiera ruch hello.</span><span class="sxs-lookup"><span data-stu-id="8cd28-105">You place these filters, which control both inbound and outbound traffic, on a Network Security Group attached toohello resource that receives hello traffic.</span></span> <span data-ttu-id="8cd28-106">Użyjmy typowym przykładem ruchu w sieci web na porcie 80.</span><span class="sxs-lookup"><span data-stu-id="8cd28-106">Let's use a common example of web traffic on port 80.</span></span> <span data-ttu-id="8cd28-107">W tym artykule opisano, jak tooopen portu tooa maszynę Wirtualną przy użyciu hello Azure CLI w wersji 1.0.</span><span class="sxs-lookup"><span data-stu-id="8cd28-107">This article shows you how tooopen a port tooa VM using hello Azure CLI 1.0.</span></span>


## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="8cd28-108">Zadanie hello toocomplete wersje interfejsu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="8cd28-108">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="8cd28-109">Można ukończyć powitalnych zadań przy użyciu jednej z hello następujące wersje interfejsu wiersza polecenia:</span><span class="sxs-lookup"><span data-stu-id="8cd28-109">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="8cd28-110">[Azure CLI 1.0](#quick-commands) — nasze interfejsu wiersza polecenia dla hello classic i zasobów zarządzania wdrażania modeli (w tym artykule)</span><span class="sxs-lookup"><span data-stu-id="8cd28-110">[Azure CLI 1.0](#quick-commands) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="8cd28-111">[Azure CLI 2.0](nsg-quickstart.md) -naszej nowej generacji interfejsu wiersza polecenia dla modelu wdrażania zarządzania zasobów hello</span><span class="sxs-lookup"><span data-stu-id="8cd28-111">[Azure CLI 2.0](nsg-quickstart.md) - our next generation CLI for hello resource management deployment model</span></span>


## <a name="quick-commands"></a><span data-ttu-id="8cd28-112">Szybkie polecenia</span><span class="sxs-lookup"><span data-stu-id="8cd28-112">Quick commands</span></span>
<span data-ttu-id="8cd28-113">toocreate sieciowej grupy zabezpieczeń i zasad należy [hello Azure CLI 1.0](../../cli-install-nodejs.md) zainstalowanych i użycie tryb usługi Resource Manager:</span><span class="sxs-lookup"><span data-stu-id="8cd28-113">toocreate a Network Security Group and rules you need [hello Azure CLI 1.0](../../cli-install-nodejs.md) installed and using Resource Manager mode:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="8cd28-114">Poniższe przykłady w hello Zastąp przykładowe nazwy parametrów własne wartości.</span><span class="sxs-lookup"><span data-stu-id="8cd28-114">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="8cd28-115">Przykład nazwy parametrów uwzględnione *myResourceGroup*, *myNetworkSecurityGroup*, i *myVnet*.</span><span class="sxs-lookup"><span data-stu-id="8cd28-115">Example parameter names included *myResourceGroup*, *myNetworkSecurityGroup*, and *myVnet*.</span></span>

<span data-ttu-id="8cd28-116">Utwórz swojej grupy zabezpieczeń sieci, odpowiednio wprowadzania własne nazwy i lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="8cd28-116">Create your Network Security Group, entering your own names and location appropriately.</span></span> <span data-ttu-id="8cd28-117">Witaj poniższy przykład tworzy sieciową grupę zabezpieczeń o nazwie *myNetworkSecurityGroup* w hello *eastus* lokalizacji:</span><span class="sxs-lookup"><span data-stu-id="8cd28-117">hello following example creates a Network Security Group named *myNetworkSecurityGroup* in hello *eastus* location:</span></span>

```azurecli
azure network nsg create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNetworkSecurityGroup
```

<span data-ttu-id="8cd28-118">Dodaj regułę tooallow HTTP ruchu tooyour serwer sieci Web (lub dostosować własne scenariusz, takich jak SSH łączności dostępu lub bazy danych).</span><span class="sxs-lookup"><span data-stu-id="8cd28-118">Add a rule tooallow HTTP traffic tooyour webserver (or adjust for your own scenario, such as SSH access or database connectivity).</span></span> <span data-ttu-id="8cd28-119">Witaj poniższy przykład powoduje utworzenie reguły o nazwie *myNetworkSecurityGroupRule* tooallow TCP, ruch na porcie 80:</span><span class="sxs-lookup"><span data-stu-id="8cd28-119">hello following example creates a rule named *myNetworkSecurityGroupRule* tooallow TCP traffic on port 80:</span></span>

```azurecli
azure network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRule \
    --protocol tcp \
    --direction inbound \
    --priority 1000 \
    --destination-port-range 80 \
    --access allow
```

<span data-ttu-id="8cd28-120">Skojarz hello sieciową grupę zabezpieczeń z maszyny Wirtualnej interfejsu sieciowego (NIC).</span><span class="sxs-lookup"><span data-stu-id="8cd28-120">Associate hello Network Security Group with your VM's network interface (NIC).</span></span> <span data-ttu-id="8cd28-121">Witaj poniższy przykład powoduje skojarzenie istniejącej karty NIC o nazwie *myNic* z hello sieciową grupę zabezpieczeń o nazwie *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="8cd28-121">hello following example associates an existing NIC named *myNic* with hello Network Security Group named *myNetworkSecurityGroup*:</span></span>

```azurecli
azure network nic set \
    --resource-group myResourceGroup \
    --network-security-group-name myNetworkSecurityGroup \
    --name myNic
```

<span data-ttu-id="8cd28-122">Alternatywnie można skojarzyć swojej grupy zabezpieczeń sieci z podsieci sieci wirtualnej, a nie tylko toohello interfejsu sieciowego na jednej maszynie Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="8cd28-122">Alternatively, you can associate your Network Security Group with a virtual network subnet rather than just toohello network interface on a single VM.</span></span> <span data-ttu-id="8cd28-123">Witaj poniższy przykład powoduje skojarzenie istniejącą podsieć o nazwie *mySubnet* w hello *myVnet* sieci wirtualnej z hello sieciową grupę zabezpieczeń o nazwie *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="8cd28-123">hello following example associates an existing subnet named *mySubnet* in hello *myVnet* virtual network with hello Network Security Group named *myNetworkSecurityGroup*:</span></span>

```azurecli
azure network vnet subnet set \
    --resource-group myResourceGroup \
    --network-security-group-name myNetworkSecurityGroup \
    --vnet-name myVnet --name mySubnet
```

## <a name="more-information-on-network-security-groups"></a><span data-ttu-id="8cd28-124">Więcej informacji na temat grup zabezpieczeń sieci</span><span class="sxs-lookup"><span data-stu-id="8cd28-124">More information on Network Security Groups</span></span>
<span data-ttu-id="8cd28-125">Witaj w tym miejscu szybkie polecenia pozwalają tooget zapasowych i pracy z tooyour przechodzenia ruchu maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="8cd28-125">hello quick commands here allow you tooget up and running with traffic flowing tooyour VM.</span></span> <span data-ttu-id="8cd28-126">Grupy zabezpieczeń sieci stanowią wielu funkcje i poziom szczegółowości kontrolowanie dostęp do zasobów tooyour.</span><span class="sxs-lookup"><span data-stu-id="8cd28-126">Network Security Groups provide many great features and granularity for controlling access tooyour resources.</span></span> <span data-ttu-id="8cd28-127">Możesz przeczytać dodatkowe informacje [Tworzenie grupy zabezpieczeń sieci i listy ACL zasady tutaj](../../virtual-network/virtual-networks-create-nsg-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="8cd28-127">You can read more about [creating a Network Security Group and ACL rules here](../../virtual-network/virtual-networks-create-nsg-arm-cli.md).</span></span>

<span data-ttu-id="8cd28-128">Grupy zabezpieczeń sieci i reguły list kontroli dostępu można zdefiniować jako część szablonów usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="8cd28-128">You can define Network Security Groups and ACL rules as part of Azure Resource Manager templates.</span></span> <span data-ttu-id="8cd28-129">Przeczytaj więcej na temat [tworzenie grup zabezpieczeń sieci z szablonami](../../virtual-network/virtual-networks-create-nsg-arm-template.md).</span><span class="sxs-lookup"><span data-stu-id="8cd28-129">Read more about [creating Network Security Groups with templates](../../virtual-network/virtual-networks-create-nsg-arm-template.md).</span></span>

<span data-ttu-id="8cd28-130">Jeśli potrzebujesz toouse przekierowania portów toomap unikatowy portu zewnętrznego portu wewnętrznego tooan na maszynie Wirtualnej, użyj modułu równoważenia obciążenia i reguły translatora adresów sieciowych (NAT).</span><span class="sxs-lookup"><span data-stu-id="8cd28-130">If you need toouse port-forwarding toomap a unique external port tooan internal port on your VM, use a load balancer and Network Address Translation (NAT) rules.</span></span> <span data-ttu-id="8cd28-131">Może na przykład mają tooexpose port TCP 8080 zewnętrznie i mieć ruch skierowany tooTCP port 80 na maszynie Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="8cd28-131">For example, you may want tooexpose TCP port 8080 externally and have traffic directed tooTCP port 80 on a VM.</span></span> <span data-ttu-id="8cd28-132">Informacje na temat [tworzenia modułu równoważenia obciążenia internetowy](../../load-balancer/load-balancer-get-started-internet-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="8cd28-132">You can learn about [creating an Internet-facing load balancer](../../load-balancer/load-balancer-get-started-internet-arm-cli.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="8cd28-133">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="8cd28-133">Next steps</span></span>
<span data-ttu-id="8cd28-134">W tym przykładzie utworzono ruch tooallow HTTP Prosta reguła.</span><span class="sxs-lookup"><span data-stu-id="8cd28-134">In this example, you created a simple rule tooallow HTTP traffic.</span></span> <span data-ttu-id="8cd28-135">Można znaleźć informacje dotyczące tworzenia środowisk bardziej szczegółowe w hello następujące artykuły:</span><span class="sxs-lookup"><span data-stu-id="8cd28-135">You can find information on creating more detailed environments in hello following articles:</span></span>

* [<span data-ttu-id="8cd28-136">Omówienie usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="8cd28-136">Azure Resource Manager overview</span></span>](../../azure-resource-manager/resource-group-overview.md)
* [<span data-ttu-id="8cd28-137">Co to jest sieciowa grupa zabezpieczeń?</span><span class="sxs-lookup"><span data-stu-id="8cd28-137">What is a Network Security Group (NSG)?</span></span>](../../virtual-network/virtual-networks-nsg.md)
* [<span data-ttu-id="8cd28-138">Omówienie usługi Azure Resource Manager dla usługi równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="8cd28-138">Azure Resource Manager Overview for Load Balancers</span></span>](../../load-balancer/load-balancer-arm.md)

