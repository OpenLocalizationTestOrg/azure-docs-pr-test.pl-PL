---
title: "aaaMove Maszynę wirtualną systemu Linux na platformie Azure | Dokumentacja firmy Microsoft"
description: "Przenoszenie maszyny Wirtualnej systemu Linux tooanother subskrypcji platformy Azure lub grupy zasobów w modelu wdrażania usługi Resource Manager hello."
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: d635f0a5-4458-4b95-a5f8-eed4f41eb4d4
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: article
ms.date: 03/22/2017
ms.author: cynthn
ms.openlocfilehash: 938d04234059111912f03e72d14dabd338bc0678
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="move-a-linux-vm-tooanother-subscription-or-resource-group"></a><span data-ttu-id="fc37f-103">Przenieś grupę zasobów lub subskrypcji tooanother maszyny Wirtualnej systemu Linux</span><span class="sxs-lookup"><span data-stu-id="fc37f-103">Move a Linux VM tooanother subscription or resource group</span></span>
<span data-ttu-id="fc37f-104">W tym artykule przedstawiono sposób toomove maszyny Wirtualnej systemu Linux, między grupami zasobów lub subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="fc37f-104">This article walks you through how toomove a Linux VM between resource groups or subscriptions.</span></span> <span data-ttu-id="fc37f-105">Przenoszenie maszyny Wirtualnej między subskrypcjami mogą być przydatne, jeśli utworzono Maszynę wirtualną w osobistych subskrypcji i teraz toomove go subskrypcji tooyour firmy.</span><span class="sxs-lookup"><span data-stu-id="fc37f-105">Moving a VM between subscriptions can be handy if you created a VM in a personal subscription and now want toomove it tooyour company's subscription.</span></span>

> [!IMPORTANT]
><span data-ttu-id="fc37f-106">Nie można przenieść dysków zarządzanych w tej chwili.</span><span class="sxs-lookup"><span data-stu-id="fc37f-106">You cannot move Managed Disks at this time.</span></span> 
>
><span data-ttu-id="fc37f-107">Nowych identyfikatorów zasobów są tworzone w ramach przeniesienia hello.</span><span class="sxs-lookup"><span data-stu-id="fc37f-107">New resource IDs are created as part of hello move.</span></span> <span data-ttu-id="fc37f-108">Po hello maszyny Wirtualnej został przeniesiony, należy tooupdate narzędzia i skrypty toouse hello nowego zasobu identyfikatorów.</span><span class="sxs-lookup"><span data-stu-id="fc37f-108">Once hello VM has been moved, you need tooupdate your tools and scripts toouse hello new resource IDs.</span></span> 
> 
> 

## <a name="use-hello-azure-cli-toomove-a-vm"></a><span data-ttu-id="fc37f-109">Użyj hello Azure CLI toomove maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="fc37f-109">Use hello Azure CLI toomove a VM</span></span>
<span data-ttu-id="fc37f-110">toosuccessfully przenieść Maszynę wirtualną, należy toomove hello maszyny Wirtualnej i wszystkie dodatkowe zasoby.</span><span class="sxs-lookup"><span data-stu-id="fc37f-110">toosuccessfully move a VM, you need toomove hello VM and all its supporting resources.</span></span> <span data-ttu-id="fc37f-111">Użyj hello **Pokaż grupy azure** polecenia toolist wszystkie zasoby hello w grupie zasobów i ich identyfikatorów.</span><span class="sxs-lookup"><span data-stu-id="fc37f-111">Use hello **azure group show** command toolist all hello resources in a resource group and their IDs.</span></span> <span data-ttu-id="fc37f-112">Pomaga toopipe hello dane wyjściowe tego polecenia tooa pliku, więc można skopiować i wkleić hello identyfikatorów na nowsze poleceń.</span><span class="sxs-lookup"><span data-stu-id="fc37f-112">It helps toopipe hello output of this command tooa file so you can copy and paste hello IDs into later commands.</span></span>

    azure group show <resourceGroupName>

