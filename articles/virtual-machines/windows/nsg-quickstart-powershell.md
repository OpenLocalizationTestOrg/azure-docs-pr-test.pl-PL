---
title: "aaaOpen porty tooa maszyny Wirtualnej przy użyciu programu Azure PowerShell | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooopen portu / create tooyour punktu końcowego maszyny Wirtualnej systemu Windows przy użyciu trybie wdrażania Menedżera zasobów Azure hello i programu Azure PowerShell"
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: cf45f7d8-451a-48ab-8419-730366d54f1e
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 08/21/2017
ms.author: iainfou
ms.openlocfilehash: c1817a0c447ae4ce7a1ce2a1fc6927bedf2dacb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooopen-ports-and-endpoints-tooa-vm-in-azure-using-powershell"></a><span data-ttu-id="2fbb6-103">Jak tooopen portów i punkty końcowe tooa maszyny Wirtualnej na platformie Azure przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="2fbb6-103">How tooopen ports and endpoints tooa VM in Azure using PowerShell</span></span>
[!INCLUDE [virtual-machines-common-nsg-quickstart](../../../includes/virtual-machines-common-nsg-quickstart.md)]

## <a name="quick-commands"></a><span data-ttu-id="2fbb6-104">Szybkie polecenia</span><span class="sxs-lookup"><span data-stu-id="2fbb6-104">Quick commands</span></span>
<span data-ttu-id="2fbb6-105">Grupy zabezpieczeń sieci toocreate i reguły listy ACL należy [hello najnowszą wersję programu Azure PowerShell zainstalowany](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="2fbb6-105">toocreate a Network Security Group and ACL rules you need [hello latest version of Azure PowerShell installed](/powershell/azureps-cmdlets-docs).</span></span> <span data-ttu-id="2fbb6-106">Możesz również [wykonaj te czynności przy użyciu portalu Azure hello](nsg-quickstart-portal.md).</span><span class="sxs-lookup"><span data-stu-id="2fbb6-106">You can also [perform these steps using hello Azure portal](nsg-quickstart-portal.md).</span></span>

<span data-ttu-id="2fbb6-107">Zaloguj się tooyour konto platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="2fbb6-107">Log in tooyour Azure account:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="2fbb6-108">Poniższe przykłady w hello Zastąp przykładowe nazwy parametrów własne wartości.</span><span class="sxs-lookup"><span data-stu-id="2fbb6-108">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="2fbb6-109">Przykład nazwy parametrów uwzględnione *myResourceGroup*, *myNetworkSecurityGroup*, i *myVnet*.</span><span class="sxs-lookup"><span data-stu-id="2fbb6-109">Example parameter names included *myResourceGroup*, *myNetworkSecurityGroup*, and *myVnet*.</span></span>

<span data-ttu-id="2fbb6-110">Utworzyć regułę z [AzureRmNetworkSecurityRuleConfig nowy](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig).</span><span class="sxs-lookup"><span data-stu-id="2fbb6-110">Create a rule with [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig).</span></span> <span data-ttu-id="2fbb6-111">Witaj poniższy przykład powoduje utworzenie reguły o nazwie *myNetworkSecurityGroupRule* tooallow *tcp* ruch na porcie *80*:</span><span class="sxs-lookup"><span data-stu-id="2fbb6-111">hello following example creates a rule named *myNetworkSecurityGroupRule* tooallow *tcp* traffic on port *80*:</span></span>

```powershell
$httprule = New-AzureRmNetworkSecurityRuleConfig `
    -Name "myNetworkSecurityGroupRule" `
    -Description "Allow HTTP" `
    -Access "Allow" `
    -Protocol "Tcp" `
    -Direction "Inbound" `
    -Priority "100" `
    -SourceAddressPrefix "Internet" `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 80
```

<span data-ttu-id="2fbb6-112">Następnie utwórz grupy zabezpieczeń sieci z [AzureRmNetworkSecurityGroup nowy](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) i przypisz hello HTTP reguł utworzony w następujący sposób.</span><span class="sxs-lookup"><span data-stu-id="2fbb6-112">Next, create your Network Security group with [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) and assign hello HTTP rule you just created as follows.</span></span> <span data-ttu-id="2fbb6-113">Witaj poniższy przykład tworzy sieciową grupę zabezpieczeń o nazwie *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="2fbb6-113">hello following example creates a Network Security Group named *myNetworkSecurityGroup*:</span></span>

```powershell
$nsg = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName "myResourceGroup" `
    -Location "EastUS" `
    -Name "myNetworkSecurityGroup" `
    -SecurityRules $httprule
```

<span data-ttu-id="2fbb6-114">Teraz załóżmy przypisać podsieć tooa grupy zabezpieczeń sieci.</span><span class="sxs-lookup"><span data-stu-id="2fbb6-114">Now let's assign your Network Security Group tooa subnet.</span></span> <span data-ttu-id="2fbb6-115">Witaj w poniższym przykładzie przypisano istniejącej sieci wirtualnej o nazwie *myVnet* zmiennej toohello *$vnet* z [Get-AzureRmVirtualNetwork](/powershell/module/azurerm.network/get-azurermvirtualnetwork):</span><span class="sxs-lookup"><span data-stu-id="2fbb6-115">hello following example assigns an existing virtual network named *myVnet* toohello variable *$vnet* with [Get-AzureRmVirtualNetwork](/powershell/module/azurerm.network/get-azurermvirtualnetwork):</span></span>

```powershell
$vnet = Get-AzureRmVirtualNetwork `
    -ResourceGroupName "myResourceGroup" `
    -Name "myVnet"
```

<span data-ttu-id="2fbb6-116">Skojarz grupy zabezpieczeń sieci z podsieci z [AzureRmVirtualNetworkSubnetConfig zestawu](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig).</span><span class="sxs-lookup"><span data-stu-id="2fbb6-116">Associate your Network Security Group with your subnet with [Set-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig).</span></span> <span data-ttu-id="2fbb6-117">Witaj poniższy przykład powoduje skojarzenie podsieci hello o nazwie *mySubnet* z grupy zabezpieczeń sieci:</span><span class="sxs-lookup"><span data-stu-id="2fbb6-117">hello following example associates hello subnet named *mySubnet* with your Network Security Group:</span></span>

```powershell
$subnetPrefix = $vnet.Subnets|?{$_.Name -eq 'mySubnet'}

Set-AzureRmVirtualNetworkSubnetConfig `
    -VirtualNetwork $vnet `
    -Name "mySubnet" `
    -AddressPrefix $subnetPrefix.AddressPrefix `
    -NetworkSecurityGroup $nsg
```

<span data-ttu-id="2fbb6-118">Na koniec, aktualizacja sieci wirtualnej z [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork) aby Twoje mocą tootake zmiany:</span><span class="sxs-lookup"><span data-stu-id="2fbb6-118">Finally, update your virtual network with [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork) in order for your changes tootake effect:</span></span>

```powershell
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
```


## <a name="more-information-on-network-security-groups"></a><span data-ttu-id="2fbb6-119">Więcej informacji na temat grup zabezpieczeń sieci</span><span class="sxs-lookup"><span data-stu-id="2fbb6-119">More information on Network Security Groups</span></span>
<span data-ttu-id="2fbb6-120">Witaj w tym miejscu szybkie polecenia pozwalają tooget zapasowych i pracy z tooyour przechodzenia ruchu maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="2fbb6-120">hello quick commands here allow you tooget up and running with traffic flowing tooyour VM.</span></span> <span data-ttu-id="2fbb6-121">Grupy zabezpieczeń sieci stanowią wielu funkcje i poziom szczegółowości kontrolowanie dostęp do zasobów tooyour.</span><span class="sxs-lookup"><span data-stu-id="2fbb6-121">Network Security Groups provide many great features and granularity for controlling access tooyour resources.</span></span> <span data-ttu-id="2fbb6-122">Możesz przeczytać dodatkowe informacje [Tworzenie grupy zabezpieczeń sieci i listy ACL zasady tutaj](tutorial-virtual-network.md#manage-internal-traffic).</span><span class="sxs-lookup"><span data-stu-id="2fbb6-122">You can read more about [creating a Network Security Group and ACL rules here](tutorial-virtual-network.md#manage-internal-traffic).</span></span>

<span data-ttu-id="2fbb6-123">Dla aplikacji sieci web wysokiej dostępności należy umieszczać maszyny wirtualne za usługą równoważenia obciążenia Azure.</span><span class="sxs-lookup"><span data-stu-id="2fbb6-123">For highly available web applications, you should place your VMs behind an Azure Load Balancer.</span></span> <span data-ttu-id="2fbb6-124">Moduł równoważenia obciążenia Hello dystrybuuje tooVMs ruchu, z sieciową grupą zabezpieczeń, który umożliwia filtrowanie ruchu.</span><span class="sxs-lookup"><span data-stu-id="2fbb6-124">hello load balancer distributes traffic tooVMs, with a Network Security Group that provides traffic filtering.</span></span> <span data-ttu-id="2fbb6-125">Aby uzyskać więcej informacji, zobacz [jak maszyn saldo tooload wirtualnych systemu Linux, w Azure toocreate wysokiej dostępności aplikacji](tutorial-load-balancer.md).</span><span class="sxs-lookup"><span data-stu-id="2fbb6-125">For more information, see [How tooload balance Linux virtual machines in Azure toocreate a highly available application](tutorial-load-balancer.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="2fbb6-126">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="2fbb6-126">Next steps</span></span>
<span data-ttu-id="2fbb6-127">W tym przykładzie utworzono ruch tooallow HTTP Prosta reguła.</span><span class="sxs-lookup"><span data-stu-id="2fbb6-127">In this example, you created a simple rule tooallow HTTP traffic.</span></span> <span data-ttu-id="2fbb6-128">Można znaleźć informacje dotyczące tworzenia środowisk bardziej szczegółowe w hello następujące artykuły:</span><span class="sxs-lookup"><span data-stu-id="2fbb6-128">You can find information on creating more detailed environments in hello following articles:</span></span>

* [<span data-ttu-id="2fbb6-129">Omówienie usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="2fbb6-129">Azure Resource Manager overview</span></span>](../../azure-resource-manager/resource-group-overview.md)
* [<span data-ttu-id="2fbb6-130">Co to jest sieciowa grupa zabezpieczeń?</span><span class="sxs-lookup"><span data-stu-id="2fbb6-130">What is a Network Security Group (NSG)?</span></span>](../../virtual-network/virtual-networks-nsg.md)
* [<span data-ttu-id="2fbb6-131">Omówienie usługi Azure Resource Manager dla usługi równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="2fbb6-131">Azure Resource Manager Overview for Load Balancers</span></span>](../../load-balancer/load-balancer-arm.md)

