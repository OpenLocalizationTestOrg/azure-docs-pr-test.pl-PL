---
title: aaaOpen porty tooa maszyny Wirtualnej systemu Linux 2.0 interfejsu wiersza polecenia platformy Azure | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak tooopen portu / create tooyour punktu końcowego maszyny Wirtualnej systemu Linux przy użyciu wdrażania Menedżera zasobów Azure hello modelu i hello Azure CLI 2.0"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: eef9842b-495a-46cf-99a6-74e49807e74e
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 08/21/2017
ms.author: iainfou
ms.openlocfilehash: c79b31206e97558171609cf033bb3cb3370777c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="open-ports-and-endpoints-tooa-linux-vm-with-hello-azure-cli"></a><span data-ttu-id="0ce82-103">Otwórz porty i punkty końcowe tooa maszyny Wirtualnej systemu Linux z hello wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="0ce82-103">Open ports and endpoints tooa Linux VM with hello Azure CLI</span></span>
<span data-ttu-id="0ce82-104">Otwarcie portu lub tworzenie punktu końcowego tooa maszyny wirtualnej (VM) na platformie Azure przez utworzenie filtru sieci w podsieci lub interfejsu sieciowego maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="0ce82-104">You open a port, or create an endpoint, tooa virtual machine (VM) in Azure by creating a network filter on a subnet or VM network interface.</span></span> <span data-ttu-id="0ce82-105">Te filtry, które kontrolują ruchu przychodzącego i wychodzącego, należy umieścić na zasób toohello dołączony sieciowej grupy zabezpieczeń, który odbiera ruch hello.</span><span class="sxs-lookup"><span data-stu-id="0ce82-105">You place these filters, which control both inbound and outbound traffic, on a Network Security Group attached toohello resource that receives hello traffic.</span></span> <span data-ttu-id="0ce82-106">Użyjmy typowym przykładem ruchu w sieci web na porcie 80.</span><span class="sxs-lookup"><span data-stu-id="0ce82-106">Let's use a common example of web traffic on port 80.</span></span> <span data-ttu-id="0ce82-107">W tym artykule opisano sposób tooopen tooa portu maszyny Wirtualnej z hello Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="0ce82-107">This article shows you how tooopen a port tooa VM with hello Azure CLI 2.0.</span></span> <span data-ttu-id="0ce82-108">Można również wykonać te kroki hello [Azure CLI 1.0](nsg-quickstart-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="0ce82-108">You can also perform these steps with hello [Azure CLI 1.0](nsg-quickstart-nodejs.md).</span></span>


