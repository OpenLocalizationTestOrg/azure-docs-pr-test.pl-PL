---
title: "aaaOpen portów tooa maszynę Wirtualną przy użyciu hello portalu Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooopen portu / create tooyour punktu końcowego maszyny Wirtualnej systemu Windows przy użyciu modelu wdrażania Menedżera zasobów hello w hello portalu Azure"
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: f7cf0319-5ee7-435e-8f94-c484bf5ee6f1
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 08/21/2017
ms.author: iainfou
ms.openlocfilehash: aba789c65254651899aa688f256fe616c3d0126d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooopen-ports-tooa-virtual-machine-with-hello-azure-portal"></a><span data-ttu-id="8192c-103">Jak tooopen porty tooa maszynę wirtualną z hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="8192c-103">How tooopen ports tooa virtual machine with hello Azure portal</span></span>
[!INCLUDE [virtual-machines-common-nsg-quickstart](../../../includes/virtual-machines-common-nsg-quickstart.md)]

## <a name="quick-commands"></a><span data-ttu-id="8192c-104">Szybkie polecenia</span><span class="sxs-lookup"><span data-stu-id="8192c-104">Quick commands</span></span>
<span data-ttu-id="8192c-105">Możesz również [wykonaj te czynności przy użyciu programu Azure PowerShell](nsg-quickstart-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="8192c-105">You can also [perform these steps using Azure PowerShell](nsg-quickstart-powershell.md).</span></span>

<span data-ttu-id="8192c-106">Najpierw należy utworzyć grupy zabezpieczeń sieci.</span><span class="sxs-lookup"><span data-stu-id="8192c-106">First, create your Network Security Group.</span></span> <span data-ttu-id="8192c-107">Wybierz, wybierz grupę zasobów, w portalu hello **Dodaj**, następnie wyszukaj i wybierz **sieciowej grupy zabezpieczeń**:</span><span class="sxs-lookup"><span data-stu-id="8192c-107">Select a resource group in hello portal, choose **Add**, then search for and select **Network security group**:</span></span>

![Dodaj grupę zabezpieczeń sieci](./media/nsg-quickstart-portal/add-nsg.png)

<span data-ttu-id="8192c-109">Wprowadź nazwę dla swojej grupy zabezpieczeń sieci, wybierz lub Utwórz grupę zasobów, a następnie wybierz lokalizację.</span><span class="sxs-lookup"><span data-stu-id="8192c-109">Enter a name for your Network Security Group, select or create a resource group, and select a location.</span></span> <span data-ttu-id="8192c-110">Wybierz **Utwórz** po zakończeniu:</span><span class="sxs-lookup"><span data-stu-id="8192c-110">Select **Create** when finished:</span></span>

![Utwórz grupę zabezpieczeń sieci](./media/nsg-quickstart-portal/create-nsg.png)

<span data-ttu-id="8192c-112">Wybierz nową grupę zabezpieczeń sieci.</span><span class="sxs-lookup"><span data-stu-id="8192c-112">Select your new Network Security Group.</span></span> <span data-ttu-id="8192c-113">Wybierz "Reguły zabezpieczeń ruchu przychodzącego", a następnie wybierz hello **Dodaj** toocreate przycisk reguły:</span><span class="sxs-lookup"><span data-stu-id="8192c-113">Select 'Inbound security rules', then select hello **Add** button toocreate a rule:</span></span>

![Dodaj regułę ruchu przychodzącego](./media/nsg-quickstart-portal/add-inbound-rule.png)

<span data-ttu-id="8192c-115">Wybierz popularne **usługi** z menu rozwijanego hello, takich jak *HTTP*.</span><span class="sxs-lookup"><span data-stu-id="8192c-115">Choose a common **Service** from hello drop-down menu, such as *HTTP*.</span></span> <span data-ttu-id="8192c-116">Możesz też wybrać *niestandardowy* tooprovide toouse określonego portu.</span><span class="sxs-lookup"><span data-stu-id="8192c-116">You can also select *Custom* tooprovide a specific port toouse.</span></span> <span data-ttu-id="8192c-117">W razie potrzeby można zmienić priorytet hello lub nazwy.</span><span class="sxs-lookup"><span data-stu-id="8192c-117">If desired, change hello priority or name.</span></span> <span data-ttu-id="8192c-118">Witaj priorytet ma wpływ hello kolejności w której reguły są stosowane - hello niższą wartość liczbową hello, hello wcześniejszych hello jest stosowana reguła.</span><span class="sxs-lookup"><span data-stu-id="8192c-118">hello priority affects hello order in which rules are applied - hello lower hello numerical value, hello earlier hello rule is applied.</span></span> <span data-ttu-id="8192c-119">Możesz też wybrać **zaawansowane** u góry tego ekranu tooenter hello określonego źródła zakres bloku lub portu IP, na przykład.</span><span class="sxs-lookup"><span data-stu-id="8192c-119">You can also select **Advanced** at hello top of this screen tooenter a specific source IP block or port range, for example.</span></span> <span data-ttu-id="8192c-120">Gdy wszystko będzie gotowe, wybierz **OK** toocreate hello reguły:</span><span class="sxs-lookup"><span data-stu-id="8192c-120">When you are ready, select **OK** toocreate hello rule:</span></span>

![Utwórz regułę ruchu przychodzącego](./media/nsg-quickstart-portal/create-inbound-rule.png)

<span data-ttu-id="8192c-122">Z ostatnim krokiem jest tooassociate grupy zabezpieczeń sieci z podsiecią lub w konkretnym interfejsie sieciowym.</span><span class="sxs-lookup"><span data-stu-id="8192c-122">Your final step is tooassociate your Network Security Group with a subnet or a specific network interface.</span></span> <span data-ttu-id="8192c-123">Umożliwia kojarzenie hello sieciową grupę zabezpieczeń z podsiecią.</span><span class="sxs-lookup"><span data-stu-id="8192c-123">Let's associate hello Network Security Group with a subnet.</span></span> <span data-ttu-id="8192c-124">Wybierz **podsieci**, a następnie wybierz **skojarzyć**:</span><span class="sxs-lookup"><span data-stu-id="8192c-124">Select **Subnets**, then choose **Associate**:</span></span>

![Skojarzenia sieciowej grupy zabezpieczeń z podsiecią](./media/nsg-quickstart-portal/associate-subnet.png)

<span data-ttu-id="8192c-126">Wybierz sieci wirtualnej, a następnie wybierz odpowiednie podsieci hello:</span><span class="sxs-lookup"><span data-stu-id="8192c-126">Select your virtual network, and then select hello appropriate subnet:</span></span>

![Kojarzenie grupy zabezpieczeń sieci z obsługą sieci wirtualnej](./media/nsg-quickstart-portal/select-vnet-subnet.png)

<span data-ttu-id="8192c-128">Teraz utworzono grupę zabezpieczeń sieci, utworzyć regułę ruchu przychodzącego, która zezwala na ruch na porcie 80, a jego skojarzony z podsiecią.</span><span class="sxs-lookup"><span data-stu-id="8192c-128">You have now created a Network Security Group, created an inbound rule that allows traffic on port 80, and associated it with a subnet.</span></span> <span data-ttu-id="8192c-129">Wszystkie maszyny wirtualne połączyć toothat podsieci są dostępne na porcie 80.</span><span class="sxs-lookup"><span data-stu-id="8192c-129">Any VMs you connect toothat subnet are reachable on port 80.</span></span>

## <a name="more-information-on-network-security-groups"></a><span data-ttu-id="8192c-130">Więcej informacji na temat grup zabezpieczeń sieci</span><span class="sxs-lookup"><span data-stu-id="8192c-130">More information on Network Security Groups</span></span>
<span data-ttu-id="8192c-131">Witaj w tym miejscu szybkie polecenia pozwalają tooget zapasowych i pracy z tooyour przechodzenia ruchu maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="8192c-131">hello quick commands here allow you tooget up and running with traffic flowing tooyour VM.</span></span> <span data-ttu-id="8192c-132">Grupy zabezpieczeń sieci stanowią wielu funkcje i poziom szczegółowości kontrolowanie dostęp do zasobów tooyour.</span><span class="sxs-lookup"><span data-stu-id="8192c-132">Network Security Groups provide many great features and granularity for controlling access tooyour resources.</span></span> <span data-ttu-id="8192c-133">Możesz przeczytać dodatkowe informacje [Tworzenie grupy zabezpieczeń sieci i listy ACL zasady tutaj](../../virtual-network/virtual-networks-create-nsg-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="8192c-133">You can read more about [creating a Network Security Group and ACL rules here](../../virtual-network/virtual-networks-create-nsg-arm-ps.md).</span></span>

<span data-ttu-id="8192c-134">Dla aplikacji sieci web wysokiej dostępności należy umieszczać maszyny wirtualne za usługą równoważenia obciążenia Azure.</span><span class="sxs-lookup"><span data-stu-id="8192c-134">For highly available web applications, you should place your VMs behind an Azure Load Balancer.</span></span> <span data-ttu-id="8192c-135">Moduł równoważenia obciążenia Hello dystrybuuje tooVMs ruchu, z sieciową grupą zabezpieczeń, który umożliwia filtrowanie ruchu.</span><span class="sxs-lookup"><span data-stu-id="8192c-135">hello load balancer distributes traffic tooVMs, with a Network Security Group that provides traffic filtering.</span></span> <span data-ttu-id="8192c-136">Aby uzyskać więcej informacji, zobacz [jak maszyn saldo tooload wirtualnych systemu Linux, w Azure toocreate wysokiej dostępności aplikacji](tutorial-load-balancer.md).</span><span class="sxs-lookup"><span data-stu-id="8192c-136">For more information, see [How tooload balance Linux virtual machines in Azure toocreate a highly available application](tutorial-load-balancer.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="8192c-137">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="8192c-137">Next steps</span></span>
<span data-ttu-id="8192c-138">W tym przykładzie utworzono ruch tooallow HTTP Prosta reguła.</span><span class="sxs-lookup"><span data-stu-id="8192c-138">In this example, you created a simple rule tooallow HTTP traffic.</span></span> <span data-ttu-id="8192c-139">Można znaleźć informacje dotyczące tworzenia środowisk bardziej szczegółowe w hello następujące artykuły:</span><span class="sxs-lookup"><span data-stu-id="8192c-139">You can find information on creating more detailed environments in hello following articles:</span></span>

* [<span data-ttu-id="8192c-140">Omówienie usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="8192c-140">Azure Resource Manager overview</span></span>](../../azure-resource-manager/resource-group-overview.md)
* [<span data-ttu-id="8192c-141">Co to jest sieciowa grupa zabezpieczeń?</span><span class="sxs-lookup"><span data-stu-id="8192c-141">What is a Network Security Group (NSG)?</span></span>](../../virtual-network/virtual-networks-nsg.md)