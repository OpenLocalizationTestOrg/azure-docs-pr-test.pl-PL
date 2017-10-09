---
title: aaaRedeploy maszyn wirtualnych systemu Windows na platformie Azure | Dokumentacja firmy Microsoft
description: "Jak wystawia tooredeploy maszyn wirtualnych Windows Azure toomitigate połączenia RDP."
services: virtual-machines-windows
documentationcenter: virtual-machines
author: genlin
manager: timlt
tags: azure-resource-manager,top-support-issue
ms.assetid: 0ee456ee-4595-4a14-8916-72c9110fc8bd
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: support-article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/26/2017
ms.author: genli
ms.openlocfilehash: 903d9d5bf241075931ee4b746690c553d808a58f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="redeploy-windows-virtual-machine-toonew-azure-node"></a><span data-ttu-id="84507-103">Należy ponownie wdrożyć toonew maszyny wirtualnej systemu Windows Azure węzła</span><span class="sxs-lookup"><span data-stu-id="84507-103">Redeploy Windows virtual machine toonew Azure node</span></span>
<span data-ttu-id="84507-104">Jeśli został skierowany trudności Rozwiązywanie problemów z pulpitu zdalnego (RDP) połączenia lub aplikacji dostęp do opartych na tooWindows Azure maszyny wirtualnej (VM), ponowne rozmieszczanie hello maszyny Wirtualnej może pomóc.</span><span class="sxs-lookup"><span data-stu-id="84507-104">If you have been facing difficulties troubleshooting Remote Desktop (RDP) connection or application access tooWindows-based Azure virtual machine (VM), redeploying hello VM may help.</span></span> <span data-ttu-id="84507-105">Podczas ponownego wdrażania maszyny Wirtualnej przenosi do nowego węzła tooa hello maszyny Wirtualnej w ramach hello infrastruktury platformy Azure i uprawnień go ponownie na zachowaniu opcji konfiguracji i skojarzonych zasobów.</span><span class="sxs-lookup"><span data-stu-id="84507-105">When you redeploy a VM, it moves hello VM tooa new node within hello Azure infrastructure and then powers it back on, retaining all your configuration options and associated resources.</span></span> <span data-ttu-id="84507-106">W tym artykule opisano sposób tooredeploy a maszyny Wirtualnej przy użyciu programu Azure PowerShell lub hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="84507-106">This article shows you how tooredeploy a VM using Azure PowerShell or hello Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="84507-107">Po ponownego wdrażania maszyny Wirtualnej, dysku tymczasowym hello zostaną utracone i dynamicznych adresów IP skojarzonych z interfejsu sieci wirtualnej zostały zaktualizowane.</span><span class="sxs-lookup"><span data-stu-id="84507-107">After you redeploy a VM, hello temporary disk is lost and dynamic IP addresses associated with virtual network interface are updated.</span></span> 


## <a name="using-azure-powershell"></a><span data-ttu-id="84507-108">Korzystanie z programu Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="84507-108">Using Azure PowerShell</span></span>
<span data-ttu-id="84507-109">Upewnij się, że ma hello najnowsze programu Azure PowerShell 1.x zainstalowana na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="84507-109">Make sure you have hello latest Azure PowerShell 1.x installed on your machine.</span></span> <span data-ttu-id="84507-110">Aby uzyskać więcej informacji, zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="84507-110">For more information, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="84507-111">Witaj poniższy przykład wdraża hello maszyny Wirtualnej o nazwie `myVM` hello grupy zasobów o nazwie `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="84507-111">hello following example deploys hello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>

```powershell
Set-AzureRmVM -Redeploy -ResourceGroupName "myResourceGroup" -Name "myVM"
```


[!INCLUDE [virtual-machines-common-redeploy-to-new-node](../../../includes/virtual-machines-common-redeploy-to-new-node.md)]

## <a name="next-steps"></a><span data-ttu-id="84507-112">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="84507-112">Next steps</span></span>
<span data-ttu-id="84507-113">Jeśli występują problemy dotyczące łączenia tooyour maszyny Wirtualnej, można znaleźć pomoc w [Rozwiązywanie problemów z połączeniami RDP](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) lub [szczegółowe kroki rozwiązywania problemów RDP](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="84507-113">If you are having issues connecting tooyour VM, you can find specific help on [troubleshooting RDP connections](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) or [detailed RDP troubleshooting steps](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="84507-114">Jeśli nie można uzyskać dostęp do aplikacji działających na maszynie Wirtualnej, możesz przeczytać [aplikacji Rozwiązywanie problemów z](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="84507-114">If you cannot access an application running on your VM, you can also read [application troubleshooting issues](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