## <a name="quick-commands"></a><span data-ttu-id="0ce82-109">Szybkie polecenia</span><span class="sxs-lookup"><span data-stu-id="0ce82-109">Quick commands</span></span>
<span data-ttu-id="0ce82-110">Grupy zabezpieczeń sieci toocreate i potrzebnych reguł hello najnowszych [Azure CLI 2.0](/cli/azure/install-az-cli2) zainstalowane i zarejestrowane za pomocą konta Azure tooan [logowania az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="0ce82-110">toocreate a Network Security Group and rules you need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="0ce82-111">Poniższe przykłady w hello Zastąp przykładowe nazwy parametrów własne wartości.</span><span class="sxs-lookup"><span data-stu-id="0ce82-111">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="0ce82-112">Przykład nazwy parametru zawierają *myResourceGroup*, *myNetworkSecurityGroup*, i *myVnet*.</span><span class="sxs-lookup"><span data-stu-id="0ce82-112">Example parameter names include *myResourceGroup*, *myNetworkSecurityGroup*, and *myVnet*.</span></span>

<span data-ttu-id="0ce82-113">Utwórz grupę zabezpieczeń sieci hello z [utworzyć nsg sieci az](/cli/azure/network/nsg#create).</span><span class="sxs-lookup"><span data-stu-id="0ce82-113">Create hello network security group with [az network nsg create](/cli/azure/network/nsg#create).</span></span> <span data-ttu-id="0ce82-114">Witaj poniższy przykład tworzy sieciową grupę zabezpieczeń o nazwie *myNetworkSecurityGroup* w hello *eastus* lokalizacji:</span><span class="sxs-lookup"><span data-stu-id="0ce82-114">hello following example creates a network security group named *myNetworkSecurityGroup* in hello *eastus* location:</span></span>

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNetworkSecurityGroup
```

<span data-ttu-id="0ce82-115">Dodaj regułę z [Tworzenie reguły nsg sieci az](/cli/azure/network/nsg/rule#create) tooallow HTTP ruchu tooyour serwer sieci Web (lub dostosować własne scenariusz, takich jak SSH łączności dostępu lub bazy danych).</span><span class="sxs-lookup"><span data-stu-id="0ce82-115">Add a rule with [az network nsg rule create](/cli/azure/network/nsg/rule#create) tooallow HTTP traffic tooyour webserver (or adjust for your own scenario, such as SSH access or database connectivity).</span></span> <span data-ttu-id="0ce82-116">Witaj poniższy przykład powoduje utworzenie reguły o nazwie *myNetworkSecurityGroupRule* tooallow TCP, ruch na porcie 80:</span><span class="sxs-lookup"><span data-stu-id="0ce82-116">hello following example creates a rule named *myNetworkSecurityGroupRule* tooallow TCP traffic on port 80:</span></span>

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRule \
    --protocol tcp \
    --priority 1000 \
    --destination-port-range 80
```

<span data-ttu-id="0ce82-117">Skojarz hello sieciową grupę zabezpieczeń z maszyny Wirtualnej interfejsu sieciowego (NIC) z [aktualizacji kart sieciowych az](/cli/azure/network/nic#update).</span><span class="sxs-lookup"><span data-stu-id="0ce82-117">Associate hello Network Security Group with your VM's network interface (NIC) with [az network nic update](/cli/azure/network/nic#update).</span></span> <span data-ttu-id="0ce82-118">Witaj poniższy przykład powoduje skojarzenie istniejącej karty NIC o nazwie *myNic* z hello sieciową grupę zabezpieczeń o nazwie *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="0ce82-118">hello following example associates an existing NIC named *myNic* with hello Network Security Group named *myNetworkSecurityGroup*:</span></span>

```azurecli
az network nic update \
    --resource-group myResourceGroup \
    --name myNic \
    --network-security-group myNetworkSecurityGroup
```

<span data-ttu-id="0ce82-119">Alternatywnie można skojarzyć swojej grupy zabezpieczeń sieci z podsiecią sieci wirtualnej z [zaktualizować podsieci sieci wirtualnej sieci az](/cli/azure/network/vnet/subnet#update) zamiast właśnie toohello interfejsu sieciowego na jednej maszynie Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="0ce82-119">Alternatively, you can associate your Network Security Group with a virtual network subnet with [az network vnet subnet update](/cli/azure/network/vnet/subnet#update) rather than just toohello network interface on a single VM.</span></span> <span data-ttu-id="0ce82-120">Witaj poniższy przykład powoduje skojarzenie istniejącą podsieć o nazwie *mySubnet* w hello *myVnet* sieci wirtualnej z hello sieciową grupę zabezpieczeń o nazwie *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="0ce82-120">hello following example associates an existing subnet named *mySubnet* in hello *myVnet* virtual network with hello Network Security Group named *myNetworkSecurityGroup*:</span></span>

```azurecli
az network vnet subnet update \
    --resource-group myResourceGroup \
    --vnet-name myVnet \
    --name mySubnet \
    --network-security-group myNetworkSecurityGroup
```

## <a name="more-information-on-network-security-groups"></a><span data-ttu-id="0ce82-121">Więcej informacji na temat grup zabezpieczeń sieci</span><span class="sxs-lookup"><span data-stu-id="0ce82-121">More information on Network Security Groups</span></span>
<span data-ttu-id="0ce82-122">Witaj w tym miejscu szybkie polecenia pozwalają tooget zapasowych i pracy z tooyour przechodzenia ruchu maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="0ce82-122">hello quick commands here allow you tooget up and running with traffic flowing tooyour VM.</span></span> <span data-ttu-id="0ce82-123">Grupy zabezpieczeń sieci stanowią wielu funkcje i poziom szczegółowości kontrolowanie dostęp do zasobów tooyour.</span><span class="sxs-lookup"><span data-stu-id="0ce82-123">Network Security Groups provide many great features and granularity for controlling access tooyour resources.</span></span> <span data-ttu-id="0ce82-124">Możesz przeczytać dodatkowe informacje [Tworzenie grupy zabezpieczeń sieci i listy ACL zasady tutaj](tutorial-virtual-network.md#secure-network-traffic).</span><span class="sxs-lookup"><span data-stu-id="0ce82-124">You can read more about [creating a Network Security Group and ACL rules here](tutorial-virtual-network.md#secure-network-traffic).</span></span>

<span data-ttu-id="0ce82-125">Dla aplikacji sieci web wysokiej dostępności należy umieszczać maszyny wirtualne za usługą równoważenia obciążenia Azure.</span><span class="sxs-lookup"><span data-stu-id="0ce82-125">For highly available web applications, you should place your VMs behind an Azure Load Balancer.</span></span> <span data-ttu-id="0ce82-126">Moduł równoważenia obciążenia Hello dystrybuuje tooVMs ruchu, z sieciową grupą zabezpieczeń, który umożliwia filtrowanie ruchu.</span><span class="sxs-lookup"><span data-stu-id="0ce82-126">hello load balancer distributes traffic tooVMs, with a Network Security Group that provides traffic filtering.</span></span> <span data-ttu-id="0ce82-127">Aby uzyskać więcej informacji, zobacz [jak maszyn saldo tooload wirtualnych systemu Linux, w Azure toocreate wysokiej dostępności aplikacji](tutorial-load-balancer.md).</span><span class="sxs-lookup"><span data-stu-id="0ce82-127">For more information, see [How tooload balance Linux virtual machines in Azure toocreate a highly available application](tutorial-load-balancer.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="0ce82-128">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="0ce82-128">Next steps</span></span>
<span data-ttu-id="0ce82-129">W tym przykładzie utworzono ruch tooallow HTTP Prosta reguła.</span><span class="sxs-lookup"><span data-stu-id="0ce82-129">In this example, you created a simple rule tooallow HTTP traffic.</span></span> <span data-ttu-id="0ce82-130">Można znaleźć informacje dotyczące tworzenia środowisk bardziej szczegółowe w hello następujące artykuły:</span><span class="sxs-lookup"><span data-stu-id="0ce82-130">You can find information on creating more detailed environments in hello following articles:</span></span>

* [<span data-ttu-id="0ce82-131">Omówienie usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="0ce82-131">Azure Resource Manager overview</span></span>](../../azure-resource-manager/resource-group-overview.md)
* [<span data-ttu-id="0ce82-132">Co to jest sieciowa grupa zabezpieczeń?</span><span class="sxs-lookup"><span data-stu-id="0ce82-132">What is a Network Security Group (NSG)?</span></span>](../../virtual-network/virtual-networks-nsg.md)
