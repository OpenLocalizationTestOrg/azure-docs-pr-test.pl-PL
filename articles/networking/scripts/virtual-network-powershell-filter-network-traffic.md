---
title: "Przykładowy skrypt programu PowerShell aaaAzure — ruchu sieciowego maszyn wirtualnych filtru | Dokumentacja firmy Microsoft"
description: "Skrypt programu PowerShell Azure przykładowe — filtrowania ruchu przychodzącego i wychodzącego ruchu sieciowego maszyny Wirtualnej."
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
ms.openlocfilehash: 39eae6a43a8dc7f9fc616ef3ec50f95443fd3547
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="filter-inbound-and-outbound-vm-network-traffic"></a>Filtrowanie ruchu przychodzącego i wychodzącego ruchu sieciowego maszyny Wirtualnej

Ten przykładowy skrypt tworzy sieć wirtualną z podsieci frontonu i zaplecza. Ruchu przychodzącego ruchu sieciowego podsieci frontonu toohello jest tooHTTP ograniczona, a ruch protokołu HTTPS, gdy wychodzących toohello Internet z podsieci wewnętrznej hello jest niedozwolone. Po uruchomieniu skryptu hello, będziesz mieć jedną maszynę wirtualną z dwiema kartami sieciowymi. Poszczególne karty Sieciowe są połączone tooa innej podsieci.

W razie potrzeby zainstaluj hello Azure PowerShell przy użyciu instrukcji hello znalezione w hello [Przewodnik programu Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), a następnie uruchom `Login-AzureRmAccount` toocreate połączenia z platformą Azure.

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Przykładowy skrypt


[!code-powershell[main](../../../powershell_scripts/virtual-network/filter-network-traffic/filter-network-traffic.ps1  "Filter VM network traffic")]

## <a name="clean-up-deployment"></a>Czyszczenie wdrożenia 

Hello uruchom następujące polecenie, grupy zasobów hello tooremove, maszyny Wirtualnej i wszystkich powiązanych zasobów.

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a>Wyjaśnienie skryptu

Ten skrypt używa powitania po toocreate poleceń, grupy zasobów, sieci wirtualnej i grup zabezpieczeń sieci. Każde polecenie w dokumentacji konkretnego toocommand łącza tabeli hello.

| Polecenie | Uwagi |
|---|---|
| [Nowe AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) | Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby. |
| [Nowe AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | Tworzy obiekt konfiguracji podsieci |
| [Nowy AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | Tworzy sieć wirtualna platformy Azure i podsieci frontonu. |
| [Nowe AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | Tworzy toobe reguły zabezpieczeń przypisane tooa sieciowej grupy zabezpieczeń. |
| [Nowe AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) |Tworzy reguły NSG, które zezwala lub blokuje określone porty toospecific podsieci. |
| [Zestaw AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig) | Kojarzy toosubnets grup NSG. |
| [Nowe AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress) | Tworzy publicznego adresu IP adres tooaccess hello maszyny Wirtualnej na podstawie hello Internet. |
| [Nowe AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) | Tworzy interfejsy sieci wirtualnej i dołącza je podsieci sieci wirtualnej toohello frontonu i zaplecza. |
| [Nowe AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig) | Tworzy konfiguracji maszyny Wirtualnej. Ta konfiguracja zawiera informacje, takie jak nazwa maszyny Wirtualnej, system operacyjny i poświadczenia administracyjne. Konfiguracja Hello jest używany podczas tworzenia maszyny Wirtualnej. |
| [Nowe AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm) | Utwórz maszynę wirtualną. |
|[Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | Usuwa grupę zasobów i wszystkie zasoby zawarte w ciągu. |

## <a name="next-steps"></a>Następne kroki

Aby uzyskać więcej informacji na powitania programu Azure PowerShell, zobacz [dokumentacji programu Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).

Dodatkowe przykłady skryptów PowerShell sieci można znaleźć w hello [Azure Przegląd dokumentacji](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).
