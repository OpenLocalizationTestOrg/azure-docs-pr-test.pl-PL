---
title: "Przykładowy skrypt programu PowerShell aaaAzure — ruch sieciowy przez urządzenie wirtualne sieci | Dokumentacja firmy Microsoft"
description: "Przykład skryptu usługi Azure PowerShell — ruch trasy przez urządzenie wirtualne zapory w sieci."
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
ms.openlocfilehash: 3b999f3289d654c00d5becb973e2883896457d52
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="route-traffic-through-a-network-virtual-appliance"></a>Kierować ruchem przez urządzenie wirtualne sieci

Ten przykładowy skrypt tworzy sieć wirtualną z podsieci frontonu i zaplecza. Tworzy również Maszynę wirtualną z tooroute włączone ruchu między dwiema podsieciami hello przekazywania pakietów IP. Po uruchomieniu skryptu hello można wdrażać oprogramowanie sieci, takie jak aplikacja zapory, toohello maszyny Wirtualnej.

W razie potrzeby zainstaluj hello Azure PowerShell przy użyciu instrukcji hello znalezione w hello [Przewodnik programu Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), a następnie uruchom `Login-AzureRmAccount` toocreate połączenia z platformą Azure.

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Przykładowy skrypt


[!code-powershell[main](../../../powershell_scripts/virtual-network/route-traffic-through-nva/route-traffic-through-nva.ps1 "Route traffic through a network virtual appliance")]

## <a name="clean-up-deployment"></a>Czyszczenie wdrożenia 

Hello uruchom następujące polecenie, grupy zasobów hello tooremove, maszyny Wirtualnej i wszystkich powiązanych zasobów.

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```
## <a name="script-explanation"></a>Wyjaśnienie skryptu

Ten skrypt używa powitania po toocreate poleceń, grupy zasobów, sieci wirtualnej i grup zabezpieczeń sieci. Każde polecenie w dokumentacji konkretnego toocommand łącza tabeli hello.

| Polecenie | Uwagi |
|---|---|
| [Nowe AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup)  | Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby. |
| [Nowy AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | Tworzy sieć wirtualna platformy Azure i podsieci frontonu. |
| [Nowe AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | Tworzy zaplecza i strefą DMZ podsieci. |
| [Nowe AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress) | Tworzy publicznego adresu IP adres tooaccess hello maszyny Wirtualnej na podstawie hello Internet. |
| [Nowe AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) | Tworzy interfejs sieci wirtualnej i Włącz przesyłanie dalej IP dla niego. |
| [Nowe AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | Tworzy sieciową grupę zabezpieczeń (NSG). |
| [Nowe AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | Tworzy reguły NSG, które zezwala na portach HTTP i HTTPS ruchu przychodzącego toohello maszyny Wirtualnej. |
| [Zestaw AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig)| Grupy NSG hello stowarzyszonych i toosubnets tabele tras. |
| [Nowe AzureRmRouteTable](/powershell/module/azurerm.network/new-azurermroutetable)| Tworzy tabelę tras dla wszystkich tras. |
| [Nowe AzureRMRouteConfig](/powershell/module/azurerm.network/new-azurermrouteconfig)| Tworzy tras tooroute ruch między podsieciami i hello Internet za pośrednictwem hello maszyny Wirtualnej. |
| [Nowe AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm) | Tworzy maszynę wirtualną i dołącza hello tooit karty Sieciowej. To polecenie określa również toouse obrazu maszyny wirtualnej hello i poświadczenia administracyjne. |
| [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup)  | Usuwa grupę zasobów i wszystkie zasoby, które zawiera. |

## <a name="next-steps"></a>Następne kroki

Aby uzyskać więcej informacji na powitania programu Azure PowerShell, zobacz [dokumentacji programu Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).

Dodatkowe przykłady skryptów PowerShell sieci można znaleźć w hello [Azure Przegląd dokumentacji](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).
