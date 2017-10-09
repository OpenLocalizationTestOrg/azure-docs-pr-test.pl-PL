---
title: aaaMove zasobu maszyny Wirtualnej systemu Windows na platformie Azure | Dokumentacja firmy Microsoft
description: "Przenieś maszynę Wirtualną systemu Windows tooanother subskrypcji platformy Azure lub grupy zasobów w modelu wdrażania usługi Resource Manager hello."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 4e383427-4aff-4bf3-a0f4-dbff5c6f0c81
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/22/2017
ms.author: cynthn
ms.openlocfilehash: 859e78dce9acf1168780d4ee8e9f6dac0e3c11cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="move-a-windows-vm-tooanother-azure-subscription-or-resource-group"></a><span data-ttu-id="84da5-103">Przenieś maszynę Wirtualną systemu Windows tooanother subskrypcji platformy Azure lub grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="84da5-103">Move a Windows VM tooanother Azure subscription or resource group</span></span>
<span data-ttu-id="84da5-104">W tym artykule przedstawiono sposób toomove maszyny Wirtualnej systemu Windows, między grupami zasobów lub subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="84da5-104">This article walks you through how toomove a Windows VM between resource groups or subscriptions.</span></span> <span data-ttu-id="84da5-105">Przenoszenie między subskrypcjami mogą być przydatne, jeśli pierwotnie utworzono Maszynę wirtualną w osobistych subskrypcji i teraz toomove on toocontinue subskrypcji firmy tooyour swoją pracę.</span><span class="sxs-lookup"><span data-stu-id="84da5-105">Moving between subscriptions can be handy if you originally created a VM in a personal subscription and now want toomove it tooyour company's subscription toocontinue your work.</span></span>

> [!IMPORTANT]
><span data-ttu-id="84da5-106">Nie można przenieść dysków zarządzanych w tej chwili.</span><span class="sxs-lookup"><span data-stu-id="84da5-106">You cannot move Managed Disks at this time.</span></span> 
>
><span data-ttu-id="84da5-107">Nowych identyfikatorów zasobów są tworzone w ramach przeniesienia hello.</span><span class="sxs-lookup"><span data-stu-id="84da5-107">New resource IDs are created as part of hello move.</span></span> <span data-ttu-id="84da5-108">Po hello maszyny Wirtualnej został przeniesiony, należy tooupdate narzędzia i skrypty toouse hello nowego zasobu identyfikatorów.</span><span class="sxs-lookup"><span data-stu-id="84da5-108">Once hello VM has been moved, you need tooupdate your tools and scripts toouse hello new resource IDs.</span></span> 
> 
> 

[!INCLUDE [virtual-machines-common-move-vm](../../../includes/virtual-machines-common-move-vm.md)]

## <a name="use-powershell-toomove-a-vm"></a><span data-ttu-id="84da5-109">Użyj programu Powershell toomove maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="84da5-109">Use Powershell toomove a VM</span></span>
<span data-ttu-id="84da5-110">toomove grupę zasobów tooanother maszyny wirtualnej, należy się również o przeniesieniu wszystkich zasobów zależnych hello toomake.</span><span class="sxs-lookup"><span data-stu-id="84da5-110">toomove a virtual machine tooanother resource group, you need toomake sure that you also move all of hello dependent resources.</span></span> <span data-ttu-id="84da5-111">polecenia cmdlet Move-AzureRMResource hello toouse, potrzebna Nazwa zasobu hello i hello typu zasobu.</span><span class="sxs-lookup"><span data-stu-id="84da5-111">toouse hello Move-AzureRMResource cmdlet, you need hello resource name and hello type of resource.</span></span> <span data-ttu-id="84da5-112">Możesz uzyskać zarówno z polecenia cmdlet hello AzureRMResource Znajdź.</span><span class="sxs-lookup"><span data-stu-id="84da5-112">You can get both from hello Find-AzureRMResource cmdlet.</span></span>

    Find-AzureRMResource -ResourceGroupNameContains "<sourceResourceGroupName>"


