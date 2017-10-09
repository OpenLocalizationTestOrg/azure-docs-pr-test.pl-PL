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
# <a name="redeploy-windows-virtual-machine-toonew-azure-node"></a>Należy ponownie wdrożyć toonew maszyny wirtualnej systemu Windows Azure węzła
Jeśli został skierowany trudności Rozwiązywanie problemów z pulpitu zdalnego (RDP) połączenia lub aplikacji dostęp do opartych na tooWindows Azure maszyny wirtualnej (VM), ponowne rozmieszczanie hello maszyny Wirtualnej może pomóc. Podczas ponownego wdrażania maszyny Wirtualnej przenosi do nowego węzła tooa hello maszyny Wirtualnej w ramach hello infrastruktury platformy Azure i uprawnień go ponownie na zachowaniu opcji konfiguracji i skojarzonych zasobów. W tym artykule opisano sposób tooredeploy a maszyny Wirtualnej przy użyciu programu Azure PowerShell lub hello portalu Azure.

> [!NOTE]
> Po ponownego wdrażania maszyny Wirtualnej, dysku tymczasowym hello zostaną utracone i dynamicznych adresów IP skojarzonych z interfejsu sieci wirtualnej zostały zaktualizowane. 


## <a name="using-azure-powershell"></a>Korzystanie z programu Azure PowerShell
Upewnij się, że ma hello najnowsze programu Azure PowerShell 1.x zainstalowana na tym komputerze. Aby uzyskać więcej informacji, zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).

Witaj poniższy przykład wdraża hello maszyny Wirtualnej o nazwie `myVM` hello grupy zasobów o nazwie `myResourceGroup`:

```powershell
Set-AzureRmVM -Redeploy -ResourceGroupName "myResourceGroup" -Name "myVM"
```


[!INCLUDE [virtual-machines-common-redeploy-to-new-node](../../../includes/virtual-machines-common-redeploy-to-new-node.md)]

## <a name="next-steps"></a>Następne kroki
Jeśli występują problemy dotyczące łączenia tooyour maszyny Wirtualnej, można znaleźć pomoc w [Rozwiązywanie problemów z połączeniami RDP](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) lub [szczegółowe kroki rozwiązywania problemów RDP](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Jeśli nie można uzyskać dostęp do aplikacji działających na maszynie Wirtualnej, możesz przeczytać [aplikacji Rozwiązywanie problemów z](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

