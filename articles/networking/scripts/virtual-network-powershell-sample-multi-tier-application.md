---
title: "aaaAzure przykładowy skrypt programu PowerShell — tworzenie sieci dla aplikacji wielowarstwowych | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 46d6d16dc5dbc8be467359f31346f017727b1abe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-network-for-multi-tier-applications"></a><span data-ttu-id="08f9d-103">Tworzenie sieci dla aplikacji wielowarstwowych</span><span class="sxs-lookup"><span data-stu-id="08f9d-103">Create a network for multi-tier applications</span></span>

<span data-ttu-id="08f9d-104">Ten przykładowy skrypt tworzy sieć wirtualną z podsieci frontonu i zaplecza.</span><span class="sxs-lookup"><span data-stu-id="08f9d-104">This script sample creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="08f9d-105">Podsieci frontonu toohello ruchu jest ograniczony tooHTTP i SSH, podczas toohello ruchu podsieci wewnętrznej jest ograniczona tooMySQL, port 3306.</span><span class="sxs-lookup"><span data-stu-id="08f9d-105">Traffic toohello front-end subnet is limited tooHTTP and SSH, while traffic toohello back-end subnet is limited tooMySQL, port 3306.</span></span> <span data-ttu-id="08f9d-106">Po uruchamianie skryptu hello masz dwie maszyny wirtualne, w każdej podsieci, którą można wdrożyć serwera sieci web i MySQL oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="08f9d-106">After running hello script, you will have two virtual machines, one in each subnet that you can deploy web server and MySQL software to.</span></span>

<span data-ttu-id="08f9d-107">W razie potrzeby zainstaluj hello Azure PowerShell przy użyciu instrukcji hello znalezione w hello [Przewodnik programu Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), a następnie uruchom `Login-AzureRmAccount` toocreate połączenia z platformą Azure.</span><span class="sxs-lookup"><span data-stu-id="08f9d-107">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="08f9d-108">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="08f9d-108">Sample script</span></span>


[!code-powershell[main](../../../powershell_scripts/virtual-network/virtual-network-multi-tier-application/virtual-network-multi-tier-application.ps1  "Virtual network for multi-tier application")]

## <a name="clean-up-deployment"></a><span data-ttu-id="08f9d-109">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="08f9d-109">Clean up deployment</span></span> 

<span data-ttu-id="08f9d-110">Hello uruchom następujące polecenie, grupy zasobów hello tooremove, maszyny Wirtualnej i wszystkich powiązanych zasobów.</span><span class="sxs-lookup"><span data-stu-id="08f9d-110">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="08f9d-111">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="08f9d-111">Script explanation</span></span>

<span data-ttu-id="08f9d-112">Ten skrypt używa powitania po toocreate poleceń, grupy zasobów, sieci wirtualnej i grup zabezpieczeń sieci.</span><span class="sxs-lookup"><span data-stu-id="08f9d-112">This script uses hello following commands toocreate a resource group, virtual network,  and network security groups.</span></span> <span data-ttu-id="08f9d-113">Każde polecenie w dokumentacji konkretnego toocommand łącza tabeli hello.</span><span class="sxs-lookup"><span data-stu-id="08f9d-113">Each command in hello table links toocommand-specific documentation.</span></span>

| <span data-ttu-id="08f9d-114">Polecenie</span><span class="sxs-lookup"><span data-stu-id="08f9d-114">Command</span></span> | <span data-ttu-id="08f9d-115">Uwagi</span><span class="sxs-lookup"><span data-stu-id="08f9d-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="08f9d-116">Nowe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="08f9d-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="08f9d-117">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="08f9d-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="08f9d-118">Nowy AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="08f9d-118">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="08f9d-119">Tworzy sieć wirtualna platformy Azure i podsieci frontonu.</span><span class="sxs-lookup"><span data-stu-id="08f9d-119">Creates an Azure virtual network and front-end subnet.</span></span> |
| [<span data-ttu-id="08f9d-120">Nowe AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="08f9d-120">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="08f9d-121">Tworzy podsieć zaplecza.</span><span class="sxs-lookup"><span data-stu-id="08f9d-121">Creates a back-end subnet.</span></span> |
| [<span data-ttu-id="08f9d-122">Nowe AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="08f9d-122">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="08f9d-123">Tworzy publicznego adresu IP adres tooaccess hello maszyny Wirtualnej na podstawie hello Internet.</span><span class="sxs-lookup"><span data-stu-id="08f9d-123">Creates a public IP address tooaccess hello VM from hello Internet.</span></span> |
| [<span data-ttu-id="08f9d-124">Nowe AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="08f9d-124">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="08f9d-125">Tworzy interfejsy sieci wirtualnej i dołącza je podsieci sieci wirtualnej toohello frontonu i zaplecza.</span><span class="sxs-lookup"><span data-stu-id="08f9d-125">Creates virtual network interfaces and attaches them toohello virtual network's front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="08f9d-126">Nowe AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="08f9d-126">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="08f9d-127">Tworzy grupy zabezpieczeń sieci (NSG), które są skojarzone toohello podsieci frontonu i zaplecza.</span><span class="sxs-lookup"><span data-stu-id="08f9d-127">Creates network security groups (NSG) that are associated toohello front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="08f9d-128">Nowe AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="08f9d-128">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) |<span data-ttu-id="08f9d-129">Tworzy reguły NSG, które zezwala lub blokuje określone porty toospecific podsieci.</span><span class="sxs-lookup"><span data-stu-id="08f9d-129">Creates NSG rules that allow or block specific ports toospecific subnets.</span></span> |
| [<span data-ttu-id="08f9d-130">Nowe AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="08f9d-130">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="08f9d-131">Tworzy maszyny wirtualne i dołącza tooeach karty Sieciowej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="08f9d-131">Creates virtual machines and attaches a NIC tooeach VM.</span></span> <span data-ttu-id="08f9d-132">To polecenie określa również toouse obrazu maszyny wirtualnej hello i poświadczenia administracyjne.</span><span class="sxs-lookup"><span data-stu-id="08f9d-132">This command also specifies hello virtual machine image toouse and administrative credentials.</span></span> |
| [<span data-ttu-id="08f9d-133">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="08f9d-133">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="08f9d-134">Usuwa grupę zasobów i wszystkie zasoby, które zawiera.</span><span class="sxs-lookup"><span data-stu-id="08f9d-134">Deletes a resource group and all resources it contains.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="08f9d-135">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="08f9d-135">Next steps</span></span>

<span data-ttu-id="08f9d-136">Aby uzyskać więcej informacji na powitania programu Azure PowerShell, zobacz [dokumentacji programu Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="08f9d-136">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/overview).</span></span>

<span data-ttu-id="08f9d-137">Dodatkowe przykłady skryptów PowerShell sieci można znaleźć w hello [Azure Przegląd dokumentacji](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="08f9d-137">Additional networking PowerShell script samples can be found in hello [Azure Networking Overview documentation](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>
