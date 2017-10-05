---
title: "Otwieranie portów z maszyną wirtualną przy użyciu programu Azure PowerShell | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak otworzyć port / utworzyć punktu końcowego maszyny Wirtualnej systemu Windows przy użyciu wdrożeń w trybie Menedżera zasobów platformy Azure i programu Azure PowerShell"
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
ms.openlocfilehash: e818e3b3c707e1471d6f580f8379a277d3575b89
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-open-ports-and-endpoints-to-a-vm-in-azure-using-powershell"></a><span data-ttu-id="f88f8-103">Jak otworzyć porty i punktów końcowych do maszyny Wirtualnej na platformie Azure przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="f88f8-103">How to open ports and endpoints to a VM in Azure using PowerShell</span></span>
[!INCLUDE [virtual-machines-common-nsg-quickstart](../../../includes/virtual-machines-common-nsg-quickstart.md)]

## <a name="quick-commands"></a><span data-ttu-id="f88f8-104">Szybkie polecenia</span><span class="sxs-lookup"><span data-stu-id="f88f8-104">Quick commands</span></span>
<span data-ttu-id="f88f8-105">Aby utworzyć grupę zabezpieczeń sieci i listy ACL zasady należy [najnowszą wersję programu Azure PowerShell zainstalowany](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="f88f8-105">To create a Network Security Group and ACL rules you need [the latest version of Azure PowerShell installed](/powershell/azureps-cmdlets-docs).</span></span> <span data-ttu-id="f88f8-106">Możesz również [wykonaj te czynności przy użyciu portalu Azure](nsg-quickstart-portal.md).</span><span class="sxs-lookup"><span data-stu-id="f88f8-106">You can also [perform these steps using the Azure portal](nsg-quickstart-portal.md).</span></span>

<span data-ttu-id="f88f8-107">Zaloguj się do konta platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="f88f8-107">Log in to your Azure account:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="f88f8-108">W poniższych przykładach Zastąp przykładowe nazwy parametrów własne wartości.</span><span class="sxs-lookup"><span data-stu-id="f88f8-108">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="f88f8-109">Przykład nazwy parametrów uwzględnione *myResourceGroup*, *myNetworkSecurityGroup*, i *myVnet*.</span><span class="sxs-lookup"><span data-stu-id="f88f8-109">Example parameter names included *myResourceGroup*, *myNetworkSecurityGroup*, and *myVnet*.</span></span>

<span data-ttu-id="f88f8-110">Utworzyć regułę z [AzureRmNetworkSecurityRuleConfig nowy](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig).</span><span class="sxs-lookup"><span data-stu-id="f88f8-110">Create a rule with [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig).</span></span> <span data-ttu-id="f88f8-111">Poniższy przykład tworzy reguły o nazwie *myNetworkSecurityGroupRule* umożliwia *tcp* ruch na porcie *80*:</span><span class="sxs-lookup"><span data-stu-id="f88f8-111">The following example creates a rule named *myNetworkSecurityGroupRule* to allow *tcp* traffic on port *80*:</span></span>

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

<span data-ttu-id="f88f8-112">Następnie utwórz grupy zabezpieczeń sieci z [AzureRmNetworkSecurityGroup nowy](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) i Przypisz reguły HTTP utworzony w następujący sposób.</span><span class="sxs-lookup"><span data-stu-id="f88f8-112">Next, create your Network Security group with [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) and assign the HTTP rule you just created as follows.</span></span> <span data-ttu-id="f88f8-113">Poniższy przykład tworzy sieciową grupę zabezpieczeń o nazwie *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="f88f8-113">The following example creates a Network Security Group named *myNetworkSecurityGroup*:</span></span>

```powershell
$nsg = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName "myResourceGroup" `
    -Location "EastUS" `
    -Name "myNetworkSecurityGroup" `
    -SecurityRules $httprule
```

<span data-ttu-id="f88f8-114">Teraz umożliwia przypisywanie sieciowej grupy zabezpieczeń do podsieci.</span><span class="sxs-lookup"><span data-stu-id="f88f8-114">Now let's assign your Network Security Group to a subnet.</span></span> <span data-ttu-id="f88f8-115">W poniższym przykładzie przypisano istniejącej sieci wirtualnej o nazwie *myVnet* do zmiennej *$vnet* z [Get-AzureRmVirtualNetwork](/powershell/module/azurerm.network/get-azurermvirtualnetwork):</span><span class="sxs-lookup"><span data-stu-id="f88f8-115">The following example assigns an existing virtual network named *myVnet* to the variable *$vnet* with [Get-AzureRmVirtualNetwork](/powershell/module/azurerm.network/get-azurermvirtualnetwork):</span></span>

```powershell
$vnet = Get-AzureRmVirtualNetwork `
    -ResourceGroupName "myResourceGroup" `
    -Name "myVnet"
```

<span data-ttu-id="f88f8-116">Skojarz grupy zabezpieczeń sieci z podsieci z [AzureRmVirtualNetworkSubnetConfig zestawu](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig).</span><span class="sxs-lookup"><span data-stu-id="f88f8-116">Associate your Network Security Group with your subnet with [Set-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig).</span></span> <span data-ttu-id="f88f8-117">Poniższy przykład powoduje skojarzenie podsieci o nazwie *mySubnet* z grupy zabezpieczeń sieci:</span><span class="sxs-lookup"><span data-stu-id="f88f8-117">The following example associates the subnet named *mySubnet* with your Network Security Group:</span></span>

```powershell
$subnetPrefix = $vnet.Subnets|?{$_.Name -eq 'mySubnet'}

Set-AzureRmVirtualNetworkSubnetConfig `
    -VirtualNetwork $vnet `
    -Name "mySubnet" `
    -AddressPrefix $subnetPrefix.AddressPrefix `
    -NetworkSecurityGroup $nsg
```

<span data-ttu-id="f88f8-118">Na koniec, aktualizacja sieci wirtualnej z [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork) aby zmiany zaczęły obowiązywać:</span><span class="sxs-lookup"><span data-stu-id="f88f8-118">Finally, update your virtual network with [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork) in order for your changes to take effect:</span></span>

```powershell
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
```


## <a name="more-information-on-network-security-groups"></a><span data-ttu-id="f88f8-119">Więcej informacji na temat grup zabezpieczeń sieci</span><span class="sxs-lookup"><span data-stu-id="f88f8-119">More information on Network Security Groups</span></span>
<span data-ttu-id="f88f8-120">Szybkie polecenia tutaj pozwala rozpocząć pracę z ruchem przepływać do maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="f88f8-120">The quick commands here allow you to get up and running with traffic flowing to your VM.</span></span> <span data-ttu-id="f88f8-121">Grupy zabezpieczeń sieci zapewniają wiele funkcje i poziom szczegółowości kontrolowania dostępu do zasobów.</span><span class="sxs-lookup"><span data-stu-id="f88f8-121">Network Security Groups provide many great features and granularity for controlling access to your resources.</span></span> <span data-ttu-id="f88f8-122">Możesz przeczytać dodatkowe informacje [Tworzenie grupy zabezpieczeń sieci i listy ACL zasady tutaj](tutorial-virtual-network.md#manage-internal-traffic).</span><span class="sxs-lookup"><span data-stu-id="f88f8-122">You can read more about [creating a Network Security Group and ACL rules here](tutorial-virtual-network.md#manage-internal-traffic).</span></span>

<span data-ttu-id="f88f8-123">Dla aplikacji sieci web wysokiej dostępności należy umieszczać maszyny wirtualne za usługą równoważenia obciążenia Azure.</span><span class="sxs-lookup"><span data-stu-id="f88f8-123">For highly available web applications, you should place your VMs behind an Azure Load Balancer.</span></span> <span data-ttu-id="f88f8-124">Moduł równoważenia obciążenia dystrybuuje ruch do maszyn wirtualnych z sieciową grupą zabezpieczeń, który umożliwia filtrowanie ruchu.</span><span class="sxs-lookup"><span data-stu-id="f88f8-124">The load balancer distributes traffic to VMs, with a Network Security Group that provides traffic filtering.</span></span> <span data-ttu-id="f88f8-125">Aby uzyskać więcej informacji, zobacz [jak załadować saldo maszyn wirtualnych systemu Linux na platformie Azure, aby utworzyć aplikację wysokiej dostępności](tutorial-load-balancer.md).</span><span class="sxs-lookup"><span data-stu-id="f88f8-125">For more information, see [How to load balance Linux virtual machines in Azure to create a highly available application](tutorial-load-balancer.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f88f8-126">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f88f8-126">Next steps</span></span>
<span data-ttu-id="f88f8-127">W tym przykładzie utworzono prosta Reguła zezwalająca na ruch HTTP.</span><span class="sxs-lookup"><span data-stu-id="f88f8-127">In this example, you created a simple rule to allow HTTP traffic.</span></span> <span data-ttu-id="f88f8-128">Można znaleźć informacje dotyczące tworzenia środowisk bardziej szczegółowe zawierają następujące artykuły:</span><span class="sxs-lookup"><span data-stu-id="f88f8-128">You can find information on creating more detailed environments in the following articles:</span></span>

* [<span data-ttu-id="f88f8-129">Omówienie usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="f88f8-129">Azure Resource Manager overview</span></span>](../../azure-resource-manager/resource-group-overview.md)
* [<span data-ttu-id="f88f8-130">Co to jest sieciowa grupa zabezpieczeń?</span><span class="sxs-lookup"><span data-stu-id="f88f8-130">What is a Network Security Group (NSG)?</span></span>](../../virtual-network/virtual-networks-nsg.md)
* [<span data-ttu-id="f88f8-131">Omówienie usługi Azure Resource Manager dla usługi równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="f88f8-131">Azure Resource Manager Overview for Load Balancers</span></span>](../../load-balancer/load-balancer-arm.md)