<span data-ttu-id="fc37f-113">toomove Maszynę wirtualną i jego grupa zasobów tooanother zasoby, używać hello **przenoszenia zasobów platformy azure** polecenia interfejsu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="fc37f-113">toomove a VM and its resources tooanother resource group, use hello **azure resource move** CLI command.</span></span> <span data-ttu-id="fc37f-114">Witaj poniższy przykład pokazuje, jak toomove Maszynę wirtualną i zasoby najczęściej hello wymaga.</span><span class="sxs-lookup"><span data-stu-id="fc37f-114">hello following example shows how toomove a VM and hello most common resources it requires.</span></span> <span data-ttu-id="fc37f-115">Używamy hello **-i** parametru i przekazać na liście rozdzielanej przecinkami (bez spacji) identyfikatorów dla hello toomove zasobów.</span><span class="sxs-lookup"><span data-stu-id="fc37f-115">We use hello **-i** parameter and pass in a comma-separated list (without spaces) of IDs for hello resources toomove.</span></span>

    vm=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Compute/virtualMachines/<vmName>
    nic=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Network/networkInterfaces/<nicName>
    nsg=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Network/networkSecurityGroups/<nsgName>
    pip=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Network/publicIPAddresses/<publicIPName>
    vnet=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Network/virtualNetworks/<vnetName>
    diag=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Storage/storageAccounts/<diagnosticStorageAccountName>
    storage=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Storage/storageAccounts/<storageAcountName>      

    azure resource move --ids $vm,$nic,$nsg,$pip,$vnet,$storage,$diag -d "<destinationResourceGroup>"

<span data-ttu-id="fc37f-116">Jeśli chcesz, aby toomove hello maszyny Wirtualnej i jej zasobów tooa innej subskrypcji, dodawać hello **— identyfikator subskrypcji docelowej &#60; destinationSubscriptionID &#62;** parametru toospecify hello docelowej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="fc37f-116">If you want toomove hello VM and its resources tooa different subscription, add hello **--destination-subscriptionId &#60;destinationSubscriptionID&#62;** parameter toospecify hello destination subscription.</span></span>

<span data-ttu-id="fc37f-117">Jeśli pracujesz z hello wiersza polecenia na komputerze z systemem Windows, należy tooadd  **$**  przed nazwy zmiennych hello przy deklarowaniu je.</span><span class="sxs-lookup"><span data-stu-id="fc37f-117">If you are working from hello Command Prompt on a Windows computer, you need tooadd a **$** in front of hello variable names when you declare them.</span></span> <span data-ttu-id="fc37f-118">To nie jest wymagana w systemie Linux.</span><span class="sxs-lookup"><span data-stu-id="fc37f-118">This isn't needed in Linux.</span></span>

<span data-ttu-id="fc37f-119">Pojawi się monit, które mają toomove hello tooconfirm określony zasób.</span><span class="sxs-lookup"><span data-stu-id="fc37f-119">You are asked tooconfirm that you want toomove hello specified resource.</span></span> <span data-ttu-id="fc37f-120">Typ **Y** tooconfirm, które mają toomove hello zasobów.</span><span class="sxs-lookup"><span data-stu-id="fc37f-120">Type **Y** tooconfirm that you want toomove hello resources.</span></span>

[!INCLUDE [virtual-machines-common-move-vm](../../../includes/virtual-machines-common-move-vm.md)]

## <a name="next-steps"></a><span data-ttu-id="fc37f-121">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="fc37f-121">Next steps</span></span>
<span data-ttu-id="fc37f-122">Wiele różnych typów zasobów można przenosić między grupami zasobów i subskrypcje.</span><span class="sxs-lookup"><span data-stu-id="fc37f-122">You can move many different types of resources between resource groups and subscriptions.</span></span> <span data-ttu-id="fc37f-123">Aby uzyskać więcej informacji, zobacz [przenieść grupy zasobów toonew zasobów lub subskrypcji](../../resource-group-move-resources.md).</span><span class="sxs-lookup"><span data-stu-id="fc37f-123">For more information, see [Move resources toonew resource group or subscription](../../resource-group-move-resources.md).</span></span>    

