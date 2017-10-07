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
# <a name="how-tooopen-ports-and-endpoints-tooa-vm-in-azure-using-powershell"></a>Jak tooopen portów i punkty końcowe tooa maszyny Wirtualnej na platformie Azure przy użyciu programu PowerShell
[!INCLUDE [virtual-machines-common-nsg-quickstart](../../../includes/virtual-machines-common-nsg-quickstart.md)]

## <a name="quick-commands"></a>Szybkie polecenia
Grupy zabezpieczeń sieci toocreate i reguły listy ACL należy [hello najnowszą wersję programu Azure PowerShell zainstalowany](/powershell/azureps-cmdlets-docs). Możesz również [wykonaj te czynności przy użyciu portalu Azure hello](nsg-quickstart-portal.md).

Zaloguj się tooyour konto platformy Azure:

```powershell
Login-AzureRmAccount
```

Poniższe przykłady w hello Zastąp przykładowe nazwy parametrów własne wartości. Przykład nazwy parametrów uwzględnione *myResourceGroup*, *myNetworkSecurityGroup*, i *myVnet*.

Utworzyć regułę z [AzureRmNetworkSecurityRuleConfig nowy](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig). Witaj poniższy przykład powoduje utworzenie reguły o nazwie *myNetworkSecurityGroupRule* tooallow *tcp* ruch na porcie *80*:

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

Następnie utwórz grupy zabezpieczeń sieci z [AzureRmNetworkSecurityGroup nowy](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) i przypisz hello HTTP reguł utworzony w następujący sposób. Witaj poniższy przykład tworzy sieciową grupę zabezpieczeń o nazwie *myNetworkSecurityGroup*:

```powershell
$nsg = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName "myResourceGroup" `
    -Location "EastUS" `
    -Name "myNetworkSecurityGroup" `
    -SecurityRules $httprule
```

Teraz załóżmy przypisać podsieć tooa grupy zabezpieczeń sieci. Witaj w poniższym przykładzie przypisano istniejącej sieci wirtualnej o nazwie *myVnet* zmiennej toohello *$vnet* z [Get-AzureRmVirtualNetwork](/powershell/module/azurerm.network/get-azurermvirtualnetwork):

```powershell
$vnet = Get-AzureRmVirtualNetwork `
    -ResourceGroupName "myResourceGroup" `
    -Name "myVnet"
```

Skojarz grupy zabezpieczeń sieci z podsieci z [AzureRmVirtualNetworkSubnetConfig zestawu](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig). Witaj poniższy przykład powoduje skojarzenie podsieci hello o nazwie *mySubnet* z grupy zabezpieczeń sieci:

```powershell
$subnetPrefix = $vnet.Subnets|?{$_.Name -eq 'mySubnet'}

Set-AzureRmVirtualNetworkSubnetConfig `
    -VirtualNetwork $vnet `
    -Name "mySubnet" `
    -AddressPrefix $subnetPrefix.AddressPrefix `
    -NetworkSecurityGroup $nsg
```

Na koniec, aktualizacja sieci wirtualnej z [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork) aby Twoje mocą tootake zmiany:

```powershell
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
```


## <a name="more-information-on-network-security-groups"></a>Więcej informacji na temat grup zabezpieczeń sieci
Witaj w tym miejscu szybkie polecenia pozwalają tooget zapasowych i pracy z tooyour przechodzenia ruchu maszyny Wirtualnej. Grupy zabezpieczeń sieci stanowią wielu funkcje i poziom szczegółowości kontrolowanie dostęp do zasobów tooyour. Możesz przeczytać dodatkowe informacje [Tworzenie grupy zabezpieczeń sieci i listy ACL zasady tutaj](tutorial-virtual-network.md#manage-internal-traffic).

Dla aplikacji sieci web wysokiej dostępności należy umieszczać maszyny wirtualne za usługą równoważenia obciążenia Azure. Moduł równoważenia obciążenia Hello dystrybuuje tooVMs ruchu, z sieciową grupą zabezpieczeń, który umożliwia filtrowanie ruchu. Aby uzyskać więcej informacji, zobacz [jak maszyn saldo tooload wirtualnych systemu Linux, w Azure toocreate wysokiej dostępności aplikacji](tutorial-load-balancer.md).

## <a name="next-steps"></a>Następne kroki
W tym przykładzie utworzono ruch tooallow HTTP Prosta reguła. Można znaleźć informacje dotyczące tworzenia środowisk bardziej szczegółowe w hello następujące artykuły:

* [Omówienie usługi Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md)
* [Co to jest sieciowa grupa zabezpieczeń?](../../virtual-network/virtual-networks-nsg.md)
* [Omówienie usługi Azure Resource Manager dla usługi równoważenia obciążenia](../../load-balancer/load-balancer-arm.md)

