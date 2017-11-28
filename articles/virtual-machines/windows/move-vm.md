---
title: Przenoszenie zasobu maszyny Wirtualnej systemu Windows na platformie Azure | Dokumentacja firmy Microsoft
description: "Przenieś Maszynę wirtualną systemu Windows do innego Azure subskrypcji lub grupy zasobów w modelu wdrażania usługi Resource Manager."
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
ms.openlocfilehash: 1db25a5d9ff5cb6aa2787a0cafa40cfb010e3b06
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="move-a-windows-vm-to-another-azure-subscription-or-resource-group"></a><span data-ttu-id="8c2aa-103">Przenieś Maszynę wirtualną systemu Windows do innego Azure subskrypcji lub grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="8c2aa-103">Move a Windows VM to another Azure subscription or resource group</span></span>
<span data-ttu-id="8c2aa-104">W tym artykule przedstawiono sposób przenoszenia maszyny Wirtualnej systemu Windows między grupami zasobów lub subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="8c2aa-104">This article walks you through how to move a Windows VM between resource groups or subscriptions.</span></span> <span data-ttu-id="8c2aa-105">Przenoszenie między subskrypcjami można skorzystać, jeśli pierwotnie utworzono Maszynę wirtualną w osobistych subskrypcji i chcesz teraz Przenieś go do subskrypcji w firmie, aby kontynuować pracę.</span><span class="sxs-lookup"><span data-stu-id="8c2aa-105">Moving between subscriptions can be handy if you originally created a VM in a personal subscription and now want to move it to your company's subscription to continue your work.</span></span>

> [!IMPORTANT]
><span data-ttu-id="8c2aa-106">Nie można przenieść dysków zarządzanych w tej chwili.</span><span class="sxs-lookup"><span data-stu-id="8c2aa-106">You cannot move Managed Disks at this time.</span></span> 
>
><span data-ttu-id="8c2aa-107">Nowych identyfikatorów zasobów są tworzone w ramach przeniesienia.</span><span class="sxs-lookup"><span data-stu-id="8c2aa-107">New resource IDs are created as part of the move.</span></span> <span data-ttu-id="8c2aa-108">Po przeniesieniu maszyny Wirtualnej należy zaktualizować narzędzia i skrypty do używania nowych identyfikatorów zasobów.</span><span class="sxs-lookup"><span data-stu-id="8c2aa-108">Once the VM has been moved, you need to update your tools and scripts to use the new resource IDs.</span></span> 
> 
> 

[!INCLUDE [virtual-machines-common-move-vm](../../../includes/virtual-machines-common-move-vm.md)]

## <a name="use-powershell-to-move-a-vm"></a><span data-ttu-id="8c2aa-109">Aby przenieść Maszynę wirtualną za pomocą programu Powershell</span><span class="sxs-lookup"><span data-stu-id="8c2aa-109">Use Powershell to move a VM</span></span>
<span data-ttu-id="8c2aa-110">Aby przenieść maszynę wirtualną w innej grupie zasobów, musisz upewnij się, że można również przenieść wszystkie zasoby zależne.</span><span class="sxs-lookup"><span data-stu-id="8c2aa-110">To move a virtual machine to another resource group, you need to make sure that you also move all of the dependent resources.</span></span> <span data-ttu-id="8c2aa-111">Korzystanie z polecenia cmdlet Move-AzureRMResource wymaga nazwy zasobu i typu zasobu.</span><span class="sxs-lookup"><span data-stu-id="8c2aa-111">To use the Move-AzureRMResource cmdlet, you need the resource name and the type of resource.</span></span> <span data-ttu-id="8c2aa-112">Możesz uzyskać zarówno z polecenia cmdlet AzureRMResource Znajdź.</span><span class="sxs-lookup"><span data-stu-id="8c2aa-112">You can get both from the Find-AzureRMResource cmdlet.</span></span>

    Find-AzureRMResource -ResourceGroupNameContains "<sourceResourceGroupName>"


<span data-ttu-id="8c2aa-113">Aby przenieść Maszynę wirtualną, trzeba przenieść wiele zasobów.</span><span class="sxs-lookup"><span data-stu-id="8c2aa-113">To move a VM we need to move multiple resources.</span></span> <span data-ttu-id="8c2aa-114">Firma Microsoft wystarczy utworzyć oddzielne zmienne dla każdego zasobu, a następnie na liście.</span><span class="sxs-lookup"><span data-stu-id="8c2aa-114">We can just create separate variables for each resource and then list them.</span></span> <span data-ttu-id="8c2aa-115">W tym przykładzie zawiera większość podstawowych zasobów dla maszyny Wirtualnej, ale można dodać więcej zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="8c2aa-115">This example includes most of the basic resources for a VM, but you can add more as needed.</span></span>

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

<span data-ttu-id="8c2aa-116">Przeniesienie zasobów do innej subskrypcji, obejmują **- DestinationSubscriptionId** parametru.</span><span class="sxs-lookup"><span data-stu-id="8c2aa-116">To move the resources to different subscription, include the **-DestinationSubscriptionId** parameter.</span></span> 

    Move-AzureRmResource -DestinationSubscriptionId "<destinationSubscriptionID>" -DestinationResourceGroupName $destinationRG -ResourceId $vm.ResourceId, $storageAccount.ResourceId, $diagStorageAccount.ResourceId, $vNet.ResourceId, $nic.ResourceId, $ip.ResourceId, $nsg.ResourceId



<span data-ttu-id="8c2aa-117">Użytkownik jest proszony o potwierdzenie, że chcesz przenieść określonych zasobów.</span><span class="sxs-lookup"><span data-stu-id="8c2aa-117">You will be asked to confirm that you want to move the specified resources.</span></span> <span data-ttu-id="8c2aa-118">Typ **Y** aby upewnić się, że chcesz przenieść zasoby.</span><span class="sxs-lookup"><span data-stu-id="8c2aa-118">Type **Y** to confirm that you want to move the resources.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8c2aa-119">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="8c2aa-119">Next steps</span></span>
<span data-ttu-id="8c2aa-120">Wiele różnych typów zasobów można przenosić między grupami zasobów i subskrypcje.</span><span class="sxs-lookup"><span data-stu-id="8c2aa-120">You can move many different types of resources between resource groups and subscriptions.</span></span> <span data-ttu-id="8c2aa-121">Aby uzyskać więcej informacji, zobacz [Move resources to new resource group or subscription](../../resource-group-move-resources.md) (Przenoszenie zasobów do nowej grupy lub subskrypcji).</span><span class="sxs-lookup"><span data-stu-id="8c2aa-121">For more information, see [Move resources to new resource group or subscription](../../resource-group-move-resources.md).</span></span>    