<span data-ttu-id="84da5-113">toomove potrzebujemy toomove wielu zasobów maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="84da5-113">toomove a VM we need toomove multiple resources.</span></span> <span data-ttu-id="84da5-114">Firma Microsoft wystarczy utworzyć oddzielne zmienne dla każdego zasobu, a następnie na liście.</span><span class="sxs-lookup"><span data-stu-id="84da5-114">We can just create separate variables for each resource and then list them.</span></span> <span data-ttu-id="84da5-115">W tym przykładzie obejmuje większość hello podstawowych zasobów dla maszyny Wirtualnej, ale można dodać więcej zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="84da5-115">This example includes most of hello basic resources for a VM, but you can add more as needed.</span></span>

    $sourceRG = "<sourceResourceGroupName>"
    $destinationRG = "<destinationResourceGroupName>"

    $vm = Get-AzureRmResource -ResourceGroupName $sourceRG -ResourceType "Microsoft.Compute/virtualMachines" -ResourceName "<vmName>"
    $storageAccount = Get-AzureRmResource -ResourceGroupName $sourceRG -ResourceType "Microsoft.Storage/storageAccounts" -ResourceName "<storageAccountName>"
    $diagStorageAccount = Get-AzureRmResource -ResourceGroupName $sourceRG -ResourceType "Microsoft.Storage/storageAccounts" -ResourceName "<diagnosticStorageAccountName>"
    $vNet = Get-AzureRmResource -ResourceGroupName $sourceRG -ResourceType "Microsoft.Network/virtualNetworks" -ResourceName "<vNetName>"
    $nic = Get-AzureRmResource -ResourceGroupName $sourceRG -ResourceType "Microsoft.Network/networkInterfaces" -ResourceName "<nicName>"
    $ip = Get-AzureRmResource -ResourceGroupName $sourceRG -ResourceType "Microsoft.Network/publicIPAddresses" -ResourceName "<ipName>"
    $nsg = Get-AzureRmResource -ResourceGroupName $sourceRG -ResourceType "Microsoft.Network/networkSecurityGroups" -ResourceName "<nsgName>"

    Move-AzureRmResource -DestinationResourceGroupName $destinationRG -ResourceId $vm.ResourceId, $storageAccount.ResourceId, $diagStorageAccount.ResourceId, $vNet.ResourceId, $nic.ResourceId, $ip.ResourceId, $nsg.ResourceId

<span data-ttu-id="84da5-116">toomove hello zasobów toodifferent subskrypcji, obejmują hello **- DestinationSubscriptionId** parametru.</span><span class="sxs-lookup"><span data-stu-id="84da5-116">toomove hello resources toodifferent subscription, include hello **-DestinationSubscriptionId** parameter.</span></span> 

    Move-AzureRmResource -DestinationSubscriptionId "<destinationSubscriptionID>" -DestinationResourceGroupName $destinationRG -ResourceId $vm.ResourceId, $storageAccount.ResourceId, $diagStorageAccount.ResourceId, $vNet.ResourceId, $nic.ResourceId, $ip.ResourceId, $nsg.ResourceId



<span data-ttu-id="84da5-117">Konieczne będzie podanie tooconfirm, które mają toomove hello określonych zasobów.</span><span class="sxs-lookup"><span data-stu-id="84da5-117">You will be asked tooconfirm that you want toomove hello specified resources.</span></span> <span data-ttu-id="84da5-118">Typ **Y** tooconfirm, które mają toomove hello zasobów.</span><span class="sxs-lookup"><span data-stu-id="84da5-118">Type **Y** tooconfirm that you want toomove hello resources.</span></span>

## <a name="next-steps"></a><span data-ttu-id="84da5-119">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="84da5-119">Next steps</span></span>
<span data-ttu-id="84da5-120">Wiele różnych typów zasobów można przenosić między grupami zasobów i subskrypcje.</span><span class="sxs-lookup"><span data-stu-id="84da5-120">You can move many different types of resources between resource groups and subscriptions.</span></span> <span data-ttu-id="84da5-121">Aby uzyskać więcej informacji, zobacz [przenieść grupy zasobów toonew zasobów lub subskrypcji](../../resource-group-move-resources.md).</span><span class="sxs-lookup"><span data-stu-id="84da5-121">For more information, see [Move resources toonew resource group or subscription](../../resource-group-move-resources.md).</span></span>    

