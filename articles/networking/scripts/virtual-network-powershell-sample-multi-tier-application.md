---
title: "Skrypt programu PowerShell Azure przykładowe — tworzenie sieci dla aplikacji wielowarstwowych | Dokumentacja firmy Microsoft"
description: "Skrypt programu PowerShell Azure przykładowe — tworzenie sieci wirtualnej dla aplikacji wielowarstwowych."
services: virtual-network
documentationcenter: virtual-network
author: georgewallace
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: powershell
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 05/16/2017
ms.author: gwallace
ms.openlocfilehash: ab49e78ef17b093d2bbe4e3276a1ece3a4247f91
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-network-for-multi-tier-applications"></a><span data-ttu-id="dae0c-103">Tworzenie sieci dla aplikacji wielowarstwowych</span><span class="sxs-lookup"><span data-stu-id="dae0c-103">Create a network for multi-tier applications</span></span>

<span data-ttu-id="dae0c-104">Ten przykładowy skrypt tworzy sieć wirtualną z podsieci frontonu i zaplecza.</span><span class="sxs-lookup"><span data-stu-id="dae0c-104">This script sample creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="dae0c-105">Ruch do podsieci frontonu jest ograniczona do HTTP i SSH, gdy ruch do podsieci wewnętrznej jest ograniczony do MySQL, port 3306.</span><span class="sxs-lookup"><span data-stu-id="dae0c-105">Traffic to the front-end subnet is limited to HTTP and SSH, while traffic to the back-end subnet is limited to MySQL, port 3306.</span></span> <span data-ttu-id="dae0c-106">Po uruchomieniu skryptu, masz dwie maszyny wirtualne, w każdej podsieci, którą można wdrożyć serwera sieci web i MySQL oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="dae0c-106">After running the script, you will have two virtual machines, one in each subnet that you can deploy web server and MySQL software to.</span></span>

<span data-ttu-id="dae0c-107">W razie potrzeby zainstalować program Azure PowerShell przy użyciu instrukcji w [Przewodnik programu Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), a następnie uruchom `Login-AzureRmAccount` można utworzyć połączenia z platformą Azure.</span><span class="sxs-lookup"><span data-stu-id="dae0c-107">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="dae0c-108">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="dae0c-108">Sample script</span></span>


<span data-ttu-id="dae0c-109">[!code-powershell[główne](../../../powershell_scripts/virtual-network/virtual-network-multi-tier-application/virtual-network-multi-tier-application.ps1  "sieci wirtualnej dla aplikacji wielowarstwowych")]</span><span class="sxs-lookup"><span data-stu-id="dae0c-109">[!code-powershell[main](../../../powershell_scripts/virtual-network/virtual-network-multi-tier-application/virtual-network-multi-tier-application.ps1  "Virtual network for multi-tier application")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="dae0c-110">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="dae0c-110">Clean up deployment</span></span> 

<span data-ttu-id="dae0c-111">Uruchom następujące polecenie, aby usunąć grupę zasobów, maszyny Wirtualnej i wszystkie powiązane zasoby.</span><span class="sxs-lookup"><span data-stu-id="dae0c-111">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="dae0c-112">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="dae0c-112">Script explanation</span></span>

<span data-ttu-id="dae0c-113">Ten skrypt używa następujących poleceń do utworzenia grupy zasobów, sieć wirtualną i grup zabezpieczeń sieci.</span><span class="sxs-lookup"><span data-stu-id="dae0c-113">This script uses the following commands to create a resource group, virtual network,  and network security groups.</span></span> <span data-ttu-id="dae0c-114">Każde polecenie w tabeli łącza do dokumentacji specyficzne dla polecenia.</span><span class="sxs-lookup"><span data-stu-id="dae0c-114">Each command in the table links to command-specific documentation.</span></span>

| <span data-ttu-id="dae0c-115">Polecenie</span><span class="sxs-lookup"><span data-stu-id="dae0c-115">Command</span></span> | <span data-ttu-id="dae0c-116">Uwagi</span><span class="sxs-lookup"><span data-stu-id="dae0c-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="dae0c-117">Nowe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="dae0c-117">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="dae0c-118">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="dae0c-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="dae0c-119">Nowy AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="dae0c-119">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="dae0c-120">Tworzy sieć wirtualna platformy Azure i podsieci frontonu.</span><span class="sxs-lookup"><span data-stu-id="dae0c-120">Creates an Azure virtual network and front-end subnet.</span></span> |
| [<span data-ttu-id="dae0c-121">Nowe AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="dae0c-121">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="dae0c-122">Tworzy podsieć zaplecza.</span><span class="sxs-lookup"><span data-stu-id="dae0c-122">Creates a back-end subnet.</span></span> |
| [<span data-ttu-id="dae0c-123">Nowe AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="dae0c-123">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="dae0c-124">Tworzy publiczny adres IP na dostęp do maszyny Wirtualnej z Internetu.</span><span class="sxs-lookup"><span data-stu-id="dae0c-124">Creates a public IP address to access the VM from the Internet.</span></span> |
| [<span data-ttu-id="dae0c-125">Nowe AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="dae0c-125">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="dae0c-126">Tworzy interfejsy sieci wirtualnej i dołącza je do podsieci sieci wirtualnej frontonu i zaplecza.</span><span class="sxs-lookup"><span data-stu-id="dae0c-126">Creates virtual network interfaces and attaches them to the virtual network's front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="dae0c-127">Nowe AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="dae0c-127">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="dae0c-128">Tworzy sieciowej grupy zabezpieczeń (NSG), które są skojarzone z podsieci frontonu i zaplecza.</span><span class="sxs-lookup"><span data-stu-id="dae0c-128">Creates network security groups (NSG) that are associated to the front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="dae0c-129">Nowe AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="dae0c-129">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) |<span data-ttu-id="dae0c-130">Tworzy reguły NSG, które zezwala lub blokuje określone porty do określonych podsieci.</span><span class="sxs-lookup"><span data-stu-id="dae0c-130">Creates NSG rules that allow or block specific ports to specific subnets.</span></span> |
| [<span data-ttu-id="dae0c-131">Nowe AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="dae0c-131">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="dae0c-132">Tworzy maszyny wirtualne i dołącza karty Sieciowej na każdej maszynie Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="dae0c-132">Creates virtual machines and attaches a NIC to each VM.</span></span> <span data-ttu-id="dae0c-133">To polecenie określa również obraz maszyny wirtualnej do użycia i poświadczenia administracyjne.</span><span class="sxs-lookup"><span data-stu-id="dae0c-133">This command also specifies the virtual machine image to use and administrative credentials.</span></span> |
| [<span data-ttu-id="dae0c-134">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="dae0c-134">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="dae0c-135">Usuwa grupę zasobów i wszystkie zasoby, które zawiera.</span><span class="sxs-lookup"><span data-stu-id="dae0c-135">Deletes a resource group and all resources it contains.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="dae0c-136">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="dae0c-136">Next steps</span></span>

<span data-ttu-id="dae0c-137">Aby uzyskać więcej informacji dotyczących programu Azure PowerShell, zobacz [dokumentacji programu Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="dae0c-137">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/overview).</span></span>

<span data-ttu-id="dae0c-138">Dodatkowe przykłady skryptów PowerShell sieci można znaleźć w [Azure Przegląd dokumentacji](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="dae0c-138">Additional networking PowerShell script samples can be found in the [Azure Networking Overview documentation](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>